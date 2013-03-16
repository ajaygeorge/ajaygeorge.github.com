---
layout: post
title: "First among Equals"
date: 2013-03-17 00:37
comments: true
categories: java 
---
Much has been told about the ```Equals``` method in java. It's importance along with ```HashCode``` is well documented.

The contract of equals method states that it should be
> Reflexive, Symmetric, Transitive and Consistent.

Symmetry sounds easy, but could be extremely hard to get right.

The ```CaseInsensitive``` String example in Effective Java Item 8 is an excellent discussion on the same. Read it if you haven't read it already.

I was quite surprised to find the equals implementation broken in the [MongoDB Java Driver](https://jira.mongodb.org/browse/JAVA-609).

The equals Implementation:
``` java Equals code
    public boolean equals( Object o ){

        if ( this == o )
            return true;

        ObjectId other = massageToObjectId( o );
        if ( other == null )
            return false;

        return
            _time == other._time &&
            _machine == other._machine &&
            _inc == other._inc;
    }
```

The culprit is the massageToObjectId method used in the equals Implementation.
``` java
    /** Turn an object into an <code>ObjectId</code>, if possible.
     * Strings will be converted into <code>ObjectId</code>s, if possible, and <code>ObjectId</code>s will
     * be cast and returned.  Passing in <code>null</code> returns <code>null</code>.
     * @param o the object to convert
     * @return an <code>ObjectId</code> if it can be massaged, null otherwise
     */
    public static ObjectId massageToObjectId( Object o ){
        if ( o == null )
            return null;

        if ( o instanceof ObjectId )
            return (ObjectId)o;

        if ( o instanceof String ){
            String s = o.toString();
            if ( isValid( s ) )
                return new ObjectId( s );
        }

        return null;
    }
```
The author's intention is pure here. Take advantage of a String being represented as the ObjectID. 

But the issue is that now you can have ```ObjectId.equals(String)``` but not ```String.equals(ObjectId)``` which violates the Symmetry contract.

Fix would be remove the instanceof check for String and deal with only ObjectIds

Hope the core developers get around making this fix.

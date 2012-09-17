---
layout: post
title: "Why are com.sun.management.ThreadMXBean methods disabled in JConsole"
date: 2012-09-18 00:13
comments: true
categories: 
---
I had always wondered why some methods on the JConsole are disabled. You can see it in action if you check out the ThreadMXBean which is a part of the JDK
{% img http://i.stack.imgur.com/38lh7.png %}

I asked this question on SO and indeed got a wonderful reply.
Here is the reason :
{% codeblock %}
Only primitives, primitive wrappers and  additional Classes such as BigDecimal.class, BigInteger.class, Number.class, String.class, ObjectName.class are allowed as arguments to valid methods. 
{% endcodeblock %}
For the simple reason that JConsole does not know how to read up other objects as arguments to the exposed methods, they are disabled.
Read the complete discussion on SO [here](http://stackoverflow.com/questions/12025003/why-are-some-methods-on-the-jconsole-disabled) .

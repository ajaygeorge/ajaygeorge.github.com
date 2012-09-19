---
layout: post
title: "Switching off Camel Case in Octopress"
date: 2012-09-19 22:21
comments: true
categories: 
---
Ever wondered how to switch off [Camel Case](http://en.wikipedia.org/wiki/CamelCase) in Octopress?. By default Octopress has Camel case switched on for both pages and titles, which could be a bit annoying at times.  
[imathis](https://github.com/imathis) just committed an update using which you can switch off Camel Case. View the commit details [here](https://github.com/imathis/octopress/commit/3f842465bdd4e9dc2a735bb34a80fb6f78b387bb) .  

Breaking it down, here is what you have to do :
>
* Update to latest version of octopress.
* In your ```_config.yml``` change ```titlecase``` from true to false.
  That's it. !

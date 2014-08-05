---
layout: post
title: "The Problem with Libraries"
description: ""
category: Programming
tags: []
---
{% include JB/setup %}

Before I go too deep down this rat/rabbit hole, I should state that Libraries are what has allowed programming to
develop from where only the best of the best can produce software to a place where a plumber like me can still
produce some pretty amazing stuff.  Open source and libraries and tools have been the reason for the
explosion of amazing software and computer greatness in general of the 2000s.  We owe much to those who create
libraries, and contribute to libraries in any way.  You can probably thank jQuery for bringing Web 2.0 to 
all but the biggest web sites (which could afford to hire programmers to work through all of the browser
incompatibility issues) and for bringing about a resurgence in the web that resulted in HTML5.  

Modern web frameworks (really just a collection of libraries and generally methodology or code of practice for
using said libraries) brought a renaissance to web development with Ruby on Rails which basically changed the way that
websites were designed.  MVC was resurrected from the [Gang Of Four](http://en.wikipedia.org/wiki/Design_Patterns)
and became the defacto standard off how to build a website.   And I know that libraries have been
around as long as software has been written, and frameworks almost as long.  

However there is a downside to libraries and frameworks that becomes more prevalent with the explosion of 
libraries, and that is the explosion of complexity added to your project by including a library.  You take on
as a dependency all of the code written by the library that your code uses, plus any side effects that may
be caused by that code.  You are now responsible for keeping that library up to date (should any show-stopping bugs
or security flaws be found in said library), and frequently even with the advent of [semantic versioning](http://semver.org/)
updating a library will break things.  

I used to hate the nih[^nih] attitude and in a lot of ways I still do: if your core competency as a company is not
writing a payroll application, buy a payroll application do not write it yourself.  But the more I have worked with
libraries, and even very very good libraries written by people far more talented than myself, the more I find that
unless they are very easy to 

[^nih] Not invented here, were all technology must developed in house.
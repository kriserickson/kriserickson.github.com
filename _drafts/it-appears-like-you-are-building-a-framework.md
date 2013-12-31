---
layout: post
title: "It appears like you are building a framework"
description: ""
category: 
tags: [Mobile,Coding]
---
{% include JB/setup %}

<img src="/img/clippy.png" style="float:left; border: 1px solid #000; margin: 0 10px 10px 0">

There seems to be an ongoing theme in programming that instead of trying to understand and work within
someone else's framework, most programmers would rather write their own.  Re-inventing the wheel is almost
as foolish as choosing the wrong framework (and believe me I have done that enough times to be far too
cautious about devoting too much time learning a framework or language -- heck I spent a bunch of time
learning [Pike](http://pike.lysator.liu.se/) rather than [Ruby](https://www.ruby-lang.org/en/) in the
90's.   Heck after doing an inordinate amount of research during one of my internships I convinced an
employer that [Borland's Intrabuilder](http://www.drdobbs.com/borlands-intrabuilder-10/184415559) was
definitely the Web Application Server of the future, and its genius was that it used Javascript on
both the client and the server (unfortunately Javascript on the server was about 13 years too early).   But
generally it is almost always better to stand on the shoulders (and blood sweat and tears) of giants rather
than having the audacity to think that you can create something better.

I've walked down this road before creating my own [PHP framework](https://github.com/kriserickson/KrisMVC), which
is at best a little misguided.  Mostly I will argue that copying the ActiveRecord pattern was my undoing, as whenever
I have to use my framework (my wife's site for [Dance Company Ammara](http://ammara.ca) still uses it) it is the
database access that truly makes me shudder, but in my defence the golden age of PHP frameworks had yet to begin
when I wrote it (Symfony2, Laravel, Phalcon where not out yet) and the choices for a frameworks all seemed lacking.
 Though I liked Symofony at the time, I felt that it was over-engineered for a PHP framework (it tried to be far too much
 like Java frameworks like Struts) and running it on a shared hosting site without APC it was really slow.  So obviously
 I could write a better framework -- ah the hubris of youth.

So when I looked at the state of Mobile frameworks I really tried to not write a new framework.  For my work we needed
to quickly create a mobile application, and I spent a bunch of time researching the state of Mobile frameworks.  I have made
some apps 3 years ago with [jQtouch or jQT as they are now calling it](http://jqtjs.com/), however its Android
experience was always lacking and with IOS7 it looks horribly dated.
Recently I made my own [Recipe Folder](https://play.google.com/store/apps/details?id=com.recipefolder.app)





<div style="clear:both"/>
---
layout: post
title: "It appears like you are building a framework"
description: ""
category: TopcoatTouch
tags: [Mobile,Programming]
featured: true
---


<img src="/img/framework/clippy.png" style="float:left; border: 1px solid #000; margin: 0 10px 10px 0">

*TLDR - After weighing all the options I built a mobile framework around [Topcoat](http://topcoat.io), you
 can find it on [Github](https://github.com/kriserickson/topcoat-touch). *

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
 Though I liked Symfony at the time, I felt that it was over-engineered for a PHP framework (it tried to be far too much
 like Java frameworks like Struts) and running it on a shared hosting site without APC it was really slow.  So obviously
 I could write a better framework -- ah the hubris of youth.

So when I looked at the state of Mobile frameworks I really tried to not write a new framework.  For my work we needed
to quickly create a mobile application, and I spent a bunch of time researching the state of Mobile frameworks.  I made
some apps 3 years ago with [jQtouch or jQT as they are now calling it](http://jqtjs.com/), and started working with it
but quickly found it lacking.  So I did a kind of mobile rundown of the big frameworks:

Over the past year I have been working on my own mobile hobby App [Recipe Folder](https://play.google.com/store/apps/details?id=com.recipefolder.app),
a kind of [Pocket](http://getpocket.com)/[Instapaper](http://www.instapaper.com/)/ Readability (now defunct) for
Recipes (using a [Chrome Extension](https://chrome.google.com/webstore/detail/recipe-folder/nfgkogochmmkkglclaokmangionbpmha) or
[Bookmarklet](http://recipe-folder.com) you can save any Recipes you find on the web and then access them
later on your Mobile device).  It was written using jQuery Mobile, and that is a mistake I would never make again. 

I also looked at some of the commercial options (specifically [PhoneJS](http://phonejs.devexpress.com/) and [KendoUI Mobile](http://www.kendoui.com/mobile.aspx),
but once again the size of the framework scared me off.  Its not **just** that adding 1/2 a Meg of minified Javascript
on a mobile device seems like a bad idea, it is the problem of edge cases that you always run into when working with a framework when you
discover that the framework doesn't do quite what you expect and you need to change it.  Frequently when things aren't working
the way you would expect I like walking through the source to see what is going on, and with huge code bases that sometimes
just isn't possible.

I also looked at [Sencha](http://www.sencha.com/products/touch) and would seriously consider it for a large project I was writing by myself, however the complexity
of learning the platform and the time to build apps in it makes it a bit of a non-starter.  It would take anyone who had
 to work on the project a few weeks to get up to speed with the framework, and thereby diminishes the advantages of
 rapidly developing an app in HTML5 Javascript.  Let me be very clear, the Topcoat Touch framework is designed for small apps,
 that are only couple of pages and do not have a lot of data binding.  If you are building a giant mobile application seriously
 look into Sencha or using a framework like Angular (see [Topcoat with Angular](http://coenraets.org/blog/2013/11/sample-mobile-application-with-angularjs)
 for a good example of how to mix Angular with Topcoat).

My decision after watching a couple of excellent (and highly recommended) Phonegap presentations by
[Christopher Coenraets](http://coenraets.org/blog/2013/05/top-10-performance-techniques-for-phonegap-applications) and
[Tommy Williams](http://phonegap.com/blog/2013/09/30/spideroak) was to go without a framework at all.
However, after examining the source code for Christopher's [Backbone/RequireJS example](http://coenraets.org/blog/2013/06/building-modular-web-applications-with-backbone-js-and-requirejs-sample-app)
 and starting to write code without a framework I realized that there was a bunch of repetative programming chores that
 I could encapsulate into a framework.  There were also a few things that I really liked about the old jQTouch
 and that I could probably very quickly write a [micro-framework](http://microjs.com) that could acheive almost all of them.
 I could throw in [iScroll](http://cubiq.org/fyi-iscroll-is-out-of-beta) (I needed scrolling) and [Fastclick](https://github.com/ftlabs/fastclick)
  as optional micro-libraries and Bob's your uncle I would have  exactly what I wanted.  A tiny framework that could be easily extended, easily altered and was
 [very fast to learn](https://github.com/kriserickson/topcoat-touch/wiki/Getting-Started).
 And Voila! we now have [Topcoat Touch](https://github.com/kriserickson/topcoat-touch).

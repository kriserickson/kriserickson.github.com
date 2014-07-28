---
layout: post
title: "Mobile Frameworks -- KendoUI"
description: ""
category: Programming
tags: [Mobile,Phonegap,HTML5,KendoUI]
---
{% include JB/setup %}

This is Part 5 in multipart series on the State of Mobile Frameworks in 2014, see

* [Part 1 - The State of HTML Mobile Frameworks in 2014](/programming/2014/04/22/the-state-of-html-mobile-frameworks-in-2014/)
* [Part 2 - Mobile Frameworks -- JQT (Formerly jqTouch)](http://www.agingcoder.com/programming/2014/04/24/mobile-frameworks-jqt/)
* [Part 3 - Mobile Frameworks -- jQuery Mobile](http://www.agingcoder.com/programming/2014/04/26/mobile-frameworks-jquery-mobile/)
* [Part 4 - Mobile Frameworks -- Bootstrap](http://www.agingcoder.com/programming/2014/05/08/mobile-frameworks-bootstrap/)

if you haven't already.

KendoUI is one the most popular mobile frameworks around, and for good reason. Until a few months ago it had a commercial
only license which limited its attractiveness to non-enterprise developers, but its new Apache license makes it very
attractive especially if you are looking for a framework that heavily leverages jQuery.  In my opinion it is a lot 
more polished (and more specifically targeted) than jQuery Mobile.  It also has the advantage of a large company
with a long history of component development behind it, and if you want or need to get support you can get support
in a number of ways ranging from free forums to paid support if you purchase the KendoUI Professional edition.  KendoUI
can be seen as analogous to jQuery-UI and KendoUI Mobile parallels jQuery mobile.
They also provide as a SAAS[^SAAS] product something they call (AppBuilder)[http://www.telerik.com/appbuilder] (which is a terrible name since so many companies have
used it before, but I guess their previous name Icenium didn't express what the product actually did).  Appbuilder
started as fairly equal competitor to Adobe's (Phonegap Build)[https://build.phonegap.com/] allowing you to compile
your Cordova/PhoneGap applications in the cloud without having to deal with the hassles of setting up a build
environment for all of your applications.  It has become a fair bit more than that, recently, and now provides
an entire CloudIDE, Mobile Testing, Analytics, Debugging and Cloud Backend center in one package (of course
the more features you add like Analytics and Cloud Backend the more it costs).  

**How it Works**

KendoUI Mobile (from herein just called Kendo) is closest in spirit to jQuery Mobile, you create bunch of 
HTML that is divided into pages (given a data-role attribute of 'view' in KendoUI parlance).  
You add some Kendo css files and the Kendo js script (as well as jQuery) to the
head of the document.  In your own js file you create a kendo.mobile application (which initializes all of the 
magic).  It has 18 distinct controls, which range from visual elements like buttons to the more generic application (which
is used mostly for configuration of the look and feel of the application).  You then react to events with standard
jQuery events or you can wire up events directly in the html (using data-attributes).  Kendo supports data binding 
out of the box, or you can use Knockout.js or Angular if you want.  The level of flexibility given is quite large,
and they do have very good documentation.  There is even a (book)[http://www.packtpub.com/building-mobile-applications-with-kendoui-html5/book]
though it is probably a bit out of date by now.

One of the features of Kendo is that it tries to mirror the platform it is running on, so on IOS it looks sort
of like IOS, on Android it sort of looks like Android (dated, pre Holo Android), and on Windows Phone it sort of
looks like Windows Phone 8.  Unfortunately like most attempts to mirror native controls in HTML, you really end
up with the [uncanny valley effect](http://en.wikipedia.org/wiki/Uncanny_valley) where it almost looks native but
not really.  They also offer what they call a Flat UI, which is what I would probably ship across devices if I 
were to use Kendo.  

**Advantages**

There is a lot to like in Kendo, it is well maintained (well, maybe except for the fact they haven't brought their
Android skin up to Holo which came out over 3 years ago) and is much more polished in every way than jQuery Mobile.
The apps and controls seem snappy on modern devices, and the software seems very well designed.
While I am not a fan of the attempt to ape the platform that an HTML or Hybrid application is running on, if you 
are the type of person who does want that effect there are no other platforms that I know that does this that well.
The documentation is excellent and since the number of people who are using KendoUI is second only to jQuery mobile
the amount of support you can get on sites like StackOverflow is great.  The flexibility in choosing model binding
and external libraries (they recently have started moving most of their demos to Angular so you might see that as
the future of Kendo) will give you a large amount of flexibility in architect your application.  

**Disadvantages**


**Summary**

Next up, Ionic...


[^SAAS] [Software as a service](http://en.wikipedia.org/wiki/Software_as_a_service).
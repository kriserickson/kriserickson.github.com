---
layout: post
title: "Mobile Frameworks -- KendoUI"
description: "KendoUI is one the most popular mobile frameworks around, and for good reason. Until a few months ago it had a commercial only license which limited its attractiveness to non-enterprise developers, but its new Apache license makes it very attractive especially if you are looking for a framework that heavily leverages jQuery."
category: Programming
tags: [Mobile,Programming,Cordova,Phonegap,HTML5,KendoUI]
---


This is Part 5 in multipart series on the State of Mobile Frameworks in 2014, if you haven't already read the previous articles, they are here:

* [Part 1 - The State of HTML Mobile Frameworks in 2014](/programming/2014/04/22/the-state-of-html-mobile-frameworks-in-2014/)
* [Part 2 - Mobile Frameworks -- JQT (Formerly jqTouch)](/programming/2014/04/24/mobile-frameworks-jqt/)
* [Part 3 - Mobile Frameworks -- jQuery Mobile](/programming/2014/04/26/mobile-frameworks-jquery-mobile/)
* [Part 4 - Mobile Frameworks -- Bootstrap](/programming/2014/05/08/mobile-frameworks-bootstrap/)

***Note***

This article took way longer to get out than I had planned.  First I spent a while digging into AppBuilder, and by the
time I started writing the review a fair bit had changed since I last evaluated KendoUI so I wanted to at least build
a small application in it again.  I am not as familiar with Kendo as I am with any of previous frameworks having not
built a real application in it and only built a demo app (I wrote a two page note taking app) in it.  Please bear this
in mind when reading this review.

*KendoUI Mobile*

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
The documentation is excellent and since the number of people who are using Kendo is second only to jQuery mobile
the amount of support you can get on sites like StackOverflow is great.  The flexibility in choosing model binding
and external libraries (they recently have started moving most of their demos to Angular so you might see that as
the future of Kendo) will give you a large amount of flexibility in architect your application.  

**Disadvantages**

Kendo is huge, 4 Megs of Javascript source code (and the division between Mobile and KendoUI is not as clear as it is in
say jQuery Mobile) and almost 3 Megs of Css.  When you produce a keno application, you only include a small portion of
that but getting your head around 4 megs of code is large task.  While you can get up and running with Kendo in a few
hours I never got to the point where I felt truly comfortable with the large codebase. I will use either two types
of libraries in a project:
 
1. Ones that are small enough and well documented that I have no problem rolling up my sleeves and fixing or customizing them if needs be.
2. Or libraries that I feel are so robust and well tested that I can use them like built in language features (a library like jQuery for example, 
when it starts acting weird I know it is almost always something I have done and spelunking into the jQuery codebase usually leads 
to more frustration than edification so I treat it closer to plumbing than a library).  

It should also be noted that while the Kendo code is not complicated, and fairly easy
to read it contains no comments (this may be available in the Professional version, I am not sure) so you are kind
of on your own when you go looking at the code.  Customizing the CSS is done through their 
[ThemeBuilder](http://demos.telerik.com/kendo-ui/mobilethemebuilder/) which gives a little bit of 
flexibility in changing the colors but like jQuery mobile the CSS is so complicated (and in that I mean there are a huge
number of classes and changing something that you think may only effect one or two elements actually may effect a lot
more that you will not realize until much later) that if you do manage to change
some more major features of the look and feel you will not be able to update when their CSS changes.  

**Summary**

I think that Kendo is a great choice for projects where you like the Kendo look and feel, and you don't want to customize
the look and feel much more than the colors of the application.  You will get off the ground relatively quickly and will 
have a rock solid base fore creating a line of business application.  If you are the type of person that likes getting 
under the hood and tinkering with the look and feel of your page, adjusting CSS and sometimes feel that you need to 
extend a framework for it to do those little things that don't quite exactly work the way you want them to out of 
the box, I would look to one of the smaller frameworks.

You can download the free Kendo UI Core [here](http://www.telerik.com/download/kendo-ui-core), or you can build it
yourself from the [Github Repository](https://github.com/telerik/kendo-ui-core).  The extensive documentation can
be is [here](http://docs.telerik.com/kendo-ui/).



Next up, [Ionic](/programming/2014/10/11/mobile-frameworks-ionic/)...


[^SAAS] [Software as a service](http://en.wikipedia.org/wiki/Software_as_a_service).
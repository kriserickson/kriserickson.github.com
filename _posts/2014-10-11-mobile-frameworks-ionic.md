---
layout: post
title: "Mobile Frameworks - Ionic"
description: "Ionic is the new hotness in the hybrid app development world, picking up steam and popularity at I high rate.  It uses Angular to allow for declarative, interactive pages and  their own CSS UI to create a modern looking UI.  To this, Ionic adds its own special sauce: a collection of Angular directives, a CLI tool, some libraries and proscriptive structure for creating a mobile application."
category: Programming
tags: [Mobile,Cordova,Programming,Phonegap,HTML5,Ionic]
---


This is Part 6 in multipart series on the State of Mobile Frameworks in 2014, see

* [Part 1 - The State of HTML Mobile Frameworks in 2014](/programming/2014/04/22/the-state-of-html-mobile-frameworks-in-2014/)
* [Part 2 - Mobile Frameworks -- JQT (Formerly jqTouch)](/programming/2014/04/24/mobile-frameworks-jqt/)
* [Part 3 - Mobile Frameworks -- jQuery Mobile](/programming/2014/04/26/mobile-frameworks-jquery-mobile/)
* [Part 4 - Mobile Frameworks -- Bootstrap](/programming/2014/05/08/mobile-frameworks-bootstrap/)
* [Part 5 - Mobile Frameworks -- KendoUI](/programming/2014/07/28/mobile-frameworks-kendoui/)

**Edit**: I was mistakenly under the impression from an episode of [JSJabber](http://javascriptjabber.com/126-jsj-the-ionic-framework-with-max-lynch-and-tyler-renelle/)
 that Ionic had used [TopCoat](http://topcoat.io) as  their UI basis for their CSS, however mistook [@Tyler Renelle](https://twitter.com/lefnire) 
 (creator of [HabitRPG](https://habitrpg.com)) for [@Max Lynch](https://twitter.com/maxlynch) (co-creator of the Ionic framework)
 so when Tyler said that they came from Topcoat I was assuming that Ionic came from Topcoat.  A mistake which could have been
 cleared up by my looking at the CSS a little more closely when I was writing the Q&D app that wrote.  I guess this kind of speaks
 to the strengths of Ionic that until you want to customize the look and feel of the App (which was not a point that I have reached
 in the toy app that made) you don't really have to look at the CSS that much.  Anyhow, to be clear, Ionic uses their own CSS 
 which they have created and does not use Topcoat.  I have edited the article to clarify that, and thanks to [@IonicFramework](https://twitter.com/Ionicframework)
 for quickly pointing that out and not making me look like a fool for too long.

Ionic is the new hotness in the hybrid app development world, picking up steam and popularity at I high rate.  It uses
[Angular](https://angularjs.org/) to allow for declarative, interactive pages and <s>[TopCoat](http://topcoat.io)</s> their 
 own CSS UI to create a modern looking UI.  To this, Ionic adds its own special sauce: a collection of Angular directives, a CLI
tool, some libraries and proscriptive structure for creating a mobile application.

I am a huge fan of Angular and had messed around with a bit on mobile in the past with [TopCoat](http://topcoat.io/).  It 
wasn't using a framework other than Angular and I found that it worked pretty well.  
Especially on newer devices, however it seemed at the time to have some issues Android 2.3 devices
(Android 2.3 is becoming the new [IE 6](https://www.modern.ie/en-us/ie6countdown) of the browser world).  
It also seemed pretty heavy to add Angular the the little App I was making at the time.  
Eventually I abandoned the experiment and ended up creating my own little framework with
[TopcoatTouch](http://topcoattouch.com), but had Ionic been there (and at the state it is now) I probably wouldn't
have bothered and used Ionic.  That said, Angular has certain learning curve and it takes most developers a while to 
 "get it", and there can be a level of frustration when things like a binding just stop working (usually involving
 scope).

**How it Works**

Ionic provides you with a CLI tool that can easily create a skeleton application (and while it seems to be a little
bit of wheel re-invention here rather than using [Yeoman](http://yeoman.io/), however it leads to a much cleaner
directory and now that [Bower](http://bower.io) is falling out of style, it makes some sense).  The Ionic CLI
also assumes that you are creating a Cordova app, which is a nice.  It wraps the Cordova CLI so you only need
one CLI tool, which seems to mostly be so that Ionic can sell their upcoming build service (like Phonegap Build) at some point,
which I have no problem with, the more competition in the Cordova Build Services the better they will all be forced
to become better. When creating a project with the ionic CLI, there are also 3 plugins added (Device, Console and the Ionic Keyboard plugin which
provides some useful functionality but should be noted that it currently only supports IOS and Android).    

Once you have created your app with either the CLI or downloading the libraries from their [website](http://ionicframework.com/)
(or [github](https://github.com/driftyco/ionic)) and creating your own skeleton app.  You end up with (or should end up with)
a very minimal index.html with mostly javascript and css files included (you can include your first page, or that can
be in the templates.  There is also a css directory (which you can set up to use [Sass](http://sass-lang.com/)), a
javascript directory and a template directory.  If you've used angular before you will be very comfortable here, if you
haven't there will be a pretty steep learning curve to figure out exactly what is going on.  Although you might be able
to use Ionic as a stepping stone into the world of [Angular](https://angularjs.org/) I think that it is probably
better to learn Angular first (through something like [CodeSchool](https://www.codeschool.com/courses/shaping-up-with-angular-js) or
[Egghead](http://egghead.io)).  

Ionic provides some very good directives, some obvious directives, and maybe some questionable directives.  They also
provide <s>(through [TopCoat](http://topcoat.io))</s> a great and modern looking UI with CSS applied through said
directives as well as through adding classes to elements.  The CLI tool is nice, but mostly just a way of setting up a simple skeleton app and 
wrapping the Cordova CLI.  It looks like they are also creating a nice [GUI builder](http://ionicframework.com/creator/), 
but I haven't had a chance to play with it yet.

**Advantages**

Angular, angular, angular.  Angular (or something similar to Angular) is the future of SPA (and mobile) apps.  As 
mobile devices get more and more powerful, Angular starts becoming something of a no brainer, it just makes development
so fast compared to most other methods.  It is also highly testable, reliable, and has the backing of Google and many
other huge companies behind it.  The Ionic CLI makes it easy to start making and application, and that is nothing to 
sneeze at.  It is built to work with hybrid applications and Cordova from the ground up.  It's documentation is 
excellent, and due to its popularity (when I [first looked at the Ionic framework])/programming/2014/04/22/the-state-of-html-mobile-frameworks-in-2014/)
in April it had 82 questions on [Stackoverflow](http://stackoverflow.com/search?q=ionic), it now has over 1,400) it
has a lot of resources for getting answers.  And to top it off, it is well designed and well written.  
 

**Disadvantages**

Angular does have a learning curve, and if you don't already know it, learning Angular and Ionic is a fair amount
of work.  If you just want to pound out a couple page simple application it may be overkill to add this level of 
complexity to your app.  Also on older devices (if you care about supporting devices from 3 or 4 years ago) Angular
and Ionic run a little slower than a raw Javascript, HTML and CSS app.

**Summary**

As we have watched the rest of the mobile Javascript world has been moving towards Ionic, it is pretty obvious why.  Ionic
would be my framework of choice so far for any large mobile applications that I was green fielding.  Angular allows 
us to reign in complexity and yet quickly create complicated immersive applications.  Ionic does an excellent
job of leveraging and improving upon Angular in mobile.  

Next up, we see if [Onsen-UI](/programming/2014/10/16/mobile-frameworks-onsenui/) (another Angular/TopCoat based framework) adds anything to Ionic or falls short in any areas...


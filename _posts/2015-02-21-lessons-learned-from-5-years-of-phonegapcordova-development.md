---
layout: post
title: "Lessons Learned from 5 Years of PhoneGap/Cordova Development"
description: "It seems hard to believe, but it's been almost 5 years since I started doing PhoneGap development!  while I could write a history of PhoneGap, or a history of my own use of PhoneGap, I felt it would be more interesting to share some of the wisdom I have learned from the past few years..."
category: Programming
tags: [Mobile,Programming,PhoneGap,Cordova]
featured: true
---

<div style="font-size: 16px; margin: 0 0 10px 0; background: #f5f5f5; border: 1px solid #ddd; padding: 15px; margin: 0 auto 2em auto; max-width: 56.25rem; line-height: 1.5em"><strong>Update:</strong> This post is getting pretty long in the tooth, so I have updated it: <a href="/programming/2018/07/11/three-more-years-of-phonegapcordova-lessons/">Three More Years of Phonegap / Cordova Lessons</a></div>

It seems hard to believe, but it's been almost 5 years since I started doing PhoneGap development!  while
I could write a history of PhoneGap, or a history of my own use of PhoneGap, I felt it would be more interesting
to share some of the wisdom I have learned from the past few years (which mostly supersedes everything in learned
in the first few years of PhoneGap development).  I have the scars (both mental and physical from basing my head
on the keyboard) from those years but hopefully the experience and tips I share here can help someone out so they
don't have to experience the same scarification.  

If you want to look at my handiwork, my [Recipe Folder](https://recipe-folder.com) App is available in both the [iOS App Store](https://itunes.apple.com/ca/app/recipe-folder/id796838333?mt=8)
 and the [Google Play Store](https://play.google.com/store/apps/details?id=com.recipefolder.app), and was built with
 my [Topcoat Touch](http://topcoattouch.com) framework.

Just a few quick notes before starting, I do all my building of my PhoneGap/Cordova apps on my own machines and
have no experience with the various Build Services.  If you have problems getting the Android SDK installed or
don't have access to an OSX box you really should look into the various Build Services. 
[Adobe PhoneGap Build](https://build.phonegap.com/), [Telerik](http://www.telerik.com/appbuilder), and
[Appgyver](http://www.appgyver.com/) are the ones that have heard the most positive things about, but like I
said I have never used any of them so YMMV.  If you do use a build service some of these tips will apply to you,
but some you will no longer have to worry about.

So here, in no particular order, are my PhoneGap Lessons:

1. **Node is your best friend**: Sure you pretty much have to install node to get Cordova running these days (I
guess there may be hacks to get around this, or you could use an ancient version) but embrace node.  Use [grunt](http://gruntjs.com/) or
[gulp](http://gulpjs.com/) as your build system (I actually recommend having a subdirectory off your project to
place your cordova output and have a build task copy the required files there - this will make it possible to
concat and minify your JS and CSS files).  Use node [http-server](https://www.npmjs.com/package/http-server) or
 a [grunt](https://www.npmjs.com/package/grunt-serve) or [gulp](https://www.npmjs.com/package/gulp-serve) task
 to serve your project while developing it (more on that later).  Find all of the amazing things that node 
 do for you like [javascript](https://github.com/mishoo/UglifyJS2) and [css](https://github.com/gruntjs/grunt-contrib-cssmin)
 minimization, [image optimization](https://www.npmjs.com/package/imageoptim), and [testing](https://github.com/mhevery/jasmine-node).
   
2. **Node is your worst enemy**: Especially if you are on windows, node (well mostly npm) can be a real pain in the butt.  Getting
some of the NPM modules which require c compilation to work on windows is a combination of super google foo, wizardry,
and a hell of a lot luck (though it has gotten easier with release of the 
[Community Edition of Visual Studio](http://www.visualstudio.com/en-us/news/vs2013-community-vs.aspx)).  Also the current
switch from node v0.010 to [v0.12](http://strongloop.com/strongblog/node-js-v0-12-apis-breaking/) and the release of 
[io.js](https://iojs.org/en/index.html) has caused a bunch of NPM issues.

3. **Test on real devices but develop in Chrome**: If you aren't familiar with the emulation portion of the Chrome
Dev Tools and you do any mobile work, [learn about it now](https://developer.chrome.com/devtools/docs/device-mode)!  The 
Chrome Dev Tools are the only reason I still use Chrome, as it has become kind of a bloated buggy nightmare in the past
 year, but the Dev Tools are still amazing!  Learn how to use [workspaces](https://developer.chrome.com/devtools/docs/workspaces)
(even though I live in the [Jetbrains](https://www.jetbrains.com/webstorm/) world, I find I do most of my CSS editing 
and a ton of Javascript editing in the Chrome Dev Tools).  Getting good with the Chrome Dev Tools will save your proverbial
bacon, but also start testing on devices early.  You may discover that even though Chrome does its best to "Emulate" the various
devices, Chrome on the desktop and the various browsers on mobile radically differ.  You must especially test on the webkit browsers 
(Android before 4.4 - KitKat, and Safari on iOS) as are very different beasts.  [CanIUse](http://caniuse.com/) is fantastic, especially
if you go to the settings and set the various [browsers](http://caniuse.com/#compare) you want to use (by default it only shows Android 4.1 and up).  
Try to get as many real devices as you can and keep them at different versions of Android (obviously
depending on which version of Android you want to support).  The emulators are OK, but nothing matches a real device (and you can
pick up [Unlocked Android Phones](http://www.amazon.com/s/?url=field-keywords=android+unlocked) for under $50 these days). 

4. **Genymotion for Android Development is awesome**: Even though Intel HAXM hardware accelerated Android emulators are a huge improvement (and you
absolutely should [install HAXM](https://software.intel.com/en-us/android/articles/installation-instructions-for-intel-hardware-accelerated-execution-manager-windows)
for the Android SDK) [Genymotion](https://www.genymotion.com/) is a faster emulator especially at getting the binary installed on the device.  Although
they have a limited number of versions of Android they emulate (no 4.0 Ice Cream Sandwich, for example) they are another arrow in your quiver for
mobile Android testing.

5. **Multiple OSX Machines**: If you can stockpile a couple of OSX machines you will be doing yourself a favour.  There is no way
to emulate iOS6 or less on xCode 6, and you can't install xCode5 on Yosemite, so you should probably have a Yosemite box and
a Mavericks box if you can.  If you can't have two machines, don't upgrade to Yosemite (you may not want to anyway for all of the
issues that Yosemite has anyway).  I still always run on Windows and just VNC into the OSX boxes, but I am still looking for the best
iOS developing solution on Windows (any tips in the comments would be welcome).  If you are like me and want to Debug iOS on Windows, [GapDebug](https://www.genuitec.com/products/gapdebug/) offers an awesome, free iOS and
Android on Windows development solution that promises in the future to even bring the Chrome Dev Tools to iOS device debugging (they
claim to support it currently experimentally but I have yet to have that work in any way).  
 
6. **Remote Device Debugging**: Another awesome feature of the Chrome Dev Tools is the [Remove Device Debugging](https://developer.chrome.com/devtools/docs/remote-debugging),
 which obviously is a huge improvement of the alert debugging in the past, but you should also learn how to get 
 [Weinre](http://people.apache.org/~pmuellr/weinre-docs/latest/) running.  If you aren't comfortable at using it locally, which 
  is very simple these days:  `npm install weinre` then you can use the free [PhoneGap build Weinre](http://debug.build.phonegap.com/), 
  but be aware that debugging will be much slower than running Weinre locally. 
  
7. **Avoid loading the Platform project in an IDE**:  Unfortunately, I break this rule all the time and because of that I need to strictly follow
the [next suggestion](#blowAway).  IDE Project files (whether it be Eclipse, Intellij IDEA or Android Studio, and xCode) are very complicated beasts
and brittle to external editing, and if you change things in the IDE there is a good chance that the Cordova command line will not be
able to prepare, upgrade, or build any more.  Or that when do a command from the Cordova command line the project will not build
properly and you will get some cryptic error that you will spend 2 hours Googling to figure out what actually happened and how to fix it (if you even can).  
If you are very comfortable in the various IDE's and know their project structures and file formats then feel free break this rule, 
but if you do be prepared to follow the next rule. 

8. <a name="blowAway"></a>**Always be prepared to blow away a platform** The number of times the only way I could get a project to build was 
to `cordova platform remove ios
cordova platform add ios` (not picking on iOS, it happens with Android all the time too) is way too many to count.  
If you spend hours customizing your icons, splash screens, and the various settings inside the IDE you are going to be 
very unhappy when you have to lose all that work and recreate the platform.  For
that reason try to make any native changes you need to a platform part of a [plugin](http://cordova.apache.org/docs/en/edge/guide_hybrid_plugins_index.md.html)
and have scripts and a process to put your Art Assets into place.  

9. **Use as Few Plugins As Possible**: Plugins are one of the best features of PhoneGap, but there use adds to the fragility of your build.
If you can get away without using a plugin (especially a third party plugin), you will probably save yourself a bunch of hassle.  This will
also make it easier to use a build service, if you go down that path.  Also keeping plugins up to date is another serious pain that hopefully
will be fixed soon in cordova (BTW, I only recently discovered that you don't need to remove a plugin to update it, you can just do 
`cordova plugin add org.apache.cordova.device` and you will get the latest version of the device plugin).
    
10. **Don't write your own Framework**: I would have given different advice on this a year and half ago, but really the quality of 
mobile frameworks have improved so much in the past year that I would never write a framework-less app again 
(though having built one [framework](http://topcoattouch.com) I would probably use that again).  I would probably
recommend Ionic if you are targeting high end phones, or something less heavy if you are not.  For a full rundown on the
various mobile frameworks, especially targeting Cordova checkout my previous article on 
[The State of Mobile Frameworks](http://www.agingcoder.com/programming/2014/04/22/the-state-of-html-mobile-frameworks-in-2014/).

Hopefully some of these tips and rules you will find helpful in developing your own Cordova Apps.  If you have any tips to share,
  please do so in the comments, and as always feel free to ask questions (which I will try to answer).
  
  

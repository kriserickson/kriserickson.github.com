---
layout: post
title: "Mobile Frameworks - OnsenUI"
description: ""
category: Programming
tags: [Mobile,Phonegap,HTML5,KendoUI]
---
{% include JB/setup %}

This is Part 7 in multipart series on the State of Mobile Frameworks in 2014, see

* [Part 1 - The State of HTML Mobile Frameworks in 2014](/programming/2014/04/22/the-state-of-html-mobile-frameworks-in-2014/)
* [Part 2 - Mobile Frameworks -- JQT (Formerly jqTouch)](/programming/2014/04/24/mobile-frameworks-jqt/)
* [Part 3 - Mobile Frameworks -- jQuery Mobile](/programming/2014/04/26/mobile-frameworks-jquery-mobile/)
* [Part 4 - Mobile Frameworks -- Bootstrap](/programming/2014/05/08/mobile-frameworks-bootstrap/)
* [Part 5 - Mobile Frameworks -- KendoUI](/programming/2014/07/28/mobile-frameworks-kendoui/)
* [Part 6 - Mobile Frameworks -- Ionic](/programming/2014/10/11/mobile-frameworks-ionic/)

[Onsen](http://onsen.io/) is another [Angular](https://angularjs.org) based mobile UI framework, and this one actually (I checked, honestly)
does have its CSS framework based on [TopCoat](http://topcoat.io), although they have modified it a fair bit.  It hails from Japan 
(Onsen means Hotsprings or Spa in Japanese, so the name is cute pun) which may explain why it lacks the exposure of [Ionic](http://ionicframework.com/).
There are some differences in philosophy and execution of Onsen, and depending on how you feel about convention over configuration
and how proscriptive you want your UI Onsen may appeal to you.  Also (though not required for Onsen) its creators also provide
an online IDE and development environment called [Monaca](http://monaca.mobi/en/) that lets you quickly bring live debugging to your device through their debugging app.  And
offers another PhoneGap/Cordova build platform (similar to [AppBuilder from Telerik](http://www.telerik.com/appbuilder1), but a little
more immediate).

**How it Works**

Onsen is lacking a command line GUI tool (though if you use their Monaca IDE you can create a new Onsen app picking from
a collection of templates), though there is a [Yeoman Generator for Onsen](https://github.com/arvindr21/generator-onsenui-phonegap).
However their recommended way of starting a new App is download one of their zipped "starter kits" from their [getting started page](http://onsen.io/guide/getting_started.html).
They have a Master Detail (which uses an Angular Controller, so it would be the one I would recommend downloading if you want to build
and Angular style app), a "Sliding Menu", a "Tab Bar", and a "Split View" (which are not controller based).  That is one
of the main differences between OnSen and Ionic, is that even though Onsen is using Angular under the covers you don't
have to create an Angular App if you don't want to, it is very happy to let you use jQuery or whatever JS framework you want to.  You
do have to "compile" objects that are custom (onsen) elements.  From their guide:

```ons.bootstrap();
ons.ready(function() {
    // Add another Onsen UI element
    var content = document.getElementById("my-content");
    content.innerHTML="<ons-button>Another Button</ons-button>";
    ons.compile(content);
});```
     
or with jQuery
     
```ons.bootstrap();
ons.ready(function() {
    // Add another Onsen UI element
    ons.compile($("#my-content").html("<ons-button>Another Button</ons-button>"));    
});```     

Although that might be annoying, it is nice that if you weren't comfortable with Angular you could actually use Onsen pretty
productively.

Of course you can do everything in Angular that you expect, however Onsen is a little different from Ionic in that
it isn't using Routing to change pages but has a navigator object (which can be forced into the global scope) or can
be accessed through $scope.ons.navigator in Angular app.  My guess is that they opted for having a page navigator so
that you didn't have to do angular page routing, and simplify things but it does feel like a very unangular way
of doing things.  In fact, my main problem with Onsen is that (at least from the demos and the documentation) they
are not embracing the Angular way of doing things and their sample code is not as clean as I would desire.  

The Monaca IDE on the other hand, seems to be a very polished piece of work.  It's not perfect and it has a few rough
edges with the UI (some of the dialogs are clipped in weird places, some of the icons are little rough) but 
after spending a fair bit of time in the IDE, it is surprisingly the best of the online mobile IDE's I have tried.
The IDE is responsive, and although not as full featured as [Jetbrains IDE](https://www.jetbrains.com/webstorm/) or even 
[Vim](http://www.vim.org) but it is good enough to not hate it.  You can quickly upload files as well, and if you have
a WebDev client you can edit directly on your computer.  You can then preview in a web browser or on their debugger app 
on an iPhone, Android, Windows 8 or Chrome.  You can also build an apk, ipa, or 
lets you quickly test out your app on a real device without having to build and deploy.

**Advantages**

**Disadvantages**

Allowing objects to be hoisted into global space by annotating the elements with var, not embracing routing, not using templates
out of the box.

**Summary**

Next up, Sencha-Touch...


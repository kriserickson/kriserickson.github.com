---
layout: post
title: "Mobile Frameworks - OnsenUI"
description: "Onsen is another Angular based mobile UI framework, and this one actually (I checked, honestly) does have its CSS framework based on TopCoat, although they have modified it a fair bit. It hails from Japan (Onsen means Hotsprings or Spa in Japanese, so the name is cute pun) which may explain why it lacks the exposure of Ionic. "
category: Programming
tags: [Mobile,Cordova,Phonegap,HTML5,Programming,Onsen]
---


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

{% highlight javascript %}
ons.bootstrap();
ons.ready(function() {
    // Add another Onsen UI element
    var content = document.getElementById("my-content");
    content.innerHTML="<ons-button>Another Button</ons-button>";
    ons.compile(content);
});
{% endhighlight %}
     
or with jQuery
     
{% highlight javascript %}
ons.bootstrap();
ons.ready(function() {
    // Add another Onsen UI element
    ons.compile($("#my-content").html("<ons-button>Another Button</ons-button>"));    
});
{% endhighlight %}

Although that might be annoying, it is nice that if you weren't comfortable with Angular you could actually use Onsen pretty
productively.

Of course you can do everything in Angular that you expect, however Onsen is a little different from Ionic in that
it isn't using Routing to change pages but has a navigator object (which can be forced into the global scope) or can
be accessed through $scope.ons.navigator in Angular app.  My guess is that they opted for having a page navigator so
that you didn't have to do angular page routing, and simplify things but it does feel like a very unangular way
of doing things.  In fact, my main problem with Onsen is that (at least from the demos and the documentation) they
are not embracing the Angular way of doing things and their sample code is not as clean as I would desire.  

The Monaca IDE on the other hand, seems to be a very thorough piece of work.  It's not perfect and it has a few rough
edges with the UI (some of the dialogs are clipped in weird places, the icons are not very uniform in style, and the mixture
of different libraries and frameworks -- [Ace](http://ace.c9.io/), [ExtJs](http://www.sencha.com/products/extjs/), [AngularBootstrap](http://angular-ui.github.io/bootstrap/)
leaves some rough edges), but after spending a fair bit of time in the IDE, it is surprisingly the best of the online mobile IDE's I have tried.
The IDE is responsive and although not as full featured as [Jetbrains IDE](https://www.jetbrains.com/webstorm/) or even 
[Vim](http://www.vim.org) but it is good enough to not hate it.  You can quickly upload files one directory at time, import and export as zip, 
and if you have a WebDev client you can edit directly on your computer.  You can then preview in a web browser or on their debugger app 
on an iPhone, Android, Windows 8 or Chrome (similarly to the [Phonegap Developer App](http://app.phonegap.com/).  
You can also build an apk, ipa, appx (windows 8 package) or Chrome Zip file (although I never actually got the Windows 8
package to build).  It is a fair bit simpler than AppBuilder but I didn't have nearly as many problems with it as I had
when trying to use the Telerik product.

Onsen also provides a nice Theme Editor (kind of similar to the old jQuery-UI Theme Roller) where you can start off with 
one of their predefined colour schemes and modify it to come up with your custom theme with just a few clicks.  You can
also do the same thing by editing a few [Stylus](http://learnboost.github.io/stylus/) files (their CSS is written
in Stylus) but having a nice GUI tool makes it easy for a designer who is not comfortable with Stylus or even CSS
to come up with a unique set of colours for your app.

**Advantages**

One of the big advantages of Onsen is that it uses Angular under the hood, but doesn't force you as a developer to
learn Angular.  They have gone to a bunch of effort to allow for non-angular developers to work comfortably with the
tools that they are familiar with (jQuery, etc) and still be able to create angular applications.  Using TopCoat for the
basis of their CSS and then layering theming on top through Stylus has allowed them to create an easily themable UI
that looks pretty good and is very flexible.  The Theme Editor is a nice touch, missing in most of the other mobile frameworks
I have worked with, and the Monaca IDE really surprised me (I have not been a fan of browser based IDE's in the past but
maybe I will revisit a few after my experience with Monaca).

**Disadvantages**

Onsen doesn't look quite as nice as Ionic, when running on a device the default look just feels a little off.  Perhaps that
is TopCoat showing it's age (it was created before IOS7 and Material design and though it looked fresh and Modern a year and
a half ago, it is started to look a tad dated) and maybe it is that Onsen needs to spend a tiny bit more time polishing the look.
The starter kits (with the exception of the Master-Detail) are kind of a mess, not only are they full of lipsum data, but
the entire app is encompased within the index.html (no seperate templates, no js file).  It is nice that Onsen can be written
without Angular but a good example of this should be shown.  Allowing objects to be hoisted into global space by annotating 
the elements with var attribute is I guess required to access objects like the page navigator but I feel that should be a
way to do this without polluting the global space.  Also their choice not using templates in any of the examples is another
example of how Onsen doesn't proscribe how to create apps, but also doesn't set up some important patterns which would help.
The documentation and guides are ok, but the lack of a really good full example is missing.  And that underlines one of
the other problems with Onsen (that hopefully will change) is that due to the fact it is relatively unknown (there isn't
even a [PropertyCross](http://propertycross.com/) example, and the number of questions on [StackOverflow](http://stackoverflow.com/questions/tagged/onsen-ui)
is pretty limited.  In fact one of the best references I have found is [Holly Schinsky's Onsen Sample](http://devgirl.org/2014/05/13/sample-phonegap-application-with-angularjsonsenui/), where she states in a Disclaimer that it is her
first time working with the framework.  So, there is kind of dearth of documentation, instructions, and help other than
the [documentation](http://onsen.io/guide/components.html) and [guides](http://onsen.io/guide/overview.html) on OnsenUI page.

**Summary**

THere are a lot things to like in OnsenUI, and it is nice to have multiple options for using Angular with mobile.  Onsen
does a lot of cool things, but there is room for improvement.  I would recommend improving the starter apps, as well as
creating a full featured sample app highlighting best practices in Onsen.  The Theme Roller tool is a great addition, its
nice to be able to empower a designer to be able adjust the colour palette without having to break into the CSS or Stylus.
OnsenUI is certainly worth looking at and checking out, as is their Online [IDE Monaca](http://monaca.mobi/en/).

Next up, Sencha-Touch...


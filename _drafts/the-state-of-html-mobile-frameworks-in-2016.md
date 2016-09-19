---
layout: post
title: "The State of HTML Mobile Frameworks in 2016"
description: "It's been over 2 years since I posted The State of Mobile Frameworks and a fair amount has changed in that time, so now is probably a good time to dive back into that thorny topic"
category: Programming
tags: [Mobile,Phonegap,HTML5,Cordova]
featured: true
---
#### The State of Mobile Frameworks

It's been over 2 years since I posted [The State of Mobile Frameworks](/programming/2014/04/22/the-state-of-html-mobile-frameworks-in-2014/) and a fair amount has changed in that time, so now is probably a good time to dive back into that thorny topic.  Some frameworks have withered and died, some have gained functionality and popularity, and some have effectively stayed still.   It is important to note, that mostly I am focused on Hybrid app frameworks, frameworks that are designed to run solely on mobile/tablet.  If the framework's main focus isn't building mobile first applications that can be run on PhoneGap then I am not covering it here, or am looking at it in a mobile first context.  This is clearly not the way to build a modern website, where a responsive solution is always best, but it is the way to build an app that can have more functionality than a website can by utilizing features on the device that isn't currently accessible to websites (either for security reasons or just because the feature hasn't rolled out to browsers yet).
 
 #### It's Dead Jim

Of the frameworks I looked at, 10 of the 12 have effectively disappeared.
 
* [jQT](http://jqtjs.com/) was dead in 2014, but was included since it was still appearing a lot in searches at the time.  Put the final nail in that coffin now. 
* [jQueryMobile's](http://jquerymobile.com/) last release was 2 and a half years ago, it was mostly dead then.  No one should consider using it now. 
* [Bootstrap](http://getbootstrap.com) threatened to be a valuable for mobile development, and maybe with [Bootstrap 4](http://v4-alpha.getbootstrap.com/), if it is ever released, it might be but for now it is still for use on websites only.  If you want to use Bootstrap, combine it with something like [Mobile Angular-UI](http://mobileangularui.com/), and then you have something approaching a modern solution, however I don't think it best of breed solution.
* [Sencha-Touch's](http://www.sencha.com/products/touch/) license, or its htmlless design model may have killed it, but although it still appears to exist as product it is not an option I would consider.  Also the source code doesn't appear to be a GitHub which is always a bad sign.
* [PhoneJS](http://phonejs.devexpress.com/) has been rebranded [DevExtreme Mobile](http://js.devexpress.com/MobileDevelopment/) seems to be at about the same point it was 2 years ago, also not on GitHub, also requires a commercial license.
 * [Jo](https://github.com/davebalmer/jo), the old site joapp.com is dead and there hasn't been a commit in 3 years.  Put a fork in it. 
 * [ChoclateChip-UI](https://github.com/rbiggs/chocolatechip-ui), the chocolatechip-ui.com website doesn't appear to reference the project any more, and there hasn't been a commit in a while on GitHub.  
 * [AppFramework](http://app-framework-software.intel.com/), points to the GitHub site, but I think Intel doesn't have the energy to focus on this type of project any more.
 * [TopcoatTouch](http://topcoattouch.com) was kind of dead when I wrote about this two and a half years and almost nothing has been done it since.  The TopCoat CSS framework has long since been abondoned by Adobe, so I can't recommend using it.
 * [KendoUI Mobile](http://www.telerik.com/kendo-ui) has kind of disappeared from the Kendo-UI framework in favour of responsive design (probably the right way to go).  That means, though, that the [Mobile Theme Builder](http://demos.telerik.com/kendo-ui/mobilethemebuilder) and cross platform look and feel is also effectively gone.  Kendo-UI might be good for developing responsive web sites now, but I don't think I would use it for building a Hybrid app. 
 
 I didn't mention [Famous](https://github.com/Famous/framework) in the previous article, but after a brief moment looking like they were going to be an interesting alternative to the Angular Based Mobile frameworks and a ton of VC investment, they [flamed out and had to pivot](https://techcrunch.com/2015/11/06/nopen-source/).
 
#### Is Less Diversity and Choice Maybe a Good Thing? 
 
 That leaves [Ionic](http://ionicframework.com/), and [Onsen-UI](https://onsen.io/).  There have been a few others (like (Rachet)[http://goratchet.com/] which is more of a prototyping framework), but the only real new framework I would consider would be [Framework 7](https://framework7.io/).  This dearth of choice almost brings us to back to 2013 when there were only a couple of options, before the explosion of frameworks of 2014.  And two of the three frameworks are Angular based, leaving even less choice.  It certainly means that you will have less frameworks that you will be required to evaluate before making a decision, but it also means that if you are unhappy about one of the big three's framework design choices or appearance you have less options for change.  
 
 There are certainly going to be new Frameworks in the future ([Touchstone.js](http://touchstonejs.io/), a React based mobile framework may sometime be released) and there are now a plethora of NativeJavascript frameworks ([NativeScript](https://www.nativescript.org/), [React Native](https://facebook.github.io/react-native/). [Titanium](http://www.appcelerator.com/mobile-app-development-products/) and [Tabris](https://tabrisjs.com/) to name a few) that are other viable options for mobile application building. 

However, this article is concerned with the Big Three frameworks that are left in Hybrid-Mobile Javascript space, so let's start the 500lb Gorilla.

#### Ionic

If most people ask me what Framework to use I pretty much always say [Ionic](http://ionicframework.com/).  The only
real question in the past few months has been whether or not to try to live on the bleeding edge and use [Ionic
2](http://ionic.io/2) or stay with the tried and true.  [Ionic 1](http://ionicframework.com/) is an open source
framework built on top of [Angular](https://angularjs.org/), providing a bunch of directives, css and a well
through out, proven way of creating mobile apps.  You can see my previous [look at Ionic](/programming/2014/10/11/mobile-frameworks-ionic/), 
which pretty much holds true for the past couple of years.  The [Ionic](http://ionic.io/) company, besides working on
Ionic, has developed an eco-sphere of paid add ons that add a fair of bit of value to the Ionic Framework.  A [cloud
service](http://ionic.io/cloud) which provides push notification, authentication services, a build server, and their
version of live update.  They also sell a [drag and drop designer](http://ionic.io/products/creator), that would
allow a designer to prototype an app and then allow a developer to bring the prototype to life without having to
start from scratch (a year ago, the last time I used it, it produced a pretty good framework to work with, a
little messy but I am sure that has improved over time).
 
And now they are at beta 11 of Ionic 2, which uses [Angular 2](https://angular.io) as the basis of Ionic 2.  This means
that it will be basically a rewrite to upgrade your application from Ionic to Ionic 2.  You might be able to keep some
of the html templates, the controllers (controllers no longer exist in Angular 2) will have to be completely
rewritten, and it is recommended (though not essential) that you switch from plain ol' Javascript to [TypeScript](https://www.typescriptlang.org/).  
However if you are starting a new project, you really should be thinking about starting in Ionic 2.  Now that
Angular 2 final has been released, I think we can expect Ionic 2 to leave beta shortly.  Although Angular 2 is almost
a completely different framework from Angular 1, it shares only a little of the philosophy and even less of the
syntax, it is a much more modern framework that has taken a lot insight from weaknesses of Angular 1 and from new
frameworks like [React](https://facebook.github.io/react/).  Since Angular 2 is more efficient at rendering HTML, it
is much more suited for the mobile environment.  It was wise of Ionic to switch to Angular 2, as staying with
Angular 1 would have left them on a dead-end framework.  
 
While I have not built a real world Ionic 2 application yet, and I might hesitate to work with Ionic 2 if I had to
deliver an app in the next couple of weeks, I think that one should definitely consider moving to Ionic 2 if you
are building an App that you wish to deliver in the next three months and are expecting to support for years, 
rather than an app your need to build in the next few days and will be doing little maintenance on.  Over the next
months and years, usage of Ionic 1 will drop off and Ionic 1 app will start seeming dated.  The hope is, now that
Angular 2 has been released the developers of Angular have truly made a framework that will last years.  Angular 1 had
a very good run and was the dominant framework for several years (maybe React has taken over with developer excitement,
Angular is still the top dog in [real world usage](https://www.similartech.com/compare/angular-js-vs-react-js)), and
with the force behind Angular 2 it will eventually become one of the most important Javascript Frameworks.
 
#### OnSen UI

[OnSen UI](https://onsen.io/) is another framework I have looked into [in the past](/programming/2014/10/16/mobile-frameworks-onsenui/), 
and was pleasantly with.  A fair bit has changed with what was written in the article, and they have just
recently released [OnSen UI 2](https://onsen.io/blog/onsen-ui-2-is-here/).  Like Ionic 2, it is pretty much 
a complete rewrite and is no longer based on Angular.  They have switched to using the [Custom Elements API](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Custom_Elements),
as the way that their &lt;on-sen&gt; components are rendered, and because of this they allow using a Vanilla JS,
Angular 1, Angular 2, React, [Vue](https://vuejs.org/) or even [Meteor](https://www.meteor.com/) as the binding 
framework.  They also provide two separate and automatically rendered skins, Material (for Android) and iOS.    
  
Like Ionic, their value add (monetization strategy) is adding features on backend (push notifications, live
app updating) as well as a build server, and a even Cloud IDE.  Unlike Ionic this is under a different name called
[Monaca](https://monaca.io/), which does not require use of OnSen, but clearly favours it.   

When reviewing a earlier version of OnSen, it required using [Yeoman](http://yeoman.io/) to Scaffold the 
application.  The latest version uses the [Monaca CLI](https://docs.monaca.io/en/manual/development/monaca_cli/) which
is a slick CLI that even shows previews of the templates when selecting them.  It's not as full featured as the
Ionic CLI, but I believe a lot of the functionality missing might be 

#### Framework 7


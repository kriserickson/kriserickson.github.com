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

If most people ask me what Framework to use I pretty much always say [Ionic](http://ionicframework.com/).  The only real question is whether or not to try to live on the bleeding edge and use [Ionic 2](http://ionic.io/2) or stay with the tried and true.  While Ionic t
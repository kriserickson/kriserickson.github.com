---
layout: post
title: "The State of HTML Mobile Frameworks in 2016"
description: "It's been over 2 years since I posted The State of Mobile Frameworks and a fair amount has changed in that time, so now is probably a good time to dive back into that thorny topic"
category: Mobile
imagefeature: blog/state-of-frameworks.jpg
tags: [Programming,Phonegap,HTML5,Cordova]
featured: true
---
#### The State of Mobile Frameworks 2016

It's been over 2 years since I posted [The State of Mobile Frameworks](/programming/2014/04/22/the-state-of-html-mobile-frameworks-in-2014/) and a fair amount has changed in that time, so now is probably a good time to dive back into that thorny topic.  Some frameworks have withered and died, some have gained functionality and popularity, and some have effectively stayed still.   It is important to note, that mostly I am focused on Hybrid app frameworks, frameworks that are designed to run solely on mobile/tablet.  If the framework's main focus isn't building mobile first applications that can be run on PhoneGap then I am not covering it here, or am looking at it in a mobile first context.  This is clearly not the way to build a modern website, where a responsive solution is always best, but it is the way to build an app that can have more functionality than a website can by utilizing features on the device that isn't currently accessible to websites (either for security reasons or just because the feature hasn't rolled out to browsers yet).
 
#### It's Dead Jim

Of the frameworks I looked at, 10 of the 12 have effectively disappeared.
 
* [jQT](http://jqtjs.com/) was dead in 2014, but was included since it was still appearing a lot in searches at the time.  Put the final nail in that coffin now. 
* [jQueryMobile](http://jquerymobile.com/)'s last release was 2 and a half years ago, it was mostly dead then.  No one should consider using it now. 
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
 
That leaves [Ionic](http://ionicframework.com/), and [Onsen-UI](https://onsen.io/).  There have been a few others 
(like [Rachet](http://goratchet.com/) which is more of a prototyping framework), but the only real new framework 
I would consider would be [Framework 7](https://framework7.io/).  This dearth of choice almost brings us to back to 2013 
when there were only a couple of options, before the explosion of frameworks of 2014.  
It certainly means that you will have less frameworks that you will be required to evaluate before making a decision, 
but it also means that if you are unhappy about one of the big three's framework design choices or appearance you have 
less options for change.  

There are certainly going to be new Frameworks in the future ([Touchstone.js](http://touchstonejs.io/), 
a React based mobile framework may sometime be released but it hasn't had any commits in the past 5 months) and there 
are now a plethora of NativeJavascript frameworks ([NativeScript](https://www.nativescript.org/), [React Native](https://facebook.github.io/react-native/). 
[Titanium](http://www.appcelerator.com/mobile-app-development-products/) and [Tabris](https://tabrisjs.com/) to name 
a few) that are other viable options for mobile application building. 

However, this article is concerned with the Big Three frameworks that are left in Hybrid-Mobile Javascript space.  All of
these frameworks come with the standards that we would expect: the standard mobile widgets, CSS that looks modern rather
than dated, styling to match either the iOS or Material design (Android) platforms, and the ability to quickly
create a modern looking mobile application with Cordova.

So let's start the 500lb Gorilla, Ionic.

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
 
##### Ionic 1 or Ionic 2? 
 
And now they are at beta 11 of Ionic 2, which uses [Angular 2](https://angular.io) as the basis of Ionic 2.  This means
that it will be basically a rewrite to upgrade your application from Ionic to Ionic 2.  You might be able to keep some
of the html templates, the controllers (controllers no longer exist in Angular 2) will have to be completely
rewritten, and it is recommended (though not essential) that you switch from plain ol' Javascript to [TypeScript](https://www.typescriptlang.org/). However if 
you are starting a new project, you really should be thinking about starting in Ionic 2.  Now that
Angular 2 final has been released, I think we can expect Ionic 2 to leave beta shortly.  Although Angular 2 is almost
a completely different framework from Angular 1, it shares only a little of the philosophy and even less of the
syntax, it is a much more modern framework that has taken a lot insight from weaknesses of Angular 1 and from new
frameworks like [React](https://facebook.github.io/react/).  Since Angular 2 is more efficient at rendering HTML, it
is much more suited for the mobile environment.  It was wise of Ionic to switch to Angular 2, as staying with
Angular 1 would have left them on a dead-end framework.  
 
While I have not built a real world Ionic 2 application yet, and I might hesitate to work with Ionic 2 if I had to
deliver an app in the next couple of weeks, I think that one should definitely consider moving to Ionic 2 if you
are building an App that you wish to deliver in months rather than weeks and are expecting to support for years. 
However if you need to build an app in the next few days that you will be doing little maintenance on, I would stick with Ionic 1.  
Over the next months and years, I belive that usage of Ionic 1 will drop off and Ionic 1 apps will start seeming dated.  
The hope is, now that Angular 2 has been released, the developers of Angular will stop changing the API and we can
have a framework that will last years without the constant breaking changes that we have endured over the past year.  
Angular 1 had a very good run and has been the dominant framework for several years (maybe React has taken over with 
developer excitement, Angular is still the top dog in [real world usage](https://www.similartech.com/compare/angular-js-vs-react-js)), 
and with the force behind Angular 2 it is hard to believe that it will eventually not become one of the most important 
Javascript Frameworks.

##### The Ionic Framework

What you get with the Ionic 2 Framework (not talking about the upsells from the company) is a pretty robust framework,
that smartly uses Angular 2 and its strengths.  They have hidden a lot of the complexity of getting the Angular 2 
framework up and running, the files are laid out in a sensible manner and they have leveraged the standard web construction
toolchain like NPM, Gulp and Sass so that anyone who has worked with these tools will not be confused with what is going
on behind the scenes, and because of this the live-reload and debugging in with sourcemaps just work when you type
<code>ionic server</code>.  It's clear that the Ionic team has taken what they learned from Ionic 1 and poured that
knowledge into Ionic 2, since you are going to pretty much have to start fresh anyway (since Angular 2 is so different
from Angular 1) you might as well remove any of the cruft from the previous framework.  

##### The CLI

You get a CLI that allows project creation.  The project creation,
like most of the CLI, requires you to set all of your options on the command line.  You have to know the name of 
the template you want to use (or specify a github repo, or a codepen url) and specify that on the command line.  
You have to remember specify --v2 if you want an Ionic 2 project rather than an Ionic project, otherwise it is
ctrl-c and delete and start again (if you caught it when it was building rather than after you spent the 5 minutes
to bring up the new project and then discover that it is a Ionic 1 app).  You have to specify --sass i8f you want
Sass rather than CSS.  This will be familiar to you if you have have run the Cordova CLI a lot, but other CLIs (and
even Yeoman) are more prompt based.

The CLI also wraps almost all of the cordova features (build, run, add platform, add plugin), and if you want the
advantages from the [Ionic Native](http://ionicframework.com/docs/v2/native/) plugin wrappers, I believe you have
to use <code>ionic plugin add</code> rather than <code>cordova plugin add</code> (though I haven't actually tried
using straight <code>cordova plugin add</code> with Ionic Native), for more information about how to use Ionic Native and how
it is different from [ng-cordova](http://ngcordova.com/) see [John Morony's](http://www.joshmorony.com/)
[article on Ionic Native](http://www.joshmorony.com/using-cordova-plugins-in-ionic-2-with-ionic-native/).

The CLI also gives you easy access to the various platform services that subscribing to the Ionic Cloud gives you, as
well as a couple of features that probably should be part of the standard Cordova CLI (like creating all your resource
files from a single icon and a single splash screen).

##### Other Ionic Products
   
Ionic provides a couple of Products.  Ionic Lab, which is a GUI frontend to the CLI.  It is clearly an early product,
but since the "About IonicLab" menu option does nothing, and there are no version numbers on the Downloads or on the
[info page](http://lab.ionic.io/), the only place were version info could be found was on their [GitHub page](https://github.com/driftyco/ionic-lab-issues) 
to track issues for the project and that claims that we are at "1.0.0-alpha.14", but that was last updated 
in July 2015 so who knows.  The app only works with Ionic 1 projects (it can only create Ionic 1 projects, and though 
it appears to load Ionic 2 projects you have created from the command line, you can't install a platform so it 
is stuck with just serving the app).  They might be waiting for Ionic 2 to be released to do a complete update, 
or maybe Ionic has abandoned this product failing to find some way to monetize it.
 
[Ionic Creator](https://creator.ionic.io) also is limited to Ionic 1 apps, but is a pretty good drag and drop mobile app creator.  While this
doesn't hold much interest for me, it might be very useful if you want to have a designer design the pages and then
have coders come through and make the app functional.  I've only played around with it enough to knock out a simple 
mock up, and you need the professional version to hook up any directives and do any code editing so I may not have
enough information to properly judge how useful the tool would be.
   
##### Final Thoughts on Ionic 2

While I haven't worked with Ionic 2 enough to know where the sharp edges are, I would be comfortable in using it in 
an application that was going to be completed in 6 months or so.  Now that Angular 2 is finally released, and the breaking
changes will finally stop (until Angular 2.1 at least), I think the release version of Ionic 2 should be just around
the corner.  Once it is released my assumption is that it will quickly become the dominant mobile application framework,
overtaking Ionic 1 in a year or so, so you might as well learn it.
 
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

##### CLI

When reviewing a earlier version of OnSen, it required using [Yeoman](http://yeoman.io/) to Scaffold the 
application.  The latest version uses the [Monaca CLI](https://docs.monaca.io/en/manual/development/monaca_cli/) which
is a slick CLI that even shows previews of the templates when selecting them.  It's not as full featured as the
Ionic CLI, but the features it does include seem a lot more user friendly than the Ionic version, in that not everything
has to be done as an argument to the command.  When you type <monaca create myproject> you are asked to choose what
type of project you want to make.

{% highlight bash %}
$> monaca create onsen-demo
? Choose a category: (Use arrow keys: ↑ ↓ →)
> Onsen UI
  Onsen UI and Angular 1
  Onsen UI and Angular 2
  Onsen UI and React
  Ionic
  No Framework
  Sample Apps
{% endhighlight %}   

You are next asked to choose a template (a nice feature is that pressing P on the currently selected template will bring
up a preview of the app in your browser):

{% highlight bash %}
? Select a template - Press P to see a preview (Use arrow keys: ↑ ↓ ← →)
> Onsen UI V2 Angular 2 Tabbar
  Onsen UI V2 Angular 2 Splitter
  Onsen UI V2 Angular 2 Navigation
  Onsen UI V2 Angular 2 Minimum
{% endhighlight %}

These are kind of nice features that would be relatively easy to add to all CLI's which make it much easier to get up
and started.

##### The Framework

Please note that I didn't spend much time with OnSen outside of the Angular 2 environment (as that is where my current
interests lie), other than playing with their pretty excellent [interactive tutorial](https://onsen.io/tutorial/),
which unfortunately does not support Angular2 yet (apparently coming soon).  So pretty much everything I have to 
complain about is more about how they supported the Angular2 framework.   

I started my little toy app (get a list of github users from the [GitHub api](https://api.github.com/users) with the 
minimum Angular 2 configuration.  The project structure seemed a little more messy to me than the Ionic 2 project structure, 
and I thought that there was an excessive amount of bootstraping required that ionic (maybe to its detriment in the future) 
hides in their own ionicBootstrap function.  The OnSen bootstrap also omits including "CommonModule", so none of the ng* directives
will work until you add that.  They are transpiling all the typescript, so not having an option to use SASS seems like
a bit of a lost opportunity.  The way they are transpiling (besides being very slow, it can take up to a minute to 
transpile a trivial app) makes it impossible do any debugging in the preview mode (all you get is a minified single 
app.js that is injected into the page through evals (using webpack), and though
there appears to be base64 encoded sourceMaps included they clearly aren't pointing to files that the browser 
can access because even when you throw in the <code>debugger;</code> into your code the only place it breaks is
in one of chromes VM files (see diagram below, with apologies to all those on mobile devices)
<span>
<img src="/img/state-of-frameworks-2016/debugging-onsen.jpg" style="border: 1px solid #000; margin: 10px auto 0" />
<span style="display: block; text-align: center; font-weight: bold">Debugging an Onsen Application</span>
</span>

There may be some way to get around this, but I haven't discovered it.  My guess is that since they are supporting a 
lot of different binding frameworks, they do not have the time to spend on getting the debugging working perfectly for
everyone of these platforms.  

I then tried using the Monaca online debugger to run the same project, but with the online site it currently only brings 
the minified compiled files into their debugger.  I assume this is because the online site does not yet have the ability to 
support webpack and the other transpiling infrastructure required to convert typescript files to standard javascript
but it makes the online editor basically useless for Angular 2.  It was also useless because (unlike in preview mode),
I couldn't get the transpiled version of the app running in the cloud to include "CommonModule", and therefor got the
following error when trying to run the application in the cloud (and on my device):

<code style="color:red"> Error: Template parse errors: Property binding ngforOf not used by any directive on an embedded template. 
Make sure that the property name is spelled correctly and all directives are listed in the "directives" section.</code>

Since the build cycle of this was so slow, after trying 3 or 4 ways to register the "CommonModules" I gave up. 

##### Final Thoughts on OnSen2

Although OnSen2 claims to be an actual release, rather than the RC that Ionic is, I would say that their Angular2 support
is very beta and early days.  Not being able to debug in Chrome Dev tools is a deal breaker for me (I am pretty sure
that this will get fixed, but launching with it this broken seems like a mistake), but if you want
a framework to work with in Angular 1 or regular Javascript, or maybe even React (although it shares the same slow
transpiling process, they have got debugging with map files working) you might want to look into OnSen.

#### Framework 7

Framework 7 is a different beast than Ionic and OnSen, in that it feels much more like a classic Mobile framework like Jquery Mobile 
or one of the many frameworks from 4 or 5 years ago.  First off all it is delivered with bower (OK, you don't have to install it with Bower, you can
[download(sic) it from Github as well](https://github.com/nolimits4web/Framework7/)), which is enough of a blast from the past, but also
it is very html based rather than programmatically based (the getting started html page is 75 lines and 3500 characters where the ionic 2 starting
page is 7 lines and 150 character).  Although it can be used with both [Angular 1](https://github.com/valnub/Framework7-Pure-Angular-Template), 
or even [Angular 2](http://embed.plnkr.co/KTzAqu0OQrP3ZmHpuGy8/) it was designed to really just use regular Javascript.
It has its own DOM manipulation framework ([Dom7](https://framework7.io/docs/dom.html) which really feels like a drop-in for jQuery), and it's own Templating library 
([Template7](http://idangero.us/template7/) which feels like HandleBars), so if you are used to HandleBars and JQuery you
will feel very comfortable here.  Also there is a distinct lack of TypeScript, ES6, JSX or even SASS, so there is no
transpiling and no complex packers, loaders, or anything else that greatly complicates the setup of the other libraries. 

##### Integration with Cordova

While you certainly can use Framework 7 with Cordova, there is no built in tooling to support it.  You are either going
to have to write your own gulp/grunt or custom script to take all of your html, javascript, and css and place it in
the www directory of a cordova project, or you can clone the [Framework 7 repo](https://github.com/nolimits4web/Framework7/)
on Github and work with their gulp script.  Cloning the repo does add a lot of stuff you will want to clean up though, and
the gulp script works off of their kitchen sink demo (they provide a Material and an iOS styled Kitchen Sink demo but
following this [tutorial](https://framework7.io/tutorials/maintain-both-ios-and-material-themes-in-single-app.html) you
can have both look and feels in the same app), so I would recommend editing their Gulp script for your own use.  This
is all fine, but it seems a little clunky in this day and age to have to do so much prep just to get hello world working.  They
might want to look at creating a [Yeoman](http://yeoman.io/) script for scaffolding the building process.

The lack of integration with Cordova isn't a big problem, it does add one more bit of code that you have to write or update (a Gulpfile) 
and another thing that you have to do every time you want to build your application.  Run the gulp or grunt script, then run cordova build (there 
is a gulp plugin to do builds for [ios](https://github.com/SamVerschueren/gulp-cordova-build-ios) and [android](https://github.com/SamVerschueren/gulp-cordova-build-android)
which I haven't used, but my experience with [grunt plugins for cordova](https://github.com/csantanapr/grunt-cordovacli) has been mixed at best).

##### The Framework
  
As I explained above, the framework is pretty simple.  It is basically a bunch of CSS, with a few javascript helpers.  You
have to initialize the main app, and every view you want to register.  If there is a component that requires initialization,
you have to manually initialize it as well.  For example if you want to have a picker, you initialize it in javascript:
 
{% highlight javascript %}
var triviaPicker = app.picker({
    input: '#trivaAnswer' // Here is where you select the element you want to activate on
    cols: [
       {
         values: ['Android', 'iOS', 'Blackberry', 'Windows Phone', 'PalmOS']
       }
     ]
});   
{% endhighlight %}

then when you want to activate it, you simply call open:

{% highlight javascript %}
$$(document).on('click', '#triviaButton', function() {
    triviaPicker.open(); 
});
{% endhighlight %}

The main problem, or at least the main challenge, is that there is no structure give for you on how to organize your pages.   The
JavaScript that they provide for you in both in the starter app, and their kitchen sink app is giant file of 
JavaScript in the global namespace (ugh).  Even if you look at a fairly nicely designed [sample app](https://github.com/GuillaumeBiton/HackerNews7),
it is still one file, with just comments to break up the pages.  If you are going to use Framework7 I highly recommend
you break your pages out into separate files, and look at a better place to store the templates than in the index.html
of the main file (perhaps load them from file when the app is loading).  

##### Final Thoughts on Framework 7

To be honest, Framework7 reminds me a lot of the [TopcoatTouch](https://github.com/kriserickson/topcoat-touch) framework 
(a framework that I cannot recommend using) that I wrote several years ago, except that it is a lot more polished and 
has much better documentation, and has an up-to-date CSS implementation.  I think it needs some proper large sample 
applications that show a decent way of separating concerns rather than shoving everything into a couple of files.  
I think it could also use a decent Yeoman generator to simplify the scaffolding process, and pre-build a gulp or grunt 
script that could concat and minify all the Javascript and CSS. However if you are more comfortable with the older jQuery 
style of development, rather than the more modern Angular and React style you could do worse than choosing 
Framework7 (you could choose [jQuery Mobile](https://jquerymobile.com/)!)

#### The Verdict

As always, it comes down to what you are going to be most productive with, what your end goal is, how long you expect
to be maintaining the application, and if you want to spend a lot of time learning instead of developing.  I can 
say without question the easiest of these frameworks to get a sample app together was Framework7.   It is very easy to
build app with, especially if you have been using jQuery and Handlebars for the past years (wow, hard to believe that
jQuery came out over 10 years ago).  The second easiest was Ionic2, it is certainly a bit trickier than Ionic 1 especially
if you are not 100% comfortable with Angular2 (check out this great article on 
[the pains of learning Angular 2](https://hackernoon.com/why-learning-angular-2-was-excruciating-d50dc28acc8a#.aupibdhf9))
but the future is pretty clearly not with Angular 1 and Ionic (unless the worlds treats Angular 2 like 
[Python 3](http://blog.thezerobit.com/2014/05/25/python-3-is-killing-python.html)).  While I really wanted to like OnSen,
and loved a lot of the features it has (like its swappable binding frameworks), I think that they should have labeled the
current Angular2 implementation beta.  It was the hardest of the frameworks to work in, the slowest, and the buggiest (I 
consider it a bug if the app works in dev mode, but not when you switch to production).  Like I said, you might like
it if you want to build an app in Angular 1 or React but I really can't recommend it at this point for Angular 2.
 
You can find the sample apps I messed around with while writing this article on [GitHub](https://github.com/kriserickson/framework-2016),
they aren't much but they might give you something to play with if you are going to explore these frameworks.






 
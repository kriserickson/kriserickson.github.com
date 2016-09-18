---
layout: post
title: "First Thoughts on NativeScript"
description: "On March 5th Telerik NativeScript, a new way of developing Mobile Apps aimed squarely at web developers.  There have been a few other platforms that have tried to do cross platform development before ..."
category: Programming
tags: [Mobile,Programming,NativeScript,JavaScript]
featured: true
---


On March 5th [Telerik](http://www.telerik.com/) released [NativeScript](https://nativescript.org), a new way of developing
Mobile Apps aimed squarely at web developers.  There have been a few other platforms that have tried to do cross platform
development before, starting with [Phonegap](http://phonegap.com/).  But there are others, 
[Titanium](http://www.appcelerator.com/titanium/) has been doing the Native component run by Javascript for past few years (though
I have never actually used it due knowing somehow who ended up paying a fortune in Titanium licensing and reading stories
like [this](http://arstechnica.com/information-technology/2012/09/when-free-isnt-developer-accuses-tool-vendor-of-extorting-customer/).
Then there is [Xamarin](http://xamarin.com/) which allows you to build apps on Android and IOS in C#.  There
are even ways of developing in [Delphi](https://www.embarcadero.com/products/rad-studio/firemonkey) if you have some
crazy desire to code in the language that [Andres Hejlsberg](http://en.wikipedia.org/wiki/Anders_Hejlsberg) developed before
writing C#.  And coming soon is [React Native](https://www.youtube.com/watch?v=KVZ-P-ZI6W4), which will be similar to 
NativeScript and Titanium in that it uses Javascript as the runtime to drive Native UI controls.

I'm not going to go into how NativeScript works, or what is different from PhoneGap or the other platforms as this
is explained best by [Telerik themselves](https://www.nativescript.org/blog/nativescript-first-public-release).  You can also 
watch the [keynote](https://www.youtube.com/watch?v=8hr4E9eodS4&feature=youtu.be) introducing NativeScript
and not have to deal with dropping audio and bandwidth issues suffered if you watched it live.  What I am going to do
is talk about the few hours I experienced playing around with it, what I think its strengths and weaknesses are and 
what Telerik can do to make NativeScript one of the pre-eminent platforms to build mobile apps on.

## The Good ##

1. I like Javascript, I am comfortable in Javascript, I believe that Javascript is only [getting better](https://github.com/lukehoban/es6features),
and I think that mobile is a natural place for Javascript.  I currently use PhoneGap, but it is definitely a [love/hate
relationship](/programming/2015/02/21/lessons-learned-from-5-years-of-phonegapcordova-development/) and if a better
platform comes along I will happily switch platforms.

2. Telerik has been designing widgets and frameworks for a long time, and has learned a lot from not only their only
own products but also from the frameworks they work in.  They have taken best of breed elements from multiple frameworks
and platforms.  The widgets they have included in the platform borrow from Android, WPF, and HTML.  But instead of 
creating a [XAML](https://msdn.microsoft.com/en-us/library/ms752059%28v=vs.110%29.aspx) implementation or clone they
have chosen to use XML and a tiny subset of CSS to support.  They have also cribbed all of the commands from the
cordova-cli so if you are familiar with that you will be instantly familiar with the NativeScript cli.

3. The platform is Apache 2 Licensed and Telerik will be making their money on tooling.  There are multiple benefits to
this, one being that you have ready access to the source code (in fact all of the UI, and libraries and everything excapt
the native runtime are included as source code in each project in a tns_modules directory) so that you can see how
extend the platform to create your own native widgets.  The fact that it is free for development will mean that it 
will get used a lot, and that is important.   And if Telerik manages the project well they will get contributions which
will help mature the project to no end, hopefully it will get contributions from people building real and complex apps
on the platform because I get the feeling that NativeScript was developed without dogfooding ([see below](#dogfooding))

4. The tooling is incredibly polished for a beta, I haven't had a single problem with it so far and their choice to clone
the functionality of the cordova cli makes it very familiar.  Even the *experiment* debug for the command line appears to work
perfectly -- and not being able to debug would probably be a deal breaker for me as I remember what debugging 
Phonegap before Dev Tools or Safari was supported for debugging ([weinre](http://people.apache.org/~pmuellr/weinre-docs/latest/) 
and debug.print was painful experience).
 
5. The way that the are allowing customization for IOS and Android looks like the best possible way to do cross platform
mobile development.   Optional automatic file inclusion based on filename (so main-page.ios.js would be included
on ios and main-page.android.js would be included on android) or you can use conditionals (if view.android or
if view.ios) to change the look and feel of apps, as well as accessing platform specific Apis.

6. The [documentation](http://docs.nativescript.org/) looks really good, and so far I have been able to find almost everything
I need in the documentation.  The current sample walkthroughs are a little shallow, but we are still in beta and hopefully
that will improve.

7. Using the best Javascript technologies like data binding with Object Observable and having TypeScript work out of the
 box.  Using node style require's for module management and basing everything on a MVVM pattern was also a wise choice 
 that will tame the potential for Javascript spaghetti code. 

8. The native/javascript bridge looks seamless, for example the FileExists code (found in 
[tns_modules/file-system/file-system-access.android](https://github.com/NativeScript/cross-platform-modules/blob/master/file-system/file-system-access.android.ts)
looks like this for android:
   
``FileSystemAccess.prototype.fileExists = function (path) {
    var file = new java.io.File(path);
    return file.exists();
};``

and this for ios:

``FileSystemAccess.prototype.fileExists = function (path) {
    var fileManager = NSFileManager.defaultManager();
    return fileManager.fileExistsAtPath(path);
};``

Nice and simple, where Android and IOS libraries just become simple Javascript objects.

## The Problems ##

1) The [styling and CSS](http://docs.nativescript.org/styling) is currently very limited.  If you look at the 
[application](http://developer.telerik.com/wp-content/uploads/2015/01/SignUpForm.png) 
created in [Getting Started with NativeScript](http://developer.telerik.com/featured/getting-started-nativescript/)
and you paid attention during the Webinar you will notice that Sebastian Witalec has set his default
Android font to Comic Sans and that the App he creates uses Comic Sans as the font for everything, there is 
currently no way I can see to change the default font.

2) Going along with the above, it looks like it is pretty hard to get things to look really polished.  The best
of the sample apps is the [tasks app](https://github.com/tjvantoll/sample-Tasks), but if you compare the mockups
(found in the [app/res/Design directory](https://github.com/tjvantoll/sample-Tasks/tree/master/app/app/res/Design))
with the current version of the app they clearly have a ways to go with styling:

<div style="text-align: center">
    <div style="display:inline-block">
        <img src="/img/nativescript/tasks-mockup.jpg" style="border: 1px solid #000; margin: 0 10px 10px 0">
        Mockup from Project
    </div>
    <div style="display:inline-block; vertical-align: top">
        <img src="/img/nativescript/tasks.jpg" style="border: 1px solid #000; margin: 0 10px 10px 0">
        <span style="margin-top: 31px; display: inline-block">
            Actual Screen
        </span>
    </div>
    <div style="height: 20px">&nbsp;</div>
    <div style="display:inline-block">
            <img src="/img/nativescript/edit-tasks-mockup.jpg" style="border: 1px solid #000; margin: 0 10px 10px 0">
            Mockup from Project
        </div>
        <div style="display:inline-block; vertical-align: top">
            <img src="/img/nativescript/edit-tasks.jpg" style="border: 1px solid #000; margin: 0 10px 10px 0">
            <span style="margin-top: 31px; display: inline-block">
                Actual Screen
            </span>
    </div>
</div>

And part of the reason you want to use Native Controls is so that things look nice and modern.  There is no obvious
way I have seen to affect the look of the Title Bar (I am sure you can change its colour, but from scanning the documentation
I have no idea how), or how to add a Menu or other control structures to the title bar.

<a name="dogfooding"></a>3) I feel that Phonegap and Cordova have problem with dogfooding and I am
concerned that might leak to Nativescript as well.  When Phonegap was it its best, Nitobi was actively using
it to develop applications for their customers.  Now that Phonegap's only real customer is PhonegapBuild there
seems to be a lot less emphasis on creating a stable product and more emphasis on [PhoneGapBuild](https://build.phonegap.com/)
and [Phonegap Enterprise](http://enterprise.phonegap.com/) and [Phonegap Desktop](http://phonegap.com/blog/2015/03/02/phonegap-app-desktop-0-1-2/)
and other for pay add-ons.  The fact that a [bug](https://issues.apache.org/jira/browse/CB-8002) that basically guaranteed 
that an IOS app would crash if you had a lot of native calls was allowed to be released and be the stable library
for 4 months is kind of disheartening.  Adobe needs to have at least one important mobile product based on PhoneGap
or this will continue to happen.  Microsoft went 5 years with WPF without having a core technology built upon it
and because of that I stipulate WPF failed to gain any traction as UI platform.  It had huge problems with Font Rendering and
performance and Microsoft didn't fix those problems until they built Visual Studio 2010, but by then most of
developers felt that WPF was a failure.  Nativescript will have the same problem unless Telerik builds an app on
top of it that is core to their business.  And it has to be an attractive App, with animations, and be respectful to
the native platforms they are on.

4) NativeScript seems to be trying to get the holy grail of multi-platform development and this might lead
to a lowest common denominator UI.  ReactNative has specifically stated that they don't see code reuse between
the UI's.  This is what Xamarin has been saying from day one as well, re-use the business logic but hand code
the UI for each platform.  NativeScript allows you to do this, but seems to be promoting the write once run
on 3 platforms, if it actually works this would be amazing but no one in my mind has managed to pull it off
in Native so far (and a lot of people would argue that the problem with Hybrid apps is that they reuse UI elements 
and end up in the [uncanny valley of apps](http://martinfowler.com/bliki/CrossPlatformMobile.html)).

**What Telerik Should Do**

1. Create awesome sample apps, that have animation, and take advantage of Native performance to do things
that just can't be done well with Hybrid apps.  Write apps that take advantage of Mobile and learn what is
needed to improve the framework, and then show us developers how it is done.

2. Dogfood the platform ([see above](#dogfooding).

3. Keep up the awesomeness:  keep up the blogging about the platform, keep the documentation up-to-date,
release regularly (but make sure to tell us how new releases will affect the old releases), and keep the
cli tooling as great as it already is.  I understand AppBuilder is important to Telerik's bottom line, but until
the NativeScript platform takes off (and this will happen mostly through free tools) they will have to make
sure that everything you can do in AppBuilder (except of course for the service value-adds) you can do with the CLI (this
is true now).

4. Starting adding as much CSS styling support as you can.  If you can do animation through CSS, do it, 
if you can't have a nice way to do animation.

5. Figure out a sane config (here is one place I would not copy phonegap) that will allow controlling aspects of
build configuration: things like allowed Orientation, and the like that are currently controlled in AndroidManifest
  and other XML files on Android and the various configuration.plists in IOS.  
  
6. Make it less brittle than Phonegap.  I haven't managed to break anything yet in NativeScript, but I haven't
really done much with it yet (and there have been no updates).  I find that PhoneGap is very brittle whenever
I change anything other than by using the command-line.  I would love it if I can add functionality in Andoird
and IOS projects without having to worry about breaking things, either that or make it so that I can literally
do everything I need without having to touch said external projects (this would be a boon for AppBuilder since
you could literally use it to build any project).

7. Personal plea (though may not be the best use of Developer time), build an extension for AppBuilder 
for the JetBrains IDE's (I would totally get an AppBuilder subscription if it worked with PHP/WebStorm). 
 
**Conclusion**

It is very early days for NativeScript and what they have done so far is very impressive.  Although I don't
think I would plan a serious App around NativeScript yet, I do look forward to version 1.0 and upcoming improvements
to the platform.  They managed to get this out before ReactNative was released, and they should charge ahead with
their lead since ReactNative will get a ton of publicity and scrutiny when it comes out.  But Facebook is dogfooding
the app, and apps they have created using ReactNative look awesome.  Since they are both going to open source it will be
interesting to see if they can incorporate elements from each other and the whole Javascript Native thing can explode
and improve!
 



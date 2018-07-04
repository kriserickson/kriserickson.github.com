---
layout: post
title: "React Native -- A Tempting Quagmire"
description: "A recent experience being asked to look into a React Native mobile has clarified some of the questions I brought up in my last aritcle on React Native, lo those 2 1/2 years ago."
category: Programming
tags: [React Native,Mobile,MNJS,JavaScript,Programming]
imagefeature: blog/react-native2.jpg
featured: true
---
A recent experience being asked to look into a React Native mobile has clarified some of the questions I brought up
in [my last aritcle on React Native](/programming/2015/11/07/a-quick-dive-into-react-native/), lo those 2 1/2 years ago.
The app was crashing, and not functioning as expected and I was asked if I could look over it and see whether it could
salvaged or was going to require a complete rewrite.  I explained that I hadn't really done much in [React Native](https://facebook.github.io/react-native/) other than write a few toy apps, but I would be happy to see what could be done.  So I installed the latest version of the react-native cli, and dug in.

The app itself was not very well written, it looked like an app that was written by programmers (and there were multiple
contributors, or at least the development company made it look like there were multiple developers from the Git commits)   
who were learning both React and React Native while they wrote the app, so the instability was more a reflection of that
than React Native itself (although the crashing was only really happening in release builds and not in the dev build).  It was
hardly a complicated app (it really only consisted of 4 screens including the login screen, and only had 7 server side API calls total).
The developers used both an event bus, and a very simple home rolled store (not [Flux](https://facebook.github.io/flux/)) that wasn't properly reactive (which was causing
a lot of the State violation troubles which caused the app to crash).  

Since this isn't an article about fixing a React Native app, or an article on how not to write React Native app so I won't
go into too much detail about that App, and how I fixed the seven or eight issues that the client had with the app.  
Service to say that the majority of the problems were resolved by adding error handling to the build (in an attempt to 
discover were things were crashing for users) and the client is happy enough that
the app isn't crashing as much and that they aren't willing to spend the extra time and money to fix the crashes so long as they don't
take the App down (I know yikes) -- and are probably going to just do a rewrite rather than invest more time and money
in the React Native route.

In spending just a few hours fixing these issues I came to understand a fair bit more real world use of React Native, however,
and I thought I would share my findings of what was good and bad about React Native in my brief experience.  These are the
experiences of someone who isn't developing an App from scratch, or who has spent a long time working with React Native, but
someone who spent a short amount of time in React Native with the specific purpose of fixing a few bugs and creating a duct
tape solution to get the client up and running again.  For a full featured look at what works in React Native and what
doesn't in a large team I highly recommend the [Blog Post on AirBnb and their experiences with React Native](https://medium.com/airbnb-engineering/react-native-at-airbnb-f95aa460be1c),
as well as the two [Fragment Podcasts](http://fragmentedpodcast.com/) with [Gabriel Peal](https://twitter.com/gpeal8) about 
the decision at AirBnb -- [Part 1](http://fragmentedpodcast.com/episodes/129/) and [Part 2](http://fragmentedpodcast.com/episodes/130/).  AirBnb had
a lot of experience with React Native (in fact, one of the first things I did with codebase was get eslint working and use the
[AirBnd React preset](https://www.npmjs.com/package/babel-preset-airbnb), which helped find a fix a ton of bugs in the
codebase). 

The Good
====
* Once the app is up and running, being able to change things very quickly through hot-reload is very nice (though that feature is shared with [NativeScript](https://www.nativescript.org/), and [Cordova](https://cordova.apache.org) through a [plugin](https://github.com/nparashuram/cordova-plugin-browsersync).
* [React](https://reactjs.org/) itself is a nice framework, that is well designed and relatively easy to learn.
* Although not as nice as [Typescript](https://www.typescriptlang.org/), [Flow](https://flow.org/en/) is better than plain Javascript.
* Nice to have an alternative to Cordova or Nativescript for multiplatform development.
* Because of WebPack and Babel you are writing in a modern version of JavaScript.  
* It has the backing of Facebook (which is still using it internally), and there are quite a few high profile [apps being developed in React Native](https://brainhub.eu/blog/famous-apps-built-with-react-native/).

The Bad
=====
* The tooling is still pretty immature, potentially because I was using a version of React (not the react-client, but the library included with the app) that was a year old, but it was very fragile.  
- You constantly had to build and build again because of locked files or random build failures.
- I never successfully was able to add a plugin "automatically", I always had to manually 
- Simple things like starting the emulator were not done (in Cordova if there is no device and no emulator running, run android is smart enough to start the emulator) where on React Native it just fails and tells you start the emulator before running again (the react-native run-android or react-native run ios command can take up to 5 minutes).
- The debugger mostly works but is kind of Ugh (if you haven't used it, what happens is a browser window is launched and then you debug that browser window, the only part that works is Sources and then you have to click on debuggerWorker.js and localhost:8080).  If you can get the dev-tools to work you can also view the component hierarchy in a seperate app.   If you want to debug things like Network on Android you have to install [Stetho](http://facebook.github.io/stetho/) or manage to get the React Native debugger to work (see below).
- I never managed to get the [React Native debugger](https://github.com/jhen0409/react-native-debugger) to work on Windows, it would launch but never connect to the App, I had a little more success with the react-devtools but it was more miss than hit in getting it to connect to the app.
* Upgrading versions is not simple.  The build I had was stuck at React Native 0.46 (and React 016.0.0-alpha.12), ReactNative (as of July 1st, 2018) is currently at 0.56.  I tried blindly updating everything to the latest of everything and nothing worked.  I spent a bunch of time slowly bumping the versions, and seeing where I could get, but each clean and release takes about 10 minutes and figuring out a magic combination of what works.  The suggested approach is to go through every release notes (here are the release notes for [React-Native 56](https://github.com/react-native-community/react-native-releases/blob/master/CHANGELOG.md#056) all 2500 words) for every version and update.  If you are developing React-Native you basically have to update your app once a month or you will get to a very bad place pretty quickly.
* The plugins are not linked to a specific version of React-Native, but you will find that some plugins do not work with certain versions of React and if someone stops supporting a plugin then the plugin will become unusable proably after 6 months or so.  
* The plugins are all linked from the ```node_modules``` directory, this causes problems on Windows, and a lot of the fixes for various problems relied on editing Java and Objective C files linked in the node_modules directory which I never did since it seemed like such a bad idea.
* Babel's handling of async and other modern Javascript features make it very difficult to Debug (async for example get turned into 
giant switch statements, variables get renamed, the handling of this is not as consitent as TypeScript).  I tried to follow [Gajus Kuizinas](https://twitter.com/kuizinas) suggestion and [not use Babel Transpilers when debugging](https://medium.com/@gajus/dont-use-babel-transpilers-when-debugging-an-application-890ee528a5b3) but because the app was written in Flow rather than JavaScipt and since the react-native packager is black box to me, I never managed to do this.
* The app behaves differently in Development mode and Release mode.  Very differently, almost all the crashes that were being reported by the client only happened in Release mode.  This may be because of react-native pacakger running in two modes, but more probably because when you debug the app in Chrome you are running in Chrome's V8 engine and not the V8 engine that is packaged on Android with React.  This might not be true on iOS, since (as seen below) I never managed to get a Release app built.
* Once again, maybe it was the version I was stuck working with, but the App was most of the time a slideshow in the Android Emulator.  You would click and as much as 2 minutes would pass before the app responded, and change screen animation could take over a minute.  I found claims that this was fixed in .52, but other claims that it was still happening (and yes I am using the Haxm Emulator that runs everything else just fine).  The app worked fine on a real device, however.
* Also when debugging on Android there was an error that happened whenever you clicked on a button (well, technically a TouchableHighlight) you got an error [Attempted to transition from state `RESPONDER_INACTIVE_PRESS_IN` to `RESPONDER_ACTIVE_LONG_PRESS_IN`, which is not supported.](https://github.com/facebook/react-native/issues/5823) which was apparently fixable by reseting the clock on your phone to exactly match your computer but I never got it to work.
* I don't know whether it is Apple and XCode's fault, or ReactNative's fault, but you can't [make a release build](https://github.com/facebook/react-native/issues/18638) (debug builds work fine) on version 9.3+ of Xcode and ReactNative less than 54.  The solution is to either upgrade (see upgrading above), or downgrade your version of XCode to 9.2.
* Compared to Cordova you really have to be willing to go into the various toolings (Android Studio and edit Gradle and Android Manifest files, and even some Java Code, and Xcode and
tweak a bunch of settings in the Gui or edit PList files).  Since I never managed to get an upgrade to work (I ended having to ```git reset``` to get back when I attempted upgrading), I don't know how editing these files plays with [```react-native-git-upgrade```](https://facebook.github.io/react-native/docs/upgrading.html), but I can imagine the mess of conflicts that will produce.
* Also unlike Cordova you won't be able to re-use most of ReactNative UI in a [PWA](https://developers.google.com/web/progressive-web-apps/), because the components 
are unique to ReactNative (though it looks like there is at least [one project](https://github.com/necolas/react-native-web) that is trying to rectify this).

Tips
===
* Get a bug reporting system working asap, as you will probably have bugs that only happen in Release Mode and other
spotty reporting in LogCat and the XCode console you will have no way to figure out what is going on.  I used 
[React Native Fabric](https://github.com/corymsmith/react-native-fabric), mostly because I am familiar with Fabric
and it is free.  You will also probably need a [sourcemap](https://github.com/mozilla/source-map) tool to convert from
the single WebPack file to something more legible.  I used [React Native Exception Handler](https://github.com/master-atul/react-native-exception-handler) to
catch uncaught errors (because it caught native errors too), but you can probably get away with just using the
ErrorUtils.setGlobalHandler.  Also if you are on Android and are rethrowing the caught Exception, you need to do that
on a setTimeout of at least 1 second as you will lose the Error Report into the ether otherwise -- React Native crashes
hard.
* Use a linter (as I said before, I used the AirBnb linter to React), it will catch a lot of stupid errors, if I had
time and this was a bigger project I would have converted to TypeScript but if not at least get the Flow that react native
projects ship with.
* Test in release mode often, I had gotten used to Dev and Release performing similarly and they really don't in React native (especially
if you are debugging in Chrome -- remember they are different Javascript Runtimes).  You don't have to do an actual build,
but ```react-native run-android --variant=release``` will put on your device a build that isn't the hot-reloading, debug
enabled build.
* If you are having trouble with Android builds, clean with:

```
cd android
gradlew clean
```   
I spent a bunch of time trying to get a build to work, only to find that by cleaning everything worked fine.
* If the JS Debugger isn't attaching, I find that killing the App on the mobile device and restarting frequently solved
that problem (also the problem of the app just having a White Screen).
* Stay on the latest version, if you get behind you are in for a world of hurt, I am pretty sure that a lot of the pain
I had with React Native was because of versioning issues, or bugs that had been fixed for months but I was seeing because
I was on a year old version of React Native.

Conclusion
====
React Native is still an interesting emergent technology, but it is not a Silver Bullet for turning Web Developers into Mobile
Developers.  Since it so raw around edges when dealing with the Native bits, you really need to have a Native Expert willing
to splunk into the guts of React Native on each platform to be successful.  My guidance would be, if you have a large
team of Web Developers and a couple Mobile Developers for each platform and you plan to do 
[Continuous Delivery](https://en.wikipedia.org/wiki/Continuous_delivery) then React Native may be a good fit for your
company.  If you are a small shop, or are creating a small app, I would recommend sticking with more traditional 
methods like going full Native or going with a more more Cross Platform solution like [Cordova](https://cordova.apache.org) 
or [Xamarin](http://xamarin.com/).
---
layout: post
title: "A Quick Dive into React Native"
description: "In my last post's comments Dave, suggested that I try (or to be honest try again) React Native.  And I thought I would give the whole MobileNativeJavaScript thing one more shot..."
category: Programming
tags: [React Native,Mobile,MNJS,JavaScript,Programming]
featured: true
comments: true
---
In my [last post's comments](http://www.agingcoder.com/programming/2015/10/15/second-thoughts-on-nativescript-react-native-and-mobilenativejavascript-in-general/), Dave (no other
name), suggested that I try (or to be honest try again) React Native.  And I thought I would give the whole MobileNativeJavaScript thing one more shot.  React Native, 
in its current form, now supports Android and iOS so it is now a closer match to NativeScript and the other MNJS frameworks.
  
It also is installed through NPM but is, shall we say, not very windows friendly.  The latest version finally install on Windows (the last time I 
tried a few weeks ago it wouldn't), though it isn't officially supported (OSX only).  So I won't complain about the issues I had getting it working with
Windows but lets just say for now you have to have a pretty good understanding of the Android build tools, gradle, and node.js to be able to get it
working on Windows at this point.  I know I should try it on my Mac but at this point my Mac is so slow that I will take the configuration over the 
pain of working with the slow Mac I own.

I followed the [tutorial](https://facebook.github.io/react-native/docs/tutorial.html) and fairly quickly had the demo Movies app up and running.
If you have any interest in React Native, it's worth spending the 15 minutes or so to go through and re-create the movies demo and pretty quickly
you will see the advantages and disadvantages of React Native.  You create a skeleton of an app, like in most frameworks, and then the CLI creates
two projects for you, an iOS Project and an Android Project.   The iOS project has to be run through xCode, whereas the android project can either
be run through the command line with

{% highlight shell %}
react-native run-android
{% endhighlight %}

or you can also run it in Android Studio (I had to do that to figure out what was going on with the Network issue I had, but more about that later).
Once the app is running on the device you can then start a local webserver which serves the javascript to the app in development.  This allows basically
instant reloads of the code, so that you can quickly make changes to your app and not go through the slow process of compiling and then pushing your
app to Android over ADB.  This is one of the best features of React Native, the almost live editing you get of the code (pressing the menu button in Android
allows you to live reload also provides access to the Debug in Chrome and the Elements Inspector (similar to the element inspector in modern Dev Tools).
ReactNative is also a little different in that it creates two app files (index.ios.js and index.android.js) which are the main application files for
the two OS Platforms.  

The idea is you create a unique UI for each platform and you can reuse non-UI code in the app, but most of the UI code is meant
to be per OS.  The other thing that is a little different is that all of the UI XML is contained within the js files.  The XML is another weird 
hybrid XML that uses the JSX syntax from React but instead of having JSX create Html it creates an XML that contains a collection of XML UI widgets) .
If you are used to React you will be used to having all your markup in your JavaScript files, if not it might be a bit of a surprise.

Getting back to the movies demo, it is pretty minimal example, but I figured it would serve as a good basis for getting up a clone of my
[Recipe Folder](https://recipe-folder.com) app.  If you haven't already, please see my [last post](http://www.agingcoder.com/programming/2015/10/15/second-thoughts-on-nativescript-react-native-and-mobilenativejavascript-in-general/) for
what I was trying to duplicate and why.  The first step was getting the recipe data, so I swapped out the movies JSON call and replaced it
with the JSON call to get a users recipes and that is where I hit my first snag:

<img src="/img/reactnative/network-react.png" style="width: 360px; border: 1px solid #000; margin: 10px auto" />
<span style="display: block; text-align: center; font-weight: bold">Meet the Red Screen of Death</span>

Well, I guess I was going to start learning more about how React Native works under the hood.  The big red error screen provided few clues into what
was wrong, so I figured I would test how debugging worked in React Native.  I pressed the Debug in Chrome button and was treated to a spinner and
another red screen, but after reading the [how-to docs](https://facebook.github.io/react-native/docs/debugging.html) on debugging in React Native
I discovered that I had to open up a WebBrowser and point it to localhost:8081/ui-debugger (makes sense, I guess I expected the react-native server
process to launch a browser for me, but oh well).  Then you have to open up the web inspector and it was at this point that I realized that the
tools were definitely aimed at Mac Users as I was told to press <span style="font-family:monospace">⌘⌥J</span> to start debugging.  And I realized that:

1. I have no idea which windows keys map to <span style="font-family:monospace">⌘⌥</span>
2. The developers tools shortcut is very different on a Mac.  
    
Eventually I realized it just wanted me to open the developer tools, and I was away at the races.  First in my script I caught the error that was thrown by the fetch and added a debugger
command to have the dev tools break in the catch.

<code>.catch(error => {
  debugger;
  console.log(error);
})</code>

The error proved unhelpful, just repeating the Network Request Error.  I added a breakpoint in the fetch library that React Native uses, and discovered
that network request was being redirected to the local webserver through localhost:8081/flow.  Digging deeper I discovered that the error was
"not a valid java.net.uri" when it got down to the actual Java code being called.  I eventually discovered that other people are having this
[problem on Android](https://github.com/facebook/react-native/issues/3115), and it probably has something to do with the fact my API has a [JSON web token](http://jwt.io/)
and the curly braces are triggering some kind of replacement in React that creates a bad URI for Java.  After spending an hour digging into this
I gave up and pointed my service at a static file which seemed to work.  A little bit of adjustment and I had a ListView with recipes showing (Huzzah!).

<img src="/img/reactnative/recipe-react.png" style="width: 360px; border: 1px solid #000; margin: 10px auto" />
<span style="display: block; text-align: center; font-weight: bold">Exciting List View</span>

Before spending too much time on styling, I decided I was going to add a ActionBar and a menu.  I searched and discovered the
[ToolbarAndroid](https://facebook.github.io/react-native/docs/toolbarandroid.html#content).  However, after spending a very frustrating hour I was stymied
with end results.  I added the markup to the render function, I imported the class, I created a container for the Toolbar and my ListView. Everything compiled
and seemed to work, but the Toolbar never showed up. I tried the Element Inspector but couldn't find hide nor hare of my toolbar.  I tried changing the
 styling, changed all the various flex stylings for the toolbar and its container.  Eventually through a bit of [cargo cult programming](https://en.wikipedia.org/wiki/Cargo_cult_programming)
I figured out that you have to style the height or it doesn't show up at all (this isn't mentioned in the docs as far as I can
see and appears to be the only component that requires setting a height).  However although I could add "actions" to the Toolbar I could
not figure out how, if it is possible, to make those actions go into a menu.  I also couldn't figure out how to style the colour
of action items. 

Next I wanted to add a new page which would show the Recipe.  Unfortunately this required re-architecting my entire App, for in
React Native as soon as you wish to add multiple pages you have to introduce a Navigator object and from looking at the various
sample apps the idea is to break out individual pages into their own files.   Using the [Movies example app](https://github.com/facebook/react-native/tree/master/Examples/Movies)
(not to be confused with the Movies tutorial app, through they appear to be similar) as a guide I created a framework
to load the two pages of my app.  It was pretty easy to style the title, and the image, and even
 the "View Original Recipe" button, but once again I flummoxed on how to create the ordered lists and unordered lists that
 show the recipe ingredients and directions.  There simply does not appear to be a way to create things like ordered lists or unordered
lists and though ReactNative unlike NativeScript does contain a WebView component that would allow for stylings of things like this, however
it doesn't at this time support it on Android.
  
It was at this point I decided that I felt the same way about ReactNative as I do about NativeScript.  
These Frameworks are really interesting technology, with very cool engineering, but don't yet provide enough significant advantages for 
someone like me to use them in this kind of uneven state.  Maybe at a later date when things are less half-baked, it will
be a useful was to quickly create Apps, for now it is mostly an interesting curiosity.  With React Native, when I wasn't fighting with mystery 
issues, I was actually having quite a bit of fun.  The React framework is a very different way of building applications.  I'm hardly an 
expert with React, having only spent a small amount of time working with it (I'm more of an Angular guy) but I do get it's appeal 
especially once you get over the mental hurdle of inter-mixing [ui and code](https://facebook.github.io/react/docs/jsx-in-depth.html).  
Once again, its a very immature framework where you will be battling with rough edges a lot since it is early days, but if you 
are a React developer, I would give React Native a try.
 

### Pro's
- Seperation of UI for Android and IOS allow for custom UI's for each platform, while reusing business logic.
- The unique development paradigm that is React, which will be attractive to React Developers (and is kind of fun to develop with if you are new to React).
- Facebook is dogfooding it by developing real apps with it.
- The interface for writing plugins is pretty simple (though they do require compilation to do native things, which NativeScript does not).
- Supports a web view (which NativeScript does not).
- App served from local webserver so the debug-edit-fix lifecycle is very rapid. 

### Con's
- Very immature and unpolished (for example Windows isn't supported, and Android support arrived last month and is very rough).
- Errors are confusing, and you may end up splunking in Android Studio in Java or Objective C in XCode to figure out what is actually going wrong.    
- Your separate UI's for Android and IOS are going to have a lot of code duplication in them.
- Still hard to style things to make them as attractive as their native counterparts. 
- Currently missing a lot of core functionality that will eventually be provided by plugins, and no way to directly manipulate things like grpahics (from 
 what I can tell the current hack is to use an embedded WebView and use the canvas).
 
Overall I find ReactNative interesting in that it is bringing something different to the MobileNativeJavaScript, and once
again it is an interesting piece of engineering.  It is still too early to actually build a real application in it unless
you are Facebook and have access to engineers who are building it (looking at the list of [apps](https://github.com/ericvicenti/react-native-community/#on-the-app-store)
that are in the App Store built with it you will see a bunch of very basic, and pretty plain looking apps, none on Android).
It will be interesting to see how development goes on React Native but I would wait before investing too much time learning it.


  
  











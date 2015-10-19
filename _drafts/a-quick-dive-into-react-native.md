---
layout: post
title: "A Quick Dive into React Native"
description: ""
category: Programming
tags: [React Native,Mobile,MNJS,JavaScript]
---
{% include JB/setup %}
In my [last post](http://www.agingcoder.com/programming/2015/10/15/second-thoughts-on-nativescript-react-native-and-mobilenativejavascript-in-general/), Dave (no other
name), suggested that I try (or to be honest try again) React Native.  And I thought I would give the whole MobileNativeJavaScript thing one more college try.

React Native, in its current form, now supports Android and iOS so it is now a closer match to NativeScript and the other MNJS frameworks.  It also is installed through NPM but is, shall we say, not very windows friendly.  The latest version finally works on windows (the last time I tried a few weeks ago it wouldn't), though it isn't officially supported (OSX only).  So I won't complain about the issues I had getting it working with Windows but lets just say for now you have to have a pretty good understanding of the Android build tools, gradle, and node.js to be able to get it working on Windows at this point.  I know I should try it on my Mac but at this point my Mac is so slow that I will take the configuration over the pain of working with the slow Mac I own.

I followed the [tutorial](https://facebook.github.io/react-native/docs/tutorial.html) and fairly quickly had the demo Movies app up and running.
If you have any interest in React Native, it's worth spending the 15 minutes or so to go through and re-create the movies demo and pretty quickly
you will see the advantages and disadvantages of React Native.  You create a skeleton of an app, like in most frameworks, and then the CLI creates
two projects for you, an iOS Project and an Android Project.   The iOS project has to be run through xCode, whereas the android project can either
be run through the command line with

<code>react-native run-android</code>

or you can also run it in Android Studio (I had to do that to figure out what was going on with the Network issue I had, but more about that later).
Once the app is running on the device you can then start a local webserver which serves the javascript to the app in development.  This allows basically
instant reloads of the code, so that you can quickly make changes to your app and not go through the slow process of compiling and then pushing your
app to Android over ADB.  This is one of the best features of React Native, the almost live editing you get of the code (pressing the menu button in Android
allows you to live reload also provides access to the Debug in Chrome and the Elements Inspector (similar to the element inspector in modern Dev Tools).
ReactNative is also a little different in that it creates two app files (index.ios.js and index.android.js) which are the main application files for
the two OS Platforms.  The idea is you create a unique UI for each platform and you can reuse non-UI code in the app, but most of the UI code is meant
to be per OS.  The other thing that is a little different is that all of the UI Xml (and it is another weird hybrid Xml that uses Reacts JSX but instead
of for Html it is for a Xml that contains default UI elements for React Native as well as any you define yourself) is contained within the js files.
If you are used to React you will be used to having all your markup in your JavaScript files, if not it might be a bit of a surprise.

Getting back to the movies demo, it is pretty minimal example, but I figured it would serve as a good basis for getting up a clone of my
[Recipe Folder](https://recipe-folder.com) app.  If you haven't already, please see my [last post](http://www.agingcoder.com/programming/2015/10/15/second-thoughts-on-nativescript-react-native-and-mobilenativejavascript-in-general/) for
what I was trying to duplicate and why.  The frist step was getting the recipe data, so I swapped out the movies JSON call and replaced it
with the JSON call to get a users recipes and I hit my first snag:

<img src="/img/reactnative/network-react.png" style="width: 360px; border: 1px solid #000; margin: 10px auto" />
<span style="display: block; text-align: center; font-weight: bold">Meet the Red Screen of Death</span>

Well, I guess I was going to start learning more about how React Native works under the hood.  The big red error screen provided few clues into what
was wrong, so I figured I would test how debugging worked in React Native.  I pressed the Debug in Chrome button and was treated to a spinner and
another red screen, but after reading the [how-to docs](https://facebook.github.io/react-native/docs/debugging.html) on debugging in React Native
I discovered that I had to open up a webbrowser and point it to localhost:8081/ui-debugger (makes sense, I guess I expected the react-native server
process to launch a browser for me, but oh well).  Then you have to open up the web inspector and it was at this point that I realized that the
tools were definitely aimed at Mac Users as I was told to press <span style="font-family:monospace">⌘⌥J</span> to start debugging.  And I realized that a) I have no idea
which windows keys map to <span style="font-family:monospace">⌘⌥</span> and b) the developers tools shortcut is very different on a Mac.  Eventually I realized it just wanted
me to open the developer tools, and I was away at the races.  First in my script I caught the error that was thrown by the fetch and added a debugger
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
[ToolbarAndroid](https://facebook.github.io/react-native/docs/toolbarandroid.html#content).  However, after spending a very frustrating hour I never
managed to get it to show up.  I added it to the render, I added the class, I created a container for the Toolbar and my ListView. Everything compiled
and seemed to work, but the Toolbar never showed up.  I tried the Element Inspector but couldn't find hide nor hare of my toolbar.  I tried changing the
 styling, changed all the various flex stylings for the toolbar and its container.  Tried every bit of [cargo cult programming](https://en.wikipedia.org/wiki/Cargo_cult_programming)
I could think of, but no luck.  Eventually I gave up, and went to style the Recipe page.  This went pretty well again, however once again when I had
to style the ordered lists and unordered lists I hit a wall.  There simply does not appear to be a way to create things like ordered lists or unordered
lists and once again ReactNative like NativeScript is missing a webview component that would allow for stylings of things like this.  It was at this point I decided
that I felt the same way about ReactNative as I do about NativeScript.  These Frameworks are really technology, with very cool engineering, but don't
yet provide enough significant advantages for someone like me to use them.








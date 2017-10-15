---
layout: post
title: "Flutter: A quick look at a new Cross Platform Mobile App Toolkit"
description: "Well over a year ago, Google (well, at least Google developers built it -- it's said to be made with 'contributions by Google and the community', introduced yet another Mobile Toolkit that allows building apps for both iOS and Android."
category: Programming
imagefeature: blog/flutter.jpg
tags: [Mobile,Programming,Dart]
featured: true
---

#### Introduction

Well over a year ago, Google (well, at least Google developers built it -- it's said to be made with "contributions by Google and the community"<sup>[ref](https://flutter.io/faq/#who-makes-flutter)</sup>), introduced yet another Mobile Toolkit that allows building apps for both iOS and Android.
Although it is still boldly declared as an alpha release (even after over year and a half), it differs from most
of the cross platform toolkits in some interesting ways so I decided to spend some time with it to see if it was
shaping into a reasonable solution for creation cross platform Apps.

#### What Exactly is Flutter

Flutter is a bit of a strange beast -- it runs fully natively, but uses Dart as its "lingua franca" (as far as I understand compiling
Dart into optionally Java or Kotlin on Android and into Object-C or Swift on iOS).

<img src="/img/flutter/new_project.png" style="border: 1px solid #000; margin: 10px auto 0" />

It doesn't use native widgets, but uses its own C++ Rendering (written with [Skia](https://en.wikipedia.org/wiki/Skia_Graphics_Engine))
to quickly draw native-like widgets.  The authors state that they are doing this to ship higher quality widgets otherwise
"the quality and performance of Flutter apps would be limited by the quality of those widgets"<sup>[ref](https://flutter.io/faq/#does-flutter-use-my-systems-oem-widgets)</sup>.
They claim to be inspired by React's style, and use code rather than markup to create UI, and not even in the JSX sense but literally
you create UI by creating objects as seen in the definition of a ChatWindow from their tutorial:

{% highlight csharp %}
  @override
  Widget build(BuildContext context) {
    return new FadeTransition(
        opacity: new CurvedAnimation(
            parent: animationController, curve: Curves.easeOut),
        child: new Container(
          margin: const EdgeInsets.symmetric(vertical: 10.0),
          child: new Row(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: <Widget>[
              new Container(
                margin: const EdgeInsets.only(right: 16.0),
                child: new CircleAvatar(child: new Text(_name[0])),
              ),
              new Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: <Widget>[
                  new Text(_name, style: Theme.of(context).textTheme.subhead),
                  new Container(
                    margin: const EdgeInsets.only(top: 5.0),
                    child: new Text(text),
                  ),
                ],
              ),
            ],
          ),
        ));
  }
{% endhighlight %}

While I am not opposed to this methodology (and in the future if Flutter got huge I am sure some kind of Visual Designer could
be written for it), I find it interesting that they would specifically state that they are targeting "designers and prototypers" for
this Toolkit, and yet chose to make a very non-visual (I know that HTML and XML is not visually representational of what is produced
but it I think it is easier to picture than a Object Definition).  That said, the Hot Reload functionality may be a way to quickly
iterate though ideas and bring a native like app to production faster than the slower build process of Android Studio or XCode.

#### Dart is the Language

Clearly Dart is not as dead a language as I thought it was.  While the [Dartium browser is dead](https://webdev.dartlang.org/tools/dartium),
 and Dart as the language to replace Javascript is clearly not the success it was hoped it be (used by Google but by few others, kind
 of on the scale of [Kotlin for Web](https://kotlinlang.org/docs/tutorials/javascript/kotlin-to-javascript/kotlin-to-javascript.html),
 [Elm](http://elm-lang.org/), [clojurescript](https://github.com/clojure/clojurescript), or [GWT](http://www.gwtproject.org/).  Used
 by a few developers who love it, but not really setting the Development on fire.

 Perhaps Flutter was seen as a way to bring prominence to Dart, maybe other more popular languages didn't have either the
 syntax or the toolchain required for Flutter, but the choice of the [Dart language does kind of stick out](https://flutter.io/faq/#why-did-flutter-choose-to-use-dart).
 Not that it's  a bad language, by any stretch of the imagination, it's a nice modern language that will feel very familiar
  to anyone who has used an Object Oriented language developed in the past 10 years (or almost 20 years for C#).
  It's just a big ask to get new developers to learn a language that  is not very widely used.  It's not hard to lean,
  and anyone with Familiarity with any of the [Algol](https://en.wikipedia.org/wiki/ALGOL)
 family of languages (C, Java, C#, and to a lesser extent Javascript) will be able to pick it up relatively quickly, but
 one might of thought with the recent push to [Kotlin](https://blog.jetbrains.com/kotlin/2017/05/kotlin-on-android-now-official/) in
 Android, Google might have chosen Kotlin as the language to use -- it certainly seems capable in both syntax and [toolchain](https://github.com/JetBrains/kotlin-native)
 but perhaps they hesitant to use a language that they don't have as much control of.

#### Intellij is the IDE

Another interesting thing about Flutter is that the IDE they support (though you can build Flutter apps without any IDE and you
text editor of choice) is [Intellij](https://www.jetbrains.com/idea) and not Android Studio (this might be a licensing issue
with how you can use the Intellij Platform and Plugins and such, but it is still interesting).  Note: you can use the community
edition, and are not required to buy the Enterprise Edition, so don't let that dissuade you from using Intellij if you do decide
to do some Flutter development.

The polish that the Intellij Flutter Plugin has (especially since Flutter is still considered Alpha) is very impressive, and I
don't know if that speaks to how easy it is to extend Intellij or how good the developers of Flutter are at working with Intellij (maybe
a bit of both).  Intellisense, Code Inspection, Debugging with hot-reload, is all seamless and higher quality than a lot of the
non-Jetbrains language plugins that I have used.  For me, using Jetbrains products every day, the decision to use Intellij rather than
writing their own or piggybacking on the Chrome Dev Tools is huge plus.

#### Documentation

The [Flutter site](https://flutter.io) is very polished and provides a great way to get started with Flutter.  They have Code-Labs
that walk you through not only installing the SDK, but building some relatively complicated applications (including a [Chat Application
that supports Firebase on the Backend](https://codelabs.developers.google.com/codelabs/flutter-firebase/#0)).  While the documentation
isn't perfectly organized, almost everything you need to know is there if you look hard enough (another quibble is that the search
is just a Google Search against flutter.io, but it mostly works).  It's nice to see that they took documentation and the getting started
tutorials so seriously.  BTW if you are going to develop for Flutter, there is not only the [main information page](https://flutter.io),
but also the harder to find [Docs Page](https://docs.flutter.io/index.html) -- yes I know it should be obvious but it took me a while
to find and it is kind of essential for doing actual flutter development.

#### Material Design

Another thing to point out, is that Flutter Apps look great from the get go.  They look like they are using native widgets (even though they
aren't), and you don't have to much to get a pretty good looking app form the get-go.  While you do have to do some mucking around with
the strange ["Cupertino Widgets"](https://flutter.io/widgets/cupertino/) to get the iOS look and feel, I think we can all agree that code
that looks like the following is ugh:

{% highlight csharp %}
child: Theme.of(context).platform == TargetPlatform.iOS
    ? new CupertinoButton(
        child: new Text("Send"),
        onPressed: _isComposing
            ? () => _handleSubmitted(_textController.text)
            : null)
    : new IconButton(
        icon: new Icon(Icons.send),
        onPressed: _isComposing
            ? () => _handleSubmitted(_textController.text)
            : null),
{% endhighlight %}

It's no worse than the separate project files you need in [React-Native](https://facebook.github.io/react-native/), similar
if contortions you have to do in [NativeScript](http://docs.nativescript.org/), and CSS fixes required for nice Cross Platform
[Cordova Apps](http://cordova.apache.org/).

#### Api Integration

As anyone who has built a real app on Cordova, or with any other cross platform toolkit, you know that unless you are
making a very simple [Line of Business App](https://en.wikipedia.org/wiki/Line_of_business) you will need to use the
Native API's at some point -- otherwise you might as well just be building a mobile web page.  Flutter supports API
calls with [packages](https://flutter.io/using-packages/), and has around [50 pre-built in packages](https://pub.dartlang.org/flutter/packages)
that have a lot of functionality of the various Cordova plugins.  And there are fairly simple instructions
for creating your own [plugins](https://flutter.io/developing-packages/) or calling platform specific
code using [platform channels](https://flutter.io/platform-channels/).  I admit that I did not actually write one of these
myself, but I did play with platform-channels on Android (the platform I am most familiar with) and it seems
on the surface to be pretty well thought out.  I also looked at the source code from a couple of the more simple
plugins like [location](https://github.com/Lyokone/flutterlocation) and it didn't seem too challenging to write a simple plugin.

#### Overall

I was happily surprised by how polished and non-frustrating (unlike, for example ReactNative) it was to get up and started with
Flutter.  I haven't built anything of size or import with it yet (and to be completely honest, I don't know exactly what set
of circumstances would push me towards building an App in Flutter even when it it was deemed to be 1.0 release), but the
App I built was built in a few hours and with very little gnashing of teeth or pulling out my hair.  The IDE experience was
polished and a breeze to use, and errors actually made sense and were easy to debug and fix.

#### Why I would Consider It

* Cross Platform - I think that building an App on two platforms with Flutter rather than just one wouldn't add too much extra dev time.
* Hot Reload - Works pretty well, sometimes it gets messed up if you [change your class a little too much](https://flutter.io/faq/#hot-reload), but that is to be expected.
* Unit Testing - I didn't dig too deep into the unit testing, but it is clear that there is a [deep testing infrastructure](https://flutter.io/testing/).
* Looks good by default - Clean material design, even if it isn't native, does look good.  Easily supports animation.
* Great IDE Integration - The installing SDK to having an App Running and Debugging is faster than anything I have used yet (even native or Cordova).

#### What would give me pause to develop an App in Flutter

* Still an alpha,
* Hiring support, how many developers are familiar with Dart?
* Not native widgets (when Apple or Google rolls out a new design language will require rewriting all the C++ code to make it look right).
* What if Google or its developers decide to stop supporting it, stuck on a dead platform with no possible re-use of the code.
* Not [a lot real world Flutter apps](https://flutter.io/faq/#who-uses-flutter) (a bunch of internal Google apps, and the [Hamilton Musical](https://play.google.com/store/apps/details?id=com.hamilton.app) app.
* A little uncertain of the advantages over the other main non-native widget toolkit -- the web and Cordova, where you can get a lot of code-reuse and a ton of developers available are familiar with the paradigm, frameworks and language.  Yes Flutter will probably perform a fair bit bitter, but now that [WkWebView](https://github.com/apache/cordova-plugin-wkwebview-engine) is more usable now, the only real devices that suffer performance are Android Devices pre-chrome (i.e. Android before 4.4) which are rapidly disappearing (currently less than 10% of the Android market).


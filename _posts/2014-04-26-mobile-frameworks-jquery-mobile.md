---
layout: post
title: "Mobile Frameworks -- jQuery Mobile"
description: "Last time we dealt with the grandaddy of all HTML5 Mobile Frameworks, now lets look at the 800 lb Gorilla.  jQuery Mobile
is bar far the most well known and commonly used Mobile Framework (and while I admin I'm going mostly by number of StackOverflow
question count, number of books available, number of articles on the web, which may also be influenced by the fact it has been
around for a few years, it still hasn't been around as long as jQTouch). It has gone through several iterations -- with
each iteration making ..."
category: Programming
tags: [Mobile,Cordova,Programming,Phonegap,HTML5,jQuery Mobile]
---


This is Part 3 in multipart series on the State of Mobile Frameworks in 2014, if you haven't already read the previous articles, they are here:

* [Part 1 - The State of HTML Mobile Frameworks in 2014](/programming/2014/04/22/the-state-of-html-mobile-frameworks-in-2014/)
* [Part 2 - Mobile Frameworks -- JQT (Formerly jqTouch)](/programming/2014/04/24/mobile-frameworks-jqt/)

***Note***

[Recipe Folder](http://recipe-folder.com) version 1 was built in jQuery Mobile (version 1.3).  I am intimately familiar
with it and all the hacks required to get a hybrid app working with it and how to get lists to semi-decently scroll in it.
I personally would not use it again for a hybrid app where I didn't want the app to look like a generic jQuery mobile app.  

*jQuery Mobile*

Last time we dealt with the grandaddy of all HTML5 Mobile Frameworks, now lets look at the 800 lb Gorilla.  jQuery Mobile
is bar far the most well known and commonly used Mobile Framework (and while I admin I'm going mostly by number of StackOverflow
question count, number of books available, number of articles on the web, which may also be influenced by the fact it has been
around for a few years, it still hasn't been around as long as jQTouch).  It has gone through several iterations -- with
each iteration making fairly major changes (the 1.3 to 1.4 upgrade guide is over 3000 words, and personally I have found
upgrading between versions difficult to the point that I favoured a rewrite rather than upgrading between 1.3 and 1.4).  It was
looking pretty dated until the 1.4 release, but has come out with a newer flat look:

<style>
.phoneComparison > div {
    display: inline-block;
    width: 49%;
    text-align: center;
    font-weight: bold;
}
</style>

<div class="phoneComparison">
<div>
<img src="/img/mobile_frameworks/jquerymobile-1.3.jpg">
<span>jQuery Mobile 1.3</span>
</div>

<div>
<img src="/img/mobile_frameworks/jquerymobile-1.4.jpg">
<span>jQuery Mobile 1.4</span>
</div>
</div>

However, the main problem with jQueryMobile is that it has been designed from the beginning to be a framework that
works on all mobile devices.  This is a laudable goal, however, it makes it particularly inappropriate for Phonegap
projects unless you actually are planning on creating a project for 5 or 6 different devices.  In the change from 1.3
to 1.4 the jQuery Mobile team has aimed the framework to be more of a responsive framework for all webpages rather than
a mobile first framework and it shows.  jQuery Mobile is more akin to bootstrap than it is to a true mobile framework.
So while I could recommend jQuery Mobile for a site that was not going to become an app, I can't really recommend it
for creating Phonegap apps.

**How it Works**

jQuery Mobile applications are created as single web page divided (no pun intended) with DIV's into pages (you can also load
external pages rather than using DIV's for pages).  The skinning is done through a combination of CSS and Javascript
with standard html elements being given classes to make them into mobile widgets.  There is no proscribed MVC framework
or any support of data-binding but a router is built in.  Of course you can override that router and then it will work with
frameworks like [Backbone](http://backbonejs.org/), however that may feel a bit hacky.  For data binding you can easily
choose a framework like [Knockout](http://knockoutjs.com/) but you have to be careful as if you change any of the HTML
without calling _refresh_ you will get an unskinned or improperly skinned widget.

**Advantages**
- Easy to use.
- Most populate mobile framework, because of that it has lots of plugins, books, and articles supporting it.
- Is documented (not the greatest organization, but everything is there).
- Theme Builder makes it easy to change Theme Colors.
- Wide set of widgets.

**Disadvantages**
- Huge Codebase (and very complex, unlike jQTouch it isn't really changeable).
- Slow, a lot of tricks and hacks are required to try to get a near native experience.
- Becoming less popular as more modern frameworks are coming out.
- If you have to dynamically change lists, and other UI elements you will find yourself constant calling the
  'refresh' method of each object.

**Summary**
I've used jQuery mobile a fair bit, and though you can quickly create an application with it, you will end up spending
a lot of the time you saved quickly creating application tweaking and trying to figure out how to get a more native
feel to your application.  There is a lot of functionality and widgets in the jQuery Mobile toolkit, however with all that
power comes with a lot of overhead, especially if you aren't going to be using all of the widgets and if you don't need
to support.  Another added feature in 1.4 is the ability to create a custom build that doesn't include quite as many
features, however, if you are going to use this, do it from the beginning do not include the entire version of jQuery Mobile
and then try removing features one at a time as you can spend a ton of debugging missing features, or just building
dozens of versions when you discover some feature you didn't think you needed was actually necessary on page 7 of your
application.  My general recommendation for jQuery mobile is to use it for websites that are primarily mobile but to avoid
it for building applications that will be installed on devices unless you have no problem with that application looking
like a generic jQuery mobile application.

I will end with [Brian Leroux's](https://twitter.com/brianleroux/) (one of Phonegap's original creators) addition to the
[#FiveWordTechHorros Meme](https://twitter.com/search?q=%23FiveWordTechHorrors&src=hash) from a few months ago:

<div style="width:500px;margin: 0 auto 20px;">
<blockquote class="twitter-tweet" lang="en"><p>use jquery mobile with phonegap <a href="https://twitter.com/search?q=%23FiveWordTechHorrors&amp;src=hash">#FiveWordTechHorrors</a></p>&mdash; xnoɹǝʃ uɐıɹq (@brianleroux) <a href="https://twitter.com/brianleroux/statuses/410650764101439488">December 11, 2013</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
</div>



Next up, [Bootstrap](/programming/2014/05/08/mobile-frameworks-bootstrap/)...


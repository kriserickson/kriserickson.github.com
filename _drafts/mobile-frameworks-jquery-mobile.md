---
layout: post
title: "Mobile Frameworks jQuery Mobile"
description: ""
category: 
tags: []
---
{% include JB/setup %}

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



**Disadvantages**



**Summary**



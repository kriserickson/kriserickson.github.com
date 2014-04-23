---
layout: post
title: "Mobile Frameworks JQT (Formerly jqTouch)"
description: "Continuing on from our overview, an in depth look into JQT"
category: Programming
tags: mobile,html,phonegap
---
{% include JB/setup %}

JQT (formerly jqTouch) is the Grandaddy of all of the HTML5 Mobile Frameworks and is almost 5 years old (a lifetime
in mobile web frameworks), I guess [iUI](http://www.iui-js.org/) but jqTouch was my introduction to mobile web development.
Initially jQuery plugin (remember the time when everything was a jQuery plugin?) it grew into a relatively fully functional
framework over time.  It was pretty actively developed in 2012, however the main work on it in 2013 seemed to be to port
it to CoffeeScript (Ugh, no love of Coffeescript from me).  It still has never officially reached version 1.0, and has
gone through 3 maintainers, and is looking a little long in the tooth these days (especially if you download the [Zip
from the jQT](https://github.com/downloads/senchalabs/jQTouch/jqtouch-1.0-b4-rc.zip) website, rather than getting
the [latest version from Github](https://github.com/senchalabs/jQTouch/archive/master.zip).

Originally jqTouch had 2 themes, a Apple theme that looked like the iPhone's original 2007 Apple Theme:

<img src="/img/mobile_frameworks/jqt-apple.jpg">

and their own theme, which looked pretty modern at the time but is pretty dated now (notice the nice faux leather
stitched navbar, and the glossy buttons.

<img src="/img/mobile_frameworks/jqt-jqt.jpg">

All that said, if you want to overhaul the css's look and feel (it was ported from css to sass a while ago which should
make it a lot easier to change the style) and you are looking for a simple Framework there are a few plus's to JQT.

+ Lightweight and small and should be pretty fast (though the CSS it is using is outdated for IOS).
+ Familiar so it will take very little time to get up and running.
+ Very simple source,  easy to change and to understand.  Only thing slightly complicated code is the CSS.
+ It's been around for a long time so there are posts about it on Stackoverflow.
+ There are some good books [Building Android Apps with HTML, CSS and Javascript](http://jonathanstark.com/android-book),
  and [Building iPhone Apps with HTML, CSS, and JavaScript](http://jonathanstark.com/iphone-book), though they are a little
  dated, and a good screencast for beginners [Meet jQtouch](https://peepcode.com/products/jqtouch) also a little dated.

And then there are the negatives, which grow day by day.

+ Sencha pushes their SenchaTouch product, and although they control jqTouch they don't seem to be actively working on it,
 it is officially still stuck on Beta4 (from Feb 2012).  All of the old active Forks (which was  were new features were developed)
 haven't been updated in a long time.
+ Looks really dated (see screenshots below) so it will require a ton of work to get it to look up to date.
+ Missing modern UI features which will have to be implemented by hand.
+ Worked on Android but never tested heavily on Android so really best for iPhone Apps.
+ If you use the latest version you'll have to make any changes in CoffeScript (don't get me wrong, I <strike>love</strike> **hate** CoffeeScript
  as much as the next guy).

So, to sum up, I see little reason to use the antiquated JQT unless you perhaps you are working on legacy project that
already uses it.

Next up, jQuery Mobile...
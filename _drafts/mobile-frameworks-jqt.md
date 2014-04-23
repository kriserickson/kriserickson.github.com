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

Originally jqTouch had 2 themes, a Apple theme that looked like the iPhone's original 2007 App's



Pros –
    Lightweight and small and should be pretty fast (though the CSS it is using is outdated for IOS).
    Familiar so it will take very little time to get up and running.
    Very simple source,  easy to change and to understand.  Only complicated code is in the CSS .
    It's been around for a long time so there are posts about it on Stackoverflow.
Cons –
    Is mostly abandoned, is officially still stuck on Beta4 (from Feb 2012), and hasn't been updated in a year.  All of the old active Forks haven't been updated in a long time (datazombies hasn't been updated in a year, Beedesk the same, ericcleammons 3 years ago).
    Looks really dated (see screenshots below) so it will require a ton of work to get it to look up to date.
    Missing modern UI features which will have to be implemented by hand.
    Never really had any android love, one look for all devices.


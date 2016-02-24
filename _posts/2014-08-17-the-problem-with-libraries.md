---
layout: post
title: "The Problem with Libraries"
description: "Before I go too deep down this rat/rabbit hole, I should state that Libraries are what has allowed programming to develop from where only the best of the best can produce software to a place where a plumber like me can still produce some pretty amazing stuff."
category: Programming
tags: [programming, craftwork, professionalism]
---


Before I go too deep down this rat/rabbit hole, I should state that Libraries are what has allowed programming to
develop from where only the best of the best can produce software to a place where a plumber like me can still
produce some pretty amazing stuff.  Open source and libraries and tools have been the reason for the
explosion of amazing software and computer greatness in general of the 2000s.  We owe much to those who create
libraries, and contribute to libraries in any way.  You can probably thank jQuery for bringing Web 2.0 to 
all but the biggest web sites (which could afford to hire programmers to work through all of the browser
incompatibility issues) and for bringing about a resurgence in the web that resulted in HTML5.  

Modern web frameworks (really just a collection of libraries and generally methodology or code of practice for
using said libraries) brought a renaissance to web development with Ruby on Rails which basically changed the way that
websites were designed.  MVC was resurrected from the [Gang Of Four](http://en.wikipedia.org/wiki/Design_Patterns)
and became the defacto standard off how to build a website.   And I know that libraries have been
around as long as software has been written, and frameworks almost as long.  

However there is a downside to libraries and frameworks that becomes more prevalent with the explosion of 
libraries, and that is the explosion of complexity added to your project by including a library.  A lot of
developers Google for a library before they think about how much work it would be to write the code
themselves (I am as guilty about this as anyone, a few years ago I would start a project with jQuery, add
jQuery-UI, and then add 10-15 jQuery or jQuery-UI plugins and have 20 external dependencies on a project in
a flash).  Designers love adding jQuery plugins, with little or no understanding how they work and without
realizing that the simple image rotator they needed could be written with 1-2 lines of code rather than a
10K library.  Library growth adds so much complexity to a project without you realizing it: a jQuery plugin to
do image rotation steals the mouse wheel and now your client is complaining because they can't scroll the screen.

I used to hate the NIH (Not Invented Here, were all technology must developed in house) attitude and in a lot of
ways I still do: if your core competency as a company is not
writing a payroll application, buy a payroll application do not write it yourself.  But the more I have worked with
libraries, and even very very good libraries written by people far more talented than myself, the more I find that
unless they are very easy to understand what is going on, you will frequently find yourself getting into the weeds
and spending hours figuring out what is going on in someone else's code.  Including a large library or framework in
your application does several things:

1. You take on all the technical debt of that library framework.  If there is a ton of code that is dealing with
IE8 inconsistencies and you are not supporting IE8 your program just became that much more complicated because of
it.  If the code was written years ago an never re-written you take on all the years of technical debt acquired
by the project.  If the project is brand new, it is probably relatively untested and you get to take on all of
the bug fixes and api adjustments while it is being improved.   I'm sure that there is a happy medium of projects
that are a couple of years old.

2. You have to constantly verify that the library is up-to-date and working: Browsers these days are evergreen,
and constantly updating, it is not like a few years ago when you only had to test your site against changes once every
couple of years now every month Firefox, and Chrome update their browsers and things might break.  For example I used a
calendar plugin on my wife's site and it stopped working, and the problem was the plugin was handling an error in
Firefox 3, that no longer exists and thus the calendar stopped working in firefox.  Unfortunately the author had long
abandoned the plugin and I had to spelunk through the source code and track down the bug.  Would it have been
better to write the calendar plugin myself, god no! but expecting code that other people have written to work forever
is naive so you have to be aware of this when you take on the dependency of plugin.

3. You just hired (without paying anything) the developer[s] of that library.  If it is an open source project,
sou have no say over what they are doing or how they work (and you have no right to say this, you aren't paying them remember),
but you have become reliant them.  If you are waiting for the next version to fix some issue you have, and they have to
take a month off to complete a project that is actually paying them, who are you to complain?  If they get a [new] job
and can no longer work on the project, well, you can fork the project but you now have two projects to work on.

4. If you have to change their library for some reason, and they don't accept your pull request, you have to keep
merging all changes into you change or accept that the library will never be updated again.

Like I said at the beginning, libraries and frameworks are awesome and powerful, but with great power comes some
developer responsibility.  Always ask yourself, do I really need to take this dependency on.  What are the side
effects of taking this library on.  When was this library written and how often is it updated.  Did the library
author write tests, and are they good tests.  How many people depend on this library (the more who depend on it
the more stable it probably is, but the more rigid it is going to be and the less the author is probably willing
to make changes for your requirements).  Do I have 100% trust in the library (like say [jQuery](http://jquery.com),
[Angular](https://angularjs.org/) or [Bootstrap](http://getbootstrap.com/) for example) or am I willing to fix issues
that I encounter when using the library.  How much of the library am I actually going to use --
[Micro Libraries](http://microjs.com/) are often an excellent solution instead of including an
all encompassing library as they are frequently small enough to quickly understand everything they are doing and
change or fix an issues you may be having.


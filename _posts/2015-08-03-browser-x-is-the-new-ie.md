---
layout: post
title: "Browser X is the new IE"
description: "Over the past few weeks there has been a hullabalou on the interwebs that started with the post from about Nolan Lawson about Safari being the new IE..."
category: Programming
tags: ["Browsers", "Chrome", "Safari", "Firefox"]
comments: true
---


Over the past few weeks there has been a hullabalou on the interwebs that started with the post from about Nolan Lawson
about [Safari being the new IE](http://nolanlawson.com/2015/06/30/safari-is-the-new-ie/), which had follow up posts like Benjamin De Cock's
[Chrome is the new IE](https://medium.com/@bdc/chrome-is-the-new-ie-1a21c1efc133) and a long rebuttal on the [Debug Podcast
](https://itunes.apple.com/us/podcast/69-melton-ray-on-safari-standards/id578812394?i=347349399&mt=2) where Don Melton's (one
of the original Safari engineers) arguments about why Safari is not the new IE sounded to my ears exactly the same
 as Microsoft in the early 2000 (for example he argued that Safari can't be updated as regularly as Chrome and Firefox because it is so 
tightly baked into the IOS platform and any unstability would damage IOS -- sounds a lot like the Microsoft grafting
IE into the Windows operating system for DOJ reasons in the early 2000's.  His argument that Apple was not spending as much time on
Safari because IOS and App's are the core of its business also seems remarkably familiar to IE's embrace, extend, eliminate practice
but I digress -- the point is that Apple has buckets of cash and they choose not to spend that much of it on working on 
Safari because it isn't in their best interest that the web is the best way to use a mobile device as 
App lock-in helps them retain their market -- not unlike the Microsoft of early 2000's).  I should also note
that Webkit was one of the greatest things to happen to the web, 3 years ago it the best browser on all platforms -- but 
unless you worked in industry in 1999 you would forget that IE5 was huge improvement over the bloated beast that Netscape
Navigator was at the time, and IE6 when it first came out was absolutely amazing. 

While I don't even know if I agree with most of Nolan's reasoning that Safari is the new IE, his main concern is about
Safari engineers not attending Edgeconf and other conferences and not being as open about their roadmaps as Chrome
and Mozilla is.  However the point that Safari only releases once a year is a huge deal, and while I may not absolutely
need IndexDB (another of Nolan's complaints) the state of ES6 support even in Safari 9 (as well as the sheer number of 
CSS features that are still left prefixed in Safari) does have them looking a lot like IE6 in the 2006 era.  When Firefox 
was innovating and IE6 was left unchanged for almost half of a decade.  They do update every year, but since Chrome and Firefox
release every 6 weeks (9 times more often), it does seem like a yearly update is a glacial pace for the modern web.  Safari
also decided a couple of years ago to completely re-imagine their Web Inspector (apparently to make it more similar to 
XCode - though why you would want to [emulate XCode](http://www.agingcoder.com/programming/2010/07/19/coding-like-its-1999/) I
have no idea) and now it is so painful to debug Safari on both Mac and IOS (maybe it is a case of [who moved my cheese](https://en.wikipedia.org/wiki/Who_Moved_My_Cheese%3F)
but there are so many key features missing from Web Inspector on Safari it is almost unusable).  And unfortunately I do
have to spend an unreasonable amount of time in Web Inspector these days because I find that when I go to look at sites I am working
on: they look fine in Chrome, I usually have to fix one or two things in Firefox, they surprisingly look fine in IE10+ (currently
I am lucky enough to be able to not have to support IE 9<) but I have to spend hours fixing Safari -- just like I had to with IE6
all those years ago when we designed things initially in Firefox.

As for De Cock's article about Chrome being the new IE, his argument is that by adding features so quickly to Chrome,
they haven't spent time optimizing and perfecting so that they perform so poorly that they are in effect, unusable.  And in 
a lot of ways, he is right, Chrome has become a bloated beast over the past few years.  I regularly look at my Task Manger
or chrome://memory-redirect/ and see Chrome eating up 5 gigs of memory (where the same number of tabs in Firefox will
be well under a Gig) -- and yes I know that Chrome will be much more well behaved if I didn't have a ton of memory but 
everyone who has run Chrome on a Macbook knows how it will [kill your battery](https://www.google.ca/search?q=chrome+macbook+battery+drain&oq=chrome+macbook+ba).
The sheer number of processes that Chrome launches (partially due to their one process per tab, but even with only 1 tab
open I will have a dozen Chrome processes running) is crazy -- and yes I may be at fault for having a dozen or so extensions
installed and running Google Drive and Hangouts but at some point the Chrome team will have to stop adding features and
do a major push on performance.  However, the best thing that Google has done is seperate the Chrome/Android browser from
Android and made even the web view upgradable, so eventually when Lollipop or better is on most of the Android devices
in the world (IOS is **much** better getting updates to user by the fact that it managed to wrangle control of updates
out of the hands of the carriers) we will not be forced to develop mobile sites based on what browsers 3 years ago could support.

Firefox is hardly perfect either, they did do a major push on performance and memory usage a few years back and it has
paid dividends, but having their [developer tools](http://getfirebug.com/) controlled by an outside volunteer development team
for so long unfortunately means that their current [developer tools](https://developer.mozilla.org/en/docs/Tools) 
which were started far too late in my opinion, are still years behind what Chrome has to offer 
(when they get Edit and Continue I will seriously consider switching to Firefox as 
my main developer platform, but until that day Chrome has me trapped in my [Cage with Golden Bars](https://en.wikipedia.org/wiki/Barfly_(film)).
Mozilla may also have spent too much time and manpower on [FirefoxOS](https://en.wikipedia.org/wiki/Firefox_OS) with though
may have been a noble effort, was probably a drain on some of the top resources at company that could have been working on more
important things.
  
So even though, in some ways, it is the best of times in Web Development: the tooling (from the Browser vendors as
well as Open Source and IDE's like Webstorm), the powerful new features that are being added (WebGL, Css animations, SVG,
Web Workers, IndexDB), the javascript language (ES6 and all of its goodness) are a potential boon to web development and we
will potentially see applications developed for browsers that would have been unimaginable before.  It iss also some of the most frustrating times
as a lot of the cool new things simply cannot be done with Polyfills or if they can be they are just too slow mobile browser
and though we get to play with them and imagine creative new uses for them, until they are all more prevalent we will be 
stuck with working with the best that 3 years ago has to offer.  





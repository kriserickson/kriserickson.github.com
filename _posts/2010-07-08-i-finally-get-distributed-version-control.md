---
layout: post
title: "I Finally Get Distributed Version Control"
description: ""
category: Programming
tags: [gihub, dcvs, duh]
---


I really haven't understood the whole distributed version control thing, and I still believe that for a non open source project,
it is probably overkill (unless you have a lot of people working on the project).   Having your own repository is great,
there are far too many times I hear about the fear of having a ton of uncommitted code due to the fact that it is in
some experimental phase and yet the programmer didn't feel that a branch or tag was worth the bother.
However my true epiphany came last night, as I was playing with [John Boxall's iBug](http://github.com/johnboxall/ibug)
(allowing some level of remote debugging on the iphone).

It was horribly broken due to the rapidly changing nature of [node.js](http://nodejs.org), so I spent 15 minutes or so
getting it working.   Normally that would be the end of it - oh I might have sent an email in the past to the author,
and a patchfile to fix their code but in something that appears to be abandoned like this I doubt anything would come of it.
But since the code was on [github](http://github.com), I just forked it and pushed my fixes to my fork.   Brilliant!
I can see this being a nightmare for popular projects, but for something nice and small like this it was a revelation.
And now there is a working version of [ibug](http://github.com/kriserickson/ibug) online,
and I can also add new functionality to it as I please!

---
layout: post
title: "Things I have learned in too many years of programming -- IDEs"
description: "When mentoring a new programmer I almost always try to force them to learn two things, Regular Expressions and VIM.  Although both are relics of a bi-gone era (I still think it is hilarious VIM popularity currently is, I expect EMACS t o swing back into vogue any day now). I still use each one every day, and save myself hundreds of hours a year simply because I can do things very quickly that take someone unfamiliar with those tools much longer.  I am pretty good at VIM, and pretty good a regular expressions (though definitely not a master in either), however I feel that people who develop in VIM or Sublime or any IDE or Editor that doesn't have constant static analysis is making life harder for themselves and overly relying on tests to do their typo checking for them.  Use an Editor for editing text and an IDE for programming."
category: Programming
tags: [programming, craftwork, professionalism]
---


# Things I have learned in too many years of programming#

As a little break from my continuing opus on the [State of Mobile Frameworks](/programming/2014/04/22/the-state-of-html-mobile-frameworks-in-2014/)
I've decided to write one of what may end up being a series of things that I have learned in my 20+ years of programming.

## IDEs##

##### **TLDR** - _IDEs make programming easier, if you are still using a text editor for programming seriously consider using a modern IDE._

When mentoring a new programmer I almost always try to force them to learn two things, Regular Expressions and VIM.  Although 
both are relics of a bi-gone era (I still think it is hilarious VIM popularity currently is, I expect EMACS t
o swing back into vogue any day now). I still use each one every day, and save myself hundreds of hours a year simply 
because I can do things very quickly that take someone unfamiliar with those tools much longer.  I am pretty good at 
VIM, and pretty good a regular expressions (though definitely not a master in either), however I feel
that people who develop in VIM or Sublime or any IDE or Editor that doesn't have constant static analysis is 
making life harder for themselves and overly relying on tests to do their typo checking for them.  Use an Editor for editing
text and an IDE for programming.

Static analysis built into the modern IDE is the greatest thing to happen to programming since unit tests.  I don't argue
that you should eschew Unit Tests because of static analysis, quite the contrary, but it is an excellent tool to add
to your arsenal that gives you immediate feedback rather than having to wait to run your unit tests.  And with IDEs
like IntelliJ[^IntelliJ] you can run static analysis against your entire codebase.  Of course there are other lint and more complex
static analysis but the easier they are to inline into your workflow the more you will use them.  I love the fact that
Intellij checks my code before I check it in, in fact one of my few complaints with IntelliJ is that I haven't found a
way to force it to run my unit tests before checking code in, something that has burned me on more occasions than I want
to admit.

Another feature that editors that don't have code insight[^insight] cannot do is refactoring: the ability of having 
the computer do my refactoring for me was almost magic 5 years ago, now if refactoring isn't available I can't take an IDE seriously.
I remember the hell of refactoring in the Visual Studio 2003 days and even in VB6 and refactoring through search and replace
basically made it impossible to refactor functions that were given a common name, as you would have so many false positives
when you were doing your global search and replace that the refactor was basically doomed.  You prayed that the compile
step caught all of your errors, but if it didn't you basically had days of pain trying to find all the subtle bugs in your
code.  And that was for strongly typed languages that compiled, in a modern scripting language unless you have 100% code
coverage in your unit tests, refactoring without tools you completely trust can lead to very subtle bugs.  

When 6 or 7 years ago when I finally got an IDE with semi-decent static analysis built in (Zend Studio 5 or something)
I ended up finding a ton typo bugs that I know where leading to tons of subtle errors in production.  I am
sure they were all sitting there in the PHP_ERROR log with the 5 million other "Undefined variable" and "Undefined Index"
messages, its just that when you have an old codebase with half a million lines of code these things frequently only 
get discovered when there is a reproducible error that affects the Business Unit. But enough of that digression, I was
speaking of the value of IDEs.

Your IDE should be at least as powerful as your text editor, and if it doesn't do things like Macro Recording, or have ways
to extend its functionality you should look elsewhere.  It should also not get in the way, if it is too slow, or constantly
have windows popping up asking you to do things it will cause distraction, and distraction is killer of productivity when
programming.  You should easily be able to do any action with a keystroke (or a combination of keystrokes) but also
be able to easily discover those keystrokes (the days of 5 page IDE cheat sheets should be a thing of the past) as well
as finding the action through search (menus are fine yes, but having a way to simply search for a command is faster since
you don't have to use the mouse).  The last thing is that your editor should be fast, if it hangs every 5 minutes or so
because it is busy doing a task and you can't type, then you again will become distracted, and start doing other things.
I believe that this is the primary reason for the switch away from IDEs to editors and with the power of even the cheapest
laptop these days that should not be an issue.

One more thing, I know I said speed was the last thing, but autosave with a history is something that I have become
so reliant on that now when I use an editor or IDE that isn't saving all the time, I find I frequently find myself
wondering if it is a browser caching problem that isn't causing the page to update rather than the fact I forgot to hit
save in the editor.  And having a history that is not tied to version control is a life saver, which allows you to 
quickly charge down a line of thought, willy-nilly deleting (rather than commenting out) lines of code knowing that
if your quick little experiment doesn't work out you can always get back to a good state in a matter of seconds.  I know
that this is one of the advantages of Git, but having it baked into an IDE without having to remember to Git commit before
going down that path is one of my favorite features about IntelliJ.

In the future this will hopefully all be delivered without having to have an actual IDE installed on your system.  Cloud 
IDEs are the future, however we are so far from them those IDEs being at a state where they compete with a real IDE.  OK,
so far may only be a couple of years given the rapid improvement of the Cloud IDEs in the past couple
of years, but the Cloud IDEs are missing almost all of the features I have mentioned above.  They are fine for updating
a few lines of code and fixing a simple bug, but to be stuck writing a whole application in them would be troublesome (plus
even though I trust things like Google Docs not to lose anything I have typed, there is something about code that I find
more valuable and so I have an unfounded yet innate fear that one of these IDEs would lose some of my precious lines of code).
One day I will be happy when I don't have to install and keep up to date a few IDEs on my systems, and that all my
development VMs will be running on a cloud somewhere with an awesome Cloud IDE as the frontend, and I can easily edit
and code from anywhere on any device.  No more Yak Shaving getting environments to work, select your language and your
framework from a set of dropdowns (or if you are so inspired start with a blank linux VM) and things just work.  No need
to setup Php or Node or Ruby or whatever with Nginx or Apache or whatever you prefer.  No need to spend hours twiddling
the XDebug setting and your firewall to get debugging to work.  I have spent far too many hours Yak Shaving getting 
Vagrant VMs that 95% work to do that last 5% to begrudge whatever anyone one would charge for this magical new world of 
development.

My very last thought on the world of IDEs is why I spend so much time breaking all of the above requirements for an 
a Development Environment (I hestiate to call it an IDE as it isn't quite yet) that is barely better than a text editor,
I am of course speaking of the Chrome Developer Tools (herein called the Dev Tools).  I frequently find myself cursing 
that I didn't go back to PHPStorm to check the syntax of something I have typed into the Dev Tools only to notice
that PHPStorm spotted the obvious error.  However the ability to do Edit and Continue in Javascript is so compelling
that I willing to put up with all of the annoyances of the Dev Tool just for that one killer feature.  It is the one
thing that I miss the most from working in Visual Studio, and one of the reasons when working in C# I shunned some of
the best new features of C# (Linq and Lambdas) because any function that had an anonymous function in it didn't support
Edit and Continue.  This is why I had such high hopes for [Light Table](http://www.lighttable.com/) inspired by 
[Bret Victor's Inventing on Principle Talk](https://www.youtube.com/watch?v=PUv66718DII), although from the last
time I checked it out (which I do admit was a while ago) none of the promise of the original Bret Victor talk had
really been fulfilled.  It's also why I might spend a little time checking out (Swift)[https://developer.apple.com/swift/], 
as the language has little interest for me in that it is close sourced, the Playground may be interesting enough to 
spend some time in it.  Though I find it hard to believe that Apple which creates an IDE as developer hostile as
XCode could make Playground something that would delight me, but here is hoping (in cause I wasn't clear I haven't
spent any time with Playground and am going by the description of other and the WWDC keynote). And hopefully if Playground 
becomes popular, some of the features of that original Bret Victor talk may come to the Dev Tools and other IDEs.

Enough of IDEs already, I have rambled on too long, however if I have done one thing, hopefully it is to convince
you if you are programming in a text editor to give a good IDE (i.e. Not Eclipse or XCode) a chance.


[^IntelliJ]: When I say IntelliJ note that I mean the entire JetBrains IDE lineup, whether it is PHPStorm/WebStore, RubyMine, PyCharm, AppCode, Android Studio, it is all based on the same codebase with features added or removed depending on the SKU.

[^insight]: By code insight I mean that the IDE has built a syntax tree (AST) and has a lexical understanding of the code so that it knows what functions are referenced when you rename a function.
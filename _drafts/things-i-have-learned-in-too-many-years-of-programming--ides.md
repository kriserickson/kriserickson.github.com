---
layout: post
title: "Things I have learned in too many years of programming  IDEs"
description: ""
category: "Programming"
tags: [programming, craftwork, professionalism]
---
{% include JB/setup %}

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
like IntelliJ[^Intellij] you can run static analysis against your entire codebase.  Of course there are other lint and more complex
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
to extend its functionality you should look elsewhere.  It should also 

[^IntelliJ]: When I say IntelliJ note that I mean the entire JetBrains IDE lineup, whether it is PHPStorm/WebStore, RubyMine,
PyCharm, AppCode, Android Studio, it is all based on the same codebase with features added or removed depending on the SKU.

[^insight]: By code insight I mean that the IDE has built a syntax tree (AST) and has a lexical understanding of the code
so that it knows what functions are referenced when you rename a function.
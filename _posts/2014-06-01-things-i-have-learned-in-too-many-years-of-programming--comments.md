---
layout: post
title: "Things I have learned in too many years of programming -- Comments"
description: "When I first started programming, I tried to write the most compact, cleverest blocks of code which I would dutifully comment to explain what they where doing.  These comments where odes to my brilliance and what a clever way I had solved this problem rather ..."
category: Programming
tags: [programming, craftwork, professionalism]
---


# Things I have learned in too many years of programming #

As a little break from my continuing opus on the [State of Mobile Frameworks](/programming/2014/04/22/the-state-of-html-mobile-frameworks-in-2014/)
I've decided to write one of what may end up being a series of things that I have learned in my 20+
years of programming.

## Comments ##

##### **TLDR** - _Comments are good, comments are bad, clarity is good, clarity is hard, moderation in all things._

When I first started programming, I tried to write the most compact, cleverest blocks of code which I would
dutifully comment to explain what they where doing.  These comments where odes to my brilliance and what a
clever way I had solved this problem rather than a succinct description of what was going on.  As time wore
on the comments grew shorter (though as I fell more confident with my programming abilities these comments
morphed over time to become a little less of bragg and more descriptive).

Somewhere around 10 years ago I started to believe that comments where not necessary (this was not something
I came upon by myself, but something I pulled out of various blogs and reading of the time).  Code should be
written so well that it doesn't require a comment.  Clarity over cleverness become my new mantra.  The truisms
spoken by the anti-comment spoke to me: comments are frequently out date and explain what used to happen.  Code
gets updated but comments don't.   Comments are often poorly written and confuse the matter as much as the code does.
People often add comments to add comments and they serve no purpose (everyone who programs for a while has seen
something like this:

{% highlight javascript %}
// creates new date
var firstUpdated = new Date();
{% endhighlight %}

or

{% highlight javascript %}
if (generateNewDate) {
    lastUpdated = new Date();
} // end if
{% endhighlight %}

During this period of time I would spend hours expunging useless comments from our company codebase, especially
the <code class="noblock">// end if</code>, <code class="noblock">// end while</code> variates (this is what indentation is for people!, and
if it is a truly long block that you wish to delineate, move it to a function or at least add the conditional in
the end comment!).

My new mantra was **"No comments!"** and I would argue to anyone who would listen that if your code needed comments
you were doing it wrong.  Make variables more descriptive, break functions into multiple functions where the name
of the function would simply explain what you where doing.  No function should be more than 10 lines.  No function should
have more than one return point, etc.

Of course I frequently found myself cheating to make functions shorter, I have always loved the ternary ? operator and
frequently abuse it (though now I never let myself use more than one on a line, I distinctly remember refcotoring a statement
once that had 4 of them.  I had sacrificed line count for readability, and fighting style metrics (too many lines) with
something approaching obfuscation level programming.

Eventually I realized, that like all things in life, the best strategy is moderation.  If you have a function that has 15 or 20 lines,
don't sacrifice readability and break it into 5 functions just to keep the 10 line function rule.  I still use the ternary
operator, and still believe that I shouldn't have to comment a simple regex.  But I have realized that I am simply not a good
enough programmer to program without comments.
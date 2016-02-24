---
layout: post
title: "The Angular 2.0 Hullabaloo"
description: "Ever since ng-europe last month, people have been freaking out about Angular 2.0, initially I had written up some thoughts about this in the days following, but I decided to wait a while for things to settle down before writing about this.  I am hardly an Angular expert, and though I do use it both at work and also in pet projects I wondered really how much I had to add to the discussion." 
category: Programming
tags: [Javascript, Controversy]
---


Ever since [ng-europe](http://ngeurope.org/) last month, people have been freaking out about Angular 2.0, initially
I had written up some thoughts about this in the days following, but I decided to wait a while for things to settle
down before writing about this.  I am hardly an Angular expert, and though I do use it both at work and also in
pet projects I wondered really how much I had to add to the discussion.  

**Freak Out -- The Sky Is Falling -- The Angular Developers Hate Us**

<img src="/img/angular2/haironfire.gif" style="float:left; border: 1px solid #000; margin: 0 10px 10px 0">

Even though  Google claims to have over [1600 sites (internal and external) running Angular](http://devchat.tv/adventures-in-angular/016-aia-ng-1-3-and-2-0-with-brad-green-igor-minar-and-mi-ko-hevery)
they have very few high profile sites running on it.  Their commitment to creating a framework that can be maintained over
years does not appear to spring from their internal usage of the framework in a any high profile applications.  
The maintainers of Angular appear to pretty well have been given free reign by their bosses at Google to completely
re-imagine the framework from the ground up, be damned whether or not it will force a complete re-write off all
projects that are using it.  Heck they have even created a [new language](https://docs.google.com/document/d/11YUzC-1d0V1-Q3V0fQ7KSit97HnZoKVygDxpWzEYW0U/edit)
for building your applications in, as well as changing basically everything about Angular (dropping $scope,
directives, modules, controllers) so that it will be a completely different animal from Angular 1.x.  The other bomb
they dropped is that Angular 1.3 would be supported from 18 Months after Angular 2.0 was released.
  
Of course everyone who has spent the past three years learning the intricacies of $scope, and how to write effective
directives and have create a giant codebase of Angular apps started freaking out.  If you work at a company were codebases
last years or decades and are evolved over time being told that pretty well everything you have written in Angular will
have to be completely rewritten if you want to stay with the latest release is not welcome news.  There has been
nebulous talk about some kind of migration strategy but always preceded by stating that until the Angular 2.0 has
been codified it is too early to talk about how it would work.  I remember the migration strategy from VB6 to VB.Net
(which I think would be similar in scope to the kind of changes proposed for Angular 2.0) and it was basically
useless to the point where there are still [companies](http://www.artinsoft.com/) 15 years later whose only job is to 
convert VB6 applications, and it is still a nightmarish task.  
 
These kind of changes have happened in past many times, and they frequently end up with two versions that kept in 
development for perpetuity (the classic example is Python where Python 3 was released over 6 years ago, and Python 2 is still 
the most widely used version of Python).  Sometimes it is successful and the new version quickly overtakes the old
version (Symfony 2 was adopted rather quickly and it had some fairly major changes), but if you look at examples in 
Javascript space where major changes have been made the new library adoption has not been fast.  ExtJS, for example,
is now at version 5 (as of June 2014) and the most commonly used version (63% of the sites that use it) are two versions
back at version 3 [according the w3techs](http://w3techs.com/technologies/details/js-extjs/all/all). 
 
And we know that Google doesn't have a track of supporting things it feels is no longer in its best interest:
shutting down [Reader](http://www.google.com/reader/about/) and [Google Wave](https://support.google.com/answer/1083134?hl=en) 
(does anyone else think that if Google had given Wave a little longer while to develop they could have had a serious 
[HipChat](https://www.hipchat.com/) or [Slack](https://slack.com/) competitor?) when 
[they no longer have interest in them](http://www.makeuseof.com/tag/top-ten-dead-google-projects-floating-cyberspace/).  
If it isn't in Google's best interest you can be sure
that support for Angular will have to come from the community, and now that they are  focusing on polymer they may not 
be so intent on making Angular the premier JavaScript framework.

The other problem with ask these changes is the FUD problem.  While this is not being did being directed by 
Angular's competitors, the lack of a clear migration path and the uncertain future of the Angular 1.x may lead companies 
and even developers to look at more stable frameworks for their JavaScript needs.  I was interviewing interns over the 
past couple of weeks and though they all expressed an interest in Angular and especially the MEAN stack, every 
single one of them mentioned their concerns with what was happening with Angular 2.  If the future JavaScript developers 
jump ship to Ember or React it doesn't matter if Angular 2 is perfect and there is a simple upgrade path because 
there will be so few developers still using Angular.

Right now Angular is the 500 lb Gorilla because of its massive user bar and it's inevitability, of it losers that it 
will lose one of its greatest assets.  

**Calm The F*ck Down -- Nothing Is Set In Stone -- There Will Be A Migration Plan**

<img src="/img/angular2/calm-down.jpg" style="float:left; border: 1px solid #000; margin: 0 10px 10px 0">


First of all, people overreact, developers doubly so.  Criticize a developers favorite editor or IDE if you ever want to 
see this effect in action.  Move someones cheese and watch the freak-outs happen, so it cane as no surprise that when 
people finally realized that Angular 2 was going to be drastically different there was going to be s reaction.  
Though the lead developers had been [dropping](http://angularjs.blogspot.ca/2014/03/angular-20.html) 
[hints](http://www.johnpapa.net/whats-coming-in-angularjs-2-0/) about major changes months but the scope of the change
was never 100% clear until ng-europe and the new syntax was demoed on [screen](https://www.youtube.com/watch?v=gNmWybAyBHI).  
Part of the problem was the fact that there hadn't been much transparency or consultation of what the users of 
angular wanted (and no, that isn't the responsibility of the developers of an open source project but if they want 
to retain said users they should probably keep that thought in mind).  The other problem is a lot of users felt 
that the Angular developers where basically architecture astronauts searching for a more elegant solution where most 
people were happy with Angular's approach.  

Of course the truth is always more complicated, and because of the internet freakout the angular developers have 
kind of jumped into crisis management mode writing blog [posts](http://eisenbergeffect.bluespire.com/all-about-angular-2-0/)  
and appearing on [podcasts][http://devchat.tv/adventures-in-angular/016-aia-ng-1-3-and-2-0-with-brad-green-igor-minar-and-mi-ko-hevery] to explain exactly 
what is going on.   Part of the changes are because even though it has Angular has sprung to popularity in the past
couple of years, it was initially written 5 years ago when the state of web technologies was different and to include
modern and upcoming features like [Shadow Dom](http://www.html5rocks.com/en/tutorials/webcomponents/shadowdom/), 
[Object Observe](http://www.html5rocks.com/en/tutorials/es7/observe/), and 
[Web Components](http://www.html5rocks.com/en/tutorials/webcomponents/customelements/) things under the hood have
to change in fairly major ways.  However, one would think that these new technologies could be implimented in ways
that don't require a complete change of the way Angular is written (although in various places the architects
behind Angular claim that it was necessary to change the way attributes are notated to get web components to work).

It is important to remember that Angular 2 is in the design process, and undoubtedly will change before the final
version is released.  The developers have promised that when they get closer to release there will be some kind
of a migration story.  And the backlash has been intense so plans for what Angular 2 will be might change or 
they might change the lifespan of Angular 1.x and continue it longer than the original 18 months earlier stated.  In
fact, my guess is the appearance of the [AngularJS 1.4 Planning](https://docs.google.com/document/d/13UG5sdi9paJdr_NvZ3IqxGnjkQvqJe1GGkQTXdfbnIk)
guide and the fact that appears to be a version 1.4 upcoming is a sign that the developers are listening.

**Conclusion** 

The griping about Angular 2.0 and the way it was quietly developed in isolation is certainly grounded (I mostly agree with
John Petersen's conclusions in his blog post [How Google broke the OSS compact with Angular 2.0](http://codebetter.com/johnvpetersen/2014/10/27/how-google-broke-the-oss-compact-with-angular-2-0/)).  It certainly seems like
the people chosen to run the Angular project could learn a lot from some of the more mature projects in the space.  
jQuery, for example, telegraphs their intentions for major changes years in advance and deprecates features very slowly
and even includes compatibility plugins (with deprecation notices so that you can find and update your code) when they
finally do remove a feature (and even then people get [frustrated](http://stackoverflow.com/questions/14891412/jquery-live-is-deprecated-well-okay-but-is-not-replaced)).
  
I am still on the Angular bandwagon, but when people ask me now whether it is still worth learning Angular or should 
they learn [React](http://facebook.github.io/react/) or [Ember](http://emberjs.com/) or wait for Angular 2 I am 
less emphatic in my "of course learn Angular refrain from the past".  Now I would definitely say try a bit of 
each and pick the one you like best after a few hours with each framework, and if you do pick Angular definately use
the Controller as abstraction.  And to the developers of Angular I would say that there is lots about Angular that can be 
improved without changing everything rewriting the framework (at least keep working on the 1.x branch until a 
majority of the [750+ issues](https://github.com/angular/angular.js/issues) are closed.  





 
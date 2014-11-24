---
layout: post
title: "The Angular 2.0 Hullabaloo"
description: ""
category: Programming
tags: [Javascript, Controversy]
---
{% include JB/setup %}

Ever since [ng-europe](http://ngeurope.org/) last month, people have been freaking out about Angular 2.0, initially
I had written up some thoughts about this in the days following, but I decided to wait a while for things to settle
down before writing about this.  I am hardly an Angular expert, and though I do use it both at work and also in
pet projects I wondered really how much I had to add to the discussion.  

**Freak Out -- The Sky Is Falling -- The Angular Developers Hate Us**

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
development for perpetuity (look at Python 3 that was released over 6 years ago and Python 2 is still the main branch
of Python).  PHP4 survived for years after PHP5 was released, and the changes required to migrate code there was minimal.



**Calm The F*ck Down -- Nothing Is Set In Stone -- There Will Be A Migration Plan**

First of all, 
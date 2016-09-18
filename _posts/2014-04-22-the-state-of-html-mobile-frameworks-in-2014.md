---
layout: post
title: "The State of HTML Mobile Frameworks in 2014"
description: "A year I released my mobile app Recipe Folder using jQuery mobile and PhoneGap.  While jQuery mobile
did the job, I realized that while easy to get started with, jQuery Mobile is fairly bloated and the upgrade cycle was taking
days of work rather than just dropping in the new files.  I figured that there had to be a better solution, and I researched
the various other HTML5 Mobile platforms when I had to create a mobile application for work. My directives was to find a
framework ..."
category: Programming
tags: [Mobile,Programming,Phonegap,Cordova,HTML5]
featured: true
---
This is part 1 of a multipart series.  There will be more parts forthcoming.

A year I released my mobile app [Recipe Folder](http://recipe-folder.com) using jQuery mobile and PhoneGap.  While jQuery mobile
did the job, I realized that while easy to get started with, jQuery Mobile is fairly bloated and the upgrade cycle was taking
days of work rather than just dropping in the new files.  I figured that there had to be a better solution, and I researched
the various other HTML5 Mobile platforms when I had to create a mobile application for work.  My directives was to find a
framework as simple as jQuery Mobile or jQTouch that looked modern and very extensible with a relatively simple codebase
that we could alter the behavior and yet not be left behind as it was updated.  Also the end result would be an application
running on Phonegap, not a web page so a framework that felt as native as possible was required.

Unfortunately I was left with the decision that there really wasn't anything out there that was fulfilled all those
goals, so I ended up creating [TopcoatTouch](http://topcoattouch.com), so full disclosure, I may be a little
biased.  However, I thought it might be useful to share the research I performed when I decided that I absolutely
needed a new framework.

First, I personally have issues with giant frameworks, I have been burned by them before
and I hope to never be burned by them again.  For me a giant framework is an impenetrable framework, or at least
it takes a huge amount of effort to discover what the framework is doing under the hood.  With all mobile
frameworks I have used in the past I have had to slightly modify the way things work (messing with the backstack
for example, the need to go back two pages not one without having an animation).  And if I have to actually change
the framework to accomplish this, and the next version of the framework changes said backstack handling, or the code
is so different that repatching my fix takes days not minutes, I will get frustrated (I am looking at you jQuery Mobile).
So, framework size is one of the factors I look at, not due to the load of the mobile device (though in the past this
may have been an issue, I seriously doubt that it will be for much longer).

Another thing I looked at was when queries about the framework peaked on Google.  I know, that you don't always want
the new hotness, but if there is very little interest in a framework then it won't get much development love.  The only
framework that I really dismissed for this reason was jQTouch and I have kind of dismissed it for other reasons as, mostly
it is looking very long in the tooth now.

Also I looked at how many questions the framework had on stack overflow, I find that technologies with active communities
on Stackoverflow will be products that are easier to get support for.

The last thing I included in this table is the license, which may affect your decision.  I would have had no problem
going with a commercial license for a work project, though for side projects I was doing on my own I would probably
avoid anything commerical.

The chart below is an updated version of what I produced:


<style>
table {
    margin: 0 auto 20px auto;
    max-width: 56.25rem;
}

</style>
|Framework   | License   | Peak Interest  | StackOverflow Questions | Lines of Code (Sloc)  |
|---|---|---|---|---|
|[jQT](http://jqtjs.com/)   | MIT  | [August 2010](https://www.google.ca/trends/explore#q=jqtouch%2C%20jqt&cmpt=q)  | 469  | 681 |
|[jQueryMobile](http://jquerymobile.com/)  | MIT  | [October 2012](https://www.google.ca/trends/explore#q=jQueryMobile)  | 18,024  | 10,222  |
|[Bootstrap](http://getbootstrap.com)   | MIT | [July 2013](https://www.google.ca/trends/explore#q=twitter%20bootstrap)  | 1,087 (I was suprised too)   | 1256  |
|[KendoUI Mobile](http://www.telerik.com/kendo-ui)  | Apache2 / Commercial  | [November 2013](https://www.google.ca/trends/explore#q=KendoUI)  | 5,798  | 34,523  |
|[Ionic](http://ionicframework.com/)   | MIT  | [April 2014](https://www.google.ca/trends/explore#q=Ionic%20framework)  | 82 | 4,199  |
|[Onsen-UI](http://onsenui.io/) | Apache2 | No Result | 5 | 4,762 |
|[Sencha-Touch](http://www.sencha.com/products/touch/)   | GPL3 / Commercial  | [March 2012](https://www.google.ca/trends/explore#q=sencha%20touch)   | 3,961 (15,128 for ExtJs)  | 8,706  |
|[Jo](http://joapp.com/)   | OpenSource / Snowflake*  | [August 2012](https://www.google.ca/trends/explore#q=jo%20mobile)  | 0  | 3,975  |
|[PhoneJS](http://phonejs.devexpress.com/)   | Commercial  | [April 2014](https://www.google.ca/trends/explore#q=phonejs)  | 58  | 23,203  |
|[ChoclateChip-UI](http://chocolatechip-ui.com/)   | MIT / Commercial  | No Results | 5  | 2,007  |
|[AppFramework](http://app-framework-software.intel.com/)   | MIT / X11  | [March 2012](https://www.google.ca/trends/explore#q=AppFramework%2C%20jqmobi&cmpt=q)   | 67  | 1,764  |
|[TopcoatTouch](http://topcoattouch.com)   | MIT  | No Results  | 0 (13 for Topcoat)  | 884 |

A few quick things to note, when I intially did the overview I was unaware of both Ionic and Onsen-UI.  I believe that
Ionic may have been out when I did the original research but certainly had no noticable online presence, Onsen appeared
a little later.  I have added them to the list because I feel that they are definately worth looking at for anyone who
is evaluating mobile frameworks, and because [Angular](https://angularjs.org/) is awesome and starting to look like
a reasonable way to go for mobile.

The next table I came up with was a list of Reliant technologies, Ease of learning the platform, and the supported platforms.

The reliant technologies are all pretty unimportant, I think that jQuery, Angular, and even jQueryUI are very solid
technologies that you aren't going to have any issues with.  In fact, I think that frameworks like ChoclateChipUI that
uses it's own Selector framework you may have issues with it not working the way you have come to expect jQuery to work (assuming
you are used to working with jQuery).

Ease of Learning is obviously subjective, if you are already familiar with Angular then Ionic and Onsen-UI are going
to be a lot easier to pickup than if you don't know angular.  Sencha has pretty steep learning curve, and I felt that
Jo was also a bit of a strange one so I rated it's ease of learning fairly high.  The frameworks that follow the
create screens in HTML, and use jQuery to control them I assumed would have the most familarity to my readers so I rated
them the easiest to learn.

The supported platforms comes from the sites, and I certainly haven't tested the platforms on anything other than IOS and Android (and
the Chrome browser).  Some of the frameworks that don't state support for WinPhone or Blackberry may work perfectly
well on those platforms, but since their site doesn't tout support of that platform I didn't add it.

|Framework   | Reliant Technologies  | Ease of Learning  | Supported Platforms  |
|---|---|---|---|---|
|[jQT](http://jqtjs.com/)   | [jQuery](http://jquery.com) | 1 | IOS / Android |
|[jQueryMobile](http://jquerymobile.com/)  | [jQuery](http://jquery.com), [jQueryUI](http://jqueryui.com)  | 1  | IOS  / Android / WinPhone / Blackberry / Meego / Tizen / Bada / Opera Mobile / Desktop Browsers |
|[Bootstrap](http://getbootstrap.com)   | [jQuery](http://jquery.com) | 1 | IOS  / Android / WinPhone / Blackberry / Meego / Tizen / Bada / Opera Mobile / Desktop Browsers |
|[KendoUI Mobile](http://www.telerik.com/kendo-ui)  | [jQuery](http://jquery.com) | 2  | IOS / Android / WinPhone |
|[Ionic](http://ionicframework.com/)   | [Angular](http://angularjs.org)  | 3 | IOS / Android |
|[Onsen-UI](http://onsenui.io/) | [Angular](http://angularjs.org) | 3 | IOS / Android |
|[Sencha-Touch](http://www.sencha.com/products/touch/)   | None (but built on ExtJS) | 5 | IOS / Android |
|[Jo](http://joapp.com/)   | None! | 4 | IOS, Android, Windows 8, BlackBerry 10, Tizen, Chrome OS  |
|[PhoneJS](http://phonejs.devexpress.com/)   | [jQuery](http://jquery.com), ([Knockout](http://knockoutjs.com/)) |  3 | IOS, Android, WinPhone, Tizen |
|[ChoclateChip-UI](http://chocolatechip-ui.com/)   | None | 2  | IOS, Android / WinPhone |
|[AppFramework](http://app-framework-software.intel.com/)   | None | 2 | IOS  / Android / WinPhone / Blackberry |
|[TopcoatTouch](http://topcoattouch.com)   | [jQuery](http://jquery.com), ([iScroll](http://iscrolljs.com/), [Hammer.js](http://eightmedia.github.io/hammer.js), [lodash](http://lodash.com/), [fastclick](https://github.com/ftlabs/fastclick)) | 1 <nobr>(MVC style 3)</nobr> | IOS / Android |


Over the next few articles are going to look at the various frameworks and do a quick skim over the advantages and disadvantages
of each based on my use of each platform (though I will freely admit that I only have surface knowledge of most of these
platforms).

I ignored a couple of neat little frameworks, [Fries](http://getfri.es/), which is an Android skin and [Ratchet](http://goratchet.com/)
as they are specifically designed for prototyping and not for building apps (though Ratchet appears to be moving more
towards being a framework).

When comparing the frameworks for yourself, one of the best resources I found for comparing these platforms is the [PropertyCross](http://propertycross.com/) website,
which gives a very good idea of what the resulting app will look like (and source code) for almost all of these platforms.  I highly
recommend it (it also has native cross browser frameworks like [Xamarin](https://xamarin.com/) if yuu are actively comparing native
and hi-brid solutions.

Until next time,

Stay mobile!

Next up [jQT](/programming/2014/04/24/mobile-frameworks-jqt/)


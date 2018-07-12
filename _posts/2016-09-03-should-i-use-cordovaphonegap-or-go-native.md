---
layout: post
title: "Should I use Cordova / Phonegap or go Native?"
description: ""
category: Programming
imagefeature: blog/direction.jpg
tags: [Mobile,Phonegap,Cordova,Native,Programming]
featured: true
---

### Cordova or Native?

The number one question I get asked, both by as a consultant and in the emails I get from readers of this blog is

"Should I use Phonegap or write a native app"

*Side note: when asked this question people almost always refer to Cordova as Phonegap, however I usually refer to it as
Cordova as that is the name of the Open Source project, rather than PhoneGap which is the Adobe branded distribution
of Cordova*

And my answer is always: it depends.  For us pragmatists it is a similar question to "What is the best programming language?"
And it depends on even more than the type of App you are planning on creating, it depends on where you want that app
to go, what features the app requires, what development talent you have available to you, what platforms you want to target,
and the list goes on.    

When I am asked if you can build it in Cordova, the answer 90% of the time is yes, you can build it Cordova.  
However, sometimes, building certain types of Apps in Cordova would require so much work will be spent on 
plugins and optimizing the HTML that it may not necessarily the most optimal choice of a platform.  

Initially I had sketched out a flowchart that gave some guidance as to whether or not you should
develop a native app or a hybrid/Cordova app, however it oversimplified things and did not properly factor a great many
things into the decision.

My new answer is more like the classic decision tool where you write down the plus and minuses of each aspect of a decision,
except I recommend you create two columns (Native and Cordova )and give points to either Native or Cordova depending upon the
answers to following questions.  You may decide to change the weights I have awarded to each question, and I may have
missed several factors that may affect the decision, please feel free to make suggestions in the comments below.

#### Number of Platforms to Support

If you only have one platform to support (for example you are building an app for a company that will supply the 
devices that the App is deployed on to their users), award 5 points for Native.  If you plan to launch iOS only for
the near term (but eventually will launch on Android or another platform) are 2 points for Native.  If you have to
launch on 2 platforms award 2 points for Cordova, if you have to launch on 3 platforms award 5 points to cordova, 
if you have to launch on 4+ platforms award 7 points to Cordova (and cry a lot, since you are going to be in an 
unenviable situation).

#### Making A Game

If you are making a game that has any level of sophisticated graphical requirements, award 5 points to Native.  You can
do graphics, and you can certainly make puzzle style games in HTML and Javascript, but if you want to squeeze everything
out of a mobile device you really want to get as close to the metal as possible and that generally means coding in C.
This may be changing as the old Android Browser is becoming a thing off the past, the old Android browser was removed in
Android KitKat 4.4.3 and replaced with the Chrome view, however it wasn't until Lollipop (5.0) that it became an evergreen 
(i.e. always updating) browser.  

#### Native Feel

There are two philosophies when designing mobile apps, one is to make the App look like they completely belong on the
platform.  Follow the platform design guidelines as closely as possible so that users familiar with ecosystem will
feel as comfortable as possible in the application.  Use the conventions of the platform to easily expose functionality,
hoping the user will intuit how to use your app because they know the platform.  Gmail is a good example of this,
where Gmail on iOS looks like an iOS app and Gmail on Android looks like an Android App:

<div style="text-align: center; margin-bottom: 20px">
    <span style="vertical-align:top; display: inline-block">
    <div>
        <img src="/img/cordova-or-native/gmail-ios.png" style="border: 1px solid #000; margin: 0 10px 10px 0">
    </div>
    <span class="figure">Gmail on iOS</span>
    </span>
    <span style="vertical-align:top; display: inline-block">     
    <div>
        <img src="/img/cordova-or-native/gmail-android.png" style="border: 1px solid #000; margin: 0 10px 10px 0" >
    </div>
    <span class="figure">Gmail on Android</span>
    </span>
</div>          

If you app falls into this category, where you want to follow the platforms design guidelines and functionality as
 much as possible, award 5 points to Native.

Then there is the design philosophy that our App is our own.  We should have a common look and feel across platforms
for our App, and that our brand and our app is more important than the platform we are running on.  Instagram is a good
 example of this:
  
  <div style="text-align: center; margin-bottom: 20px">
      <span style="vertical-align:top; display: inline-block">
      <div>
          <img src="/img/cordova-or-native/instagram-ios.png" style="border: 1px solid #000; margin: 0 10px 10px 0">
      </div>
      <span class="figure">Instagram on iOS</span>
      </span>
      <span style="vertical-align:top; display: inline-block">     
      <div>
          <img src="/img/cordova-or-native/instagram-android.png" style="border: 1px solid #000; margin: 0 10px 10px 0" >
      </div>
      <span class="figure">Instagram on Android</span>
      </span>
  </div>
  
If you want your app to not mimic the features of the underlying OS, and have its own look and feel, award 3 points to Cordova.
  
#### Development Experience
  
The experience your developers have will heavily factor into your decision.  If you are sub-contracting you might need
to adjust this scale to somehow factor in the cost of sub-contractors (native iOS and Android developers unfairly or not
usually charge more than Cordova developers).  I have no simple scale for this question, except maybe I would say add
2 points to Cordova for every developer who is an experienced web developer on your team, add 5 points to Cordova for
experienced Cordova developer and add 5 points to Native for experienced iOS or Android developer and subtract 5 points
from Native if you are missing a developer for that platform (i.e. if you have an experienced iOS developer, but no
experienced Android developer and you are shipping to both platforms then add 0 points since it is a wash).  Feel free to
adjust the number of points awarded to each side based on the level of experience on the various platforms.

#### Speed to Delivery

Everyone needs everything fast, but from experience I believe that you can create Cordova app faster than a native App,
in the end the maintenance will probably similar (and long term developers know that most of the lifecycle of a 
long-term successful app is maintenance) but it will be faster to develop a Cordova app (even if it is only for one platform,
double true if it is for multiple platforms) than Native Apps.  Add 3 points to Cordova if speed of initial delivery is
more important than the upkeep up the application.

#### OS Features Required

As a reader of this blog, you probably know what Cordova does best, and you probably know all of the built in features that
it has available to it (battery, camera, content-sync, dialogs, file, in-app-browser, media, vibration, network).  These plugins are 
all pretty battle tested and reliable ([though not 100% reliable](/phonegap/2016/03/20/phonegap-be-wary-of-plugins/)),
however as soon as you need other functionality you may want to start removing points from Cordova.  If there is a popular
plugin available you may be in luck, but look at the plugin very carefully.  Here are some things to look for:

1) Is it frequently updated, though this is not 100% guaranteed to be show stopper, the plugin may be perfect and
just "work", it is rare that mobile plugin will not have to be updated.  Apple deprecates functions all the time (just
look at the "official" plugins when you compile in XCode or Android studio and see how many deprecation warnings there are),
and if a plugin has been abandoned you may be taking on more work than you bargained for.  Frequently plugins are written
for apps and then when the app gets abandoned, so does the plugin.  It may work perfectly, or may just need some fixes, or 
may take weeks of your time getting it to work.

2) Is there are lot of users of the plugin.  Look at the stars and forks on GitHub, the number of contributors, but also
look at the number of downloads it gets on the [npm registry](https://www.npmjs.com/).  For example the cordova sanctioned 
plugins will get 4000-5000 downloads a day, whereas a popular plugin like the facebook plugin will get 500 downloads a day.

3) Is there any real showstopping issues for the plugin.   Spend the time doing due diligence and look at the github
issues for the plugin, does the the plugin author/owner seem to respond to issues.  Is he taking pull requests?  

4) Is there decent documentation and preferably an example app for the plugin (check to make sure the example isn't
the default cordova app, this has happened to me a couple of times when I thought there was a sample app and it just
turned out to be Hello Cordova).

5) See if you can make your own quick and dirty sample app that does what you need it to do, and run it on all the platforms
you are going to run on.  Obviously for something like [In App Purchase](https://github.com/j3k0/cordova-plugin-purchase)
 that might be a little too much work for preliminary research (though I can attest to how well that particular
 plugin works, it's awesome), but if it is something like a barcode scanner, make sure it functions like you expect.  

6) Check StackOverflow and see if there are lingering issues with said Plugin.

7) Ask on the [Slack Channels](http://slack.cordova.io/) if anyone has used the plugin, and what their experiences were.
 
If everything checks out, and you either don't need plugins, or the plugins work great give Cordova +5 points, otherwise
+5 to Native.  If you discover that it is something that you simply currently can't do on Cordova, then really short-circuit
this whole process and go direct to Native.  If you are going to be using plugins that may require some care and attention,
or you are going to be writing your own plugins, make sure you have access to developers who are comfortable in all the
platforms you will be developing for.  Debugging plugins requires a fairly good understanding of the underlying platform.

#### Backend Requirements

Lots of mobile apps have to communicate backend servers to be functional.  Most modern services support various [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)
protocols but sometimes you have to communicate with servers in older binary (like [ISO 8583](https://en.wikipedia.org/wiki/ISO_8583)), 
or XML protocols (like [Soap](https://en.wikipedia.org/wiki/SOAP) or [EBX](http://xml.coverpages.org/ebx.html)).  Maybe
you have to work with a particularly complicated remote API where there are libraries in Java and C (or something that
iOS can work with) but not in Javascript.  If that is the case, then award 5 points to native.  If it either a JSON Rest API
or posting to a website and having to parse the results in HTML, Javascript potentially with the help of jQuery or another
Javascript library is going to be easier, award 3 points to Cordova.

#### Update Requirements

A lot of hay was made about ReactNative's ability to update without going the App Store, and with multiple [plugins] 
(https://github.com/nordnet/cordova-hot-code-push), including one from [Microsoft](https://github.com/Microsoft/cordova-plugin-code-push), or 
with the [hydration](http://docs.phonegap.com/phonegap-build/tools/hydration/) feature from PhoneGap build you can do the
same thing with Cordova.  In the past, the week to two week updates times of the iOS App Store made this a truly compelling
feature, however with Apple's new [push to shorten approval times](http://www.bloomberg.com/news/articles/2016-05-12/apple-shortens-app-review-times-in-push-to-boost-service-sales)
to just one day that becomes a less appealing feature of Cordova.  However, if you want really want to do [Continuous Deployment](https://www.agilealliance.org/glossary/continuous-deployment/),
or you are concerned that Apple will not be maintaining there speedy approval times in the future, chalk a couple of extra points up for the Cordova side.

### The Final Result

Even if you end up ignoring the final tally (you may find after doing all the research required to come up with a number
for Cordova or Native that you have already decided on one direction or another) thinking about and researching each
of these methods will give you a feel on the way to go.  Be pragmatic and patient, realize where the advantages of the various
methodologies lie and in the end, choose wisely.   You will, if you have a successful product, have to live 
with your decision for quite a while.





        






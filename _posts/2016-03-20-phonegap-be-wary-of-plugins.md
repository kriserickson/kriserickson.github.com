---
layout: post
title: "Phonegap, Be Wary of Plugins"
description: ""
category: PhoneGap
imagefeature: blog/dragons.jpg
tags: [Programming, Android, Mobile, PhoneGap, Cordova]
featured: true
---

Today, dear reader, I have a cautionary tale to tell.  It is a story of trust, and how that trust can quickly erode
when confronted with hard truths, and the truth that nothing is ever as easy it seems.  Yes today I am writing about
Phonegap Plugins and how they are both the best and the worst part of PhoneGap.   My tale begins with email,
a reader sent me an email (yes, I usually respond to reader emails) with some nice words to say about my
[Lessons Learned From 5 Years of Phonegap](http://www.agingcoder.com/programming/2015/02/21/lessons-learned-from-5-years-of-phonegapcordova-development/)
and wondering if it would be possible to make an Android PhoneGap version of his [iOS Beditations](https://itunes.apple.com/us/app/beditations/id969123738)
app.   He had spent a large amount having a firm create a Native iOS version of the App and was hoping that the
Android version could be done more economically in PhoneGap.  I looked at the Apps features (basically the App
plays a guided mediation to bring you to sleep and then wakes you at your selected hour with an inspirational
morning meditation, it also needed to be able loop white noise while the user is sleeping and monetize the app
through purchasing new meditations) and saw that the main features missing from PhoneGap out of the box was the ability
to create an Alarm and the ability to perform In App Payment.

So to my trusty Google I went, and Googled ["Cordova plugin alarm"](https://www.google.ca/search?q=cordova+plugin+alarm),
and ["Cordova plugin in app purchase"](https://www.google.ca/search?q=cordova+plugin+in+app+purchase).  I saw that there
were plugins available, and replied that it should be relatively easy to produce such a thing in PhoneGap, sent him
the links to the PlugIns and told him that any PhoneGap developer should be able to do this project in a relatively short
period of time, and it should not cost nearly what he had spent on his Native App.  That was then end of that, I thought,
hoping that he would find some PhoneGap developer that could quickly knock the App out for him.

When a week or so later he replied inquiring if I would be interested in the task, he had already created the UI in HTML,
all I needed to do was add the functionality I figured that since I felt that it would be so easy I kind of felt
obligated to undertake the task.  I literally thought it would take under 5 hours, given that the HTML was already there,
all I needed to do was add an alarm, payment and switch from HTML audio to the [cordova media plugin](https://github.com/apache/cordova-plugin-media) since
I was pretty sure that once the device went to the lock screen the HTML audio wouldn't play anymore (I was rigth about that much).
And so I agreed to help out with my standard consulting fee, doubling my 5 hour estimate to 10 hours because one thing
I have learned as a developer is that I am a terrible estimator of time -- hoping that if it only took 5 hours I would
be over delivering and the customer would be escstatic that it cost half what I said it would.  Ah, how naive I was.

The first thing I would recommend doing when looking at a core plugin (i.e. a plugin not supported by the Cordova team)
is look at the number of Stars and Forks it has on Github, look how often it is updated, and [**read the issues**](https://github.com/wnyc/cordova-plugin-wakeuptimer/issues).  Also note that you shouldn't compare the Stars and Forks of a Cordova supported
plugin with a normal plugin, compare them to a user contributed platform.  I knew that the namespace of the plugin was
no longer important, but if you are looking for plugins to use it is important to know that just because the name
starts with "cordova-plugin-" it is not necessarily a Cordova supported plugin, it is just named that way to make it
easier to find in NPM.  Anyhow, to make a long story short, if I had read the issues I would have noticed the issue
titled ["Not working on screen lock"](https://github.com/wnyc/cordova-plugin-wakeuptimer/issues/9), which basically meant
the alarms only fired when the phone was unlocked, and since most Android phones lock when they go to sleep it basically
made the plugin useless for the purpose of the Beditations app.  So my 5 hour job now required me to go spelunking
through the source of the WakeupTimer plugin and figure out a way to get it to work when the Screen locked, which
I after debugging some other issues with plugin I fixed by setting some flags for the cordova window,

{% highlight java %}
    Window cordovaWindow = cordova.getActivity().getWindow();
    cordovaWindow.addFlags(WindowManager.LayoutParams.FLAG_SHOW_WHEN_LOCKED);
    cordovaWindow.addFlags(WindowManager.LayoutParams.FLAG_TURN_SCREEN_ON);
    cordovaWindow.addFlags(WindowManager.LayoutParams.FLAG_DISMISS_KEYGUARD);
{% endhighlight %}

and then clearing them after the Alarm is done, or when you cancel the alarm:

{% highlight java %}
    Window cordovaWindow = cordova.getActivity().getWindow();
    cordovaWindow.clearFlags(WindowManager.LayoutParams.FLAG_SHOW_WHEN_LOCKED);
    cordovaWindow.clearFlags(WindowManager.LayoutParams.FLAG_TURN_SCREEN_ON);
    cordovaWindow.clearFlags(WindowManager.LayoutParams.FLAG_DISMISS_KEYGUARD);
{% endhighlight %}

The next problem with the alarm is that if due to memory pressure the Cordova App Android decides to kill the app,
when the alarm is fired the app knows nothing about the alarm to play.  So I had to create a way to save state in
the cordova App and play the alarm if app is killed (not challenging, but another thing to develop and to test).

Playing audio through the Cordova MediaPlayer plugin worked as expected, until I wanted to loop the audio.  Unfortunately
MediaPlayer didn't support audio looping in Android, so I figured I would just wait for the end of sound event and start the
track again.  Unfortunately even though that style of looping worked in the browser (I usually develop in the platform browser
now and then move to an emulator or [Genymotion](https://www.genymotion.com/) device once it is working in the browser) in
the emulator and even on real devices the MediaPlayer plugin wasn't sending any events, it wasn't even sending the duration
of the track so I could use SetTimeout to re-start the track about when I thought it was ending.   I Googled for issues with
the Cordova MediaPlayer plugin events not being called, I even looked in the [Cordova Issue Tracker](https://issues.apache.org/jira/browse/CB/),
but couldn't find anything (part of the problem with Googling for bugs in Cordova plugins is that the period of time
the bug is around is probably under a year so they don't seem to surface in StackOverflow under the weight of all of the older
PhoneGap/Cordova issues).  Giving up on the Media plugin, I tried switching to the [NativeAudio](https://github.com/floatinghotpot/cordova-plugin-nativeaudio)
plugin which did support looping of audio, except the looping supported by the NativeAudio plugin still had a 1/4 second
gap between the end of a track and the beginning of the next one.  With something like white noise it is very noticeable,
so eventually I realized we were going to half to start playing the looped track before the previous track ended.  It was
during this period messing around with multiple tracks and the original Media Player plugin, that I tracked it down the bug in the
media player to the plugin losing its message channel and then [this commit](https://github.com/apache/cordova-plugin-media/commit/597e998d1ebe75bfefa933a56d42006f1a309a8c) appeared in the commit logs for
the plugin.  Since I was using the 2.1 version of the plugin, and the 2.2 version wasn't out yet I had to manually patch
the plugin but now at least I could the events firing.  With the patched plugin working, I got the white noise background
tracks looping without interruption and it was almost impossible determine the time of the loop.  The moral of this part
of the story is that even though a plugin is a supported plugin, doesn't mean that it won't have bugs -- where I was basically
sure that I was doing something wrong with the MediaPlugin, it was actually a bug that had caused the Android version of the
Media Plugin to not send events in version 2.0.0 and 2.10 of the plugin.

The one task that I was kind of most concerned about in the development of the Application, was the payment.  And here
is where a Cordova Plugin truly shined, I have done payment in native Android apps and the [cordova-plugin-purchase](https://github.com/j3k0/cordova-plugin-purchase)
is even easier and more intuitive than doing purchases natively.  The docs are clear and simple, the api is relatively clean,
and there are clear instructions of how to get running, add your products and even how to test, though Google doesn't
make testing of payment easy -- but I guess that is understandable since you want payment to be as locked down as possible.  I
only wish all plugins were as solid as the payment plugin, [Jean-Christophe Hoelt](https://github.com/j3k0)
has to be complimented on his excellent work and maintenance of this plugin.

And so, what should have been a 5 hour job turned out to be more like a 10-12 hour job.  It was hardly a disaster since I
had given that as an estimate to begin with, but I have learned a lot about how to judge an evaluate plugins, and to not
assume that because a plugin is a core plugin means that it is bug free.  The [Beditations App](https://play.google.com/store/apps/details?id=com.highlymeditated.beditations)
is now in the App store, and I am pretty pleased that a PhoneGap/Cordova App could be relatively quickly churned out even with
all the issues with plugins.  But it is a warning that if you plan to use plugins that aren't core (or even if they are
core), you shouldn't be to afraid of debugging said plugin in Android Studio -- and always give yourself some wiggle
room when estimating projects.




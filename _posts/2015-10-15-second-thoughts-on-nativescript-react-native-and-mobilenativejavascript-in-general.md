---
layout: post
title: "Second thoughts on NativeScript"
description: "It's been 6 months since I wrote First Thoughts on NativeScript and you would think by now with my formidable blogging output I would have written dozens of articles following up on my initial thoughts..."
category: Programming
tags: [Mobile,Programming,NativeScript,JavaScript,MNJS]
featured: true
comments: true
---

<div style="font-size: 16px; margin: 0 0 10px 0; background: #f5f5f5; border: 1px solid #ddd; padding: 15px; margin: 0 auto 2em auto; max-width: 56.25rem; line-height: 1.5em"><strong>Update:</strong> Recent experiences with React Native can be found in the post: <a href="/programming/2018/07/04/react-native-a-tempting-quagmire/">React Native -- A Tempting Quagmire</a></div>


<span style="float: left; font-size: 4.688rem; line-height: 4.375rem; padding-top: .25rem; padding-right: .5rem; padding-left: .188rem; font-family: serif;">I</span>t's been 6 months since I wrote [First Thoughts on NativeScript](http://www.agingcoder.com/programming/2015/03/07/first-thoughts-on-nativescript/)
and you would think by now with my formidable blogging output I would have written dozens of articles following up on 
my initial thoughts.  Well, as they say the best laid plans of mice and men, but I finally spent several hours with
the latest build NativeScript build ([NativeScript 1.3](https://www.nativescript.org/blog/details/nativescript-1.3-release-is-live))
and I thought I would pass on my thoughts of how NativeScript progressing and my ongoing thoughts of NativeScript,
[React Native](https://facebook.github.io/react-native/), [Titanium](http://www.appcelerator.com/titanium/),
[TabrisJs](https://tabrisjs.com/) and what I am now dubbing the "MobileNativeJavaScript" movement (I know the MNJS name
is going to catch on and rock the world!)  

First off, updating NativeScript was a lot more painful than originally installing it.  Perhaps this was because when I last installed
NativeScript it was before the great [io.js](https://iojs.org) - [node.js](https://nodejs.org) merge - where NodeJs version 0.10 was 
still the defacto standard and [node-gyp](https://github.com/nodejs/node-gyp) (the node build tool for compiling c extensions) was
a little more reliable.  I understand that there are lot of moving parts in the node world, npm is run by one [company](https://www.npmjs.com/about)
(and where the stable versions switched from 1.4.x to 3.3.5 in under a year), node is being run by a [Foundation](https://nodejs.org/en/foundation/) 
(the stable versions of NodeKs in the past year have been 0.10.x, 0.12.x, and then 4.x) and node-gyp relies upon Visual Studio in Windows 
and the XCode Command Line tools on OSX.  The possible number of combinations to debug the instllation and building of NativeScript is pretty large, 
but other complex projects ([Cordova](http://cordova.apache.org/], [TypeScript](http://www.typescriptlang.org/), and [Kraken](http://krakenjs.com/) to name a few) 
don't seem to have the same problems that NativeScript has, I failed installing it on 5 different boxes (two Macs and three windows machines, 
with different versions of node and npm).  
  
<img src="/img/nativescript2/failed_build.png" style="width: 690px; border: 1px solid #000; margin: 0 10px 10px 0" />
<span style="display: block; text-align: center; font-weight: bold">Install of Joy</span>

Eventually the only way I could get it to install was creating a clean VM and installing it there.  And I spent some time playing around
with the new features: [new CSS properties](https://github.com/NativeScript/NativeScript/issues/191), 
[plugins](https://github.com/NativeScript/NativeScript/issues/25), 
and [animations](https://github.com/NativeScript/NativeScript/issues/255).  

### The New Features

#### CSS Properties

First of all, one of the complaints I had in the my first review was that it was difficult to style things, and I am happy
to report that has been fixed.  It may seem minor, but one of the ways to not have your app look like it was put together
in two minutes is to not have every part of it look the same.  While the css is much better, it is not as extensive
(obviously) as CSS in HTML and missing a lot of what we are used to in HTML5 but they have provided a lot more to work
with now for styling your app.

#### Plugins

The plugins are a welcome addition as well. The out of the box functionality of NativeScript is pretty limited: 
you get Location, Camera, 20 UI Widgets, 5 Layouts, 5 Dialogs and not much else.  One of the features I liked when it shipped 
was that you could call any native API that you wanted in Javascript.   Unfortunately that required that you be familiar 
with Android and iOS APIs and be comfortable enough with NativeScript to be able to convert it to Javascript.  So when you wanted
to be able to, say, get the version of the App, you would have to know that the code to get it in Android is:

{% highlight java %}
PackageInfo pInfo = getPackageManager().getPackageInfo(getPackageName(), 0);
String version = pInfo.versionName;
{% endhighlight %}

And know that you would have to convert it to the following Nativescript: 

{% highlight javascript %}
var packageManger = application.android.context.getPackageManager();
var pInfo = packageManager.getPackageInfo(context.getPackageName(), 0);
var version = pInfo.versionName;
{% endhighlight %}

Now you just need to include the [nativescript-appversion](https://www.npmjs.com/package/nativescript-appversion), and
you by installing the plugin you get the iOS version as well.  There are 30 odd plugins listed (25 cross platform) on the 
[NativeScript Plugins](https://github.com/Nathanaela/nativescript-plugins)
gallery, and some are as simple as getting the app version, to some that are a little more
full featured like the [NativeScript-Grid-View](https://github.com/PeterStaev/NativeScript-Grid-View).  A majority
are a couple of lines or less for each platform, yet all are welcome as not only do they make things easier for
you they serve as good documentation on how to integrate with the Native Platforms.

#### Animation 

Animation is very important in mobile apps, it is so important that in Google's excellent design spec on Material 
Design, the first section after "What is material" is the section on [animation](https://www.google.com/design/spec/animation/).
It gives clues to the user on what is happening when they interact with the app, and gives clues on what
to do next.  It can delight the user, or frustrate them if the animation is slow, awkward, or poorly done.  NativeScript's
animation will seem mostly familiar if you have used jQuery [animate](http://api.jquery.com/animate/).  You
can animate 5 properties (opacity, backgroundColor, position, scale, and rotation) with a duration, a delay
and an iteration.  The one thing missing from the animation is an easing, they have added what they call a "curve"
which has to be class specific to the OS (either [TimeInterpolator](http://developer.android.com/reference/android/animation/TimeInterpolator.html) 
for Android or [UIAnimationCurve](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/#//apple_ref/c/tdef/UIViewAnimationCurve)
for iOS).  Which means that if you wish to support both devices you have add code like this:

{% highlight javascript %}
view.animate({
      opacity: 0,
      duration: 3000
      curve: view.ios ? UIViewAnimationCurve.UIViewAnimationCurveLinear : 
            new android.view.animation.LinearInterpolator
    });
{% endhighlight %}    

and try to find roughly equivalent classes to do your easing.  Why they couldn't have abstracted easing is a bit
of a mystery, maybe it is a feature coming in the future.  
 
### The Problems

After spending hours getting NativeScript installed, I set out to try to rough out an app (I was going to create
a quick clone of my [Recipe Folder](https://recipe-folder.com) app, since it is written in Javascript I thought
it might be pretty easy, I could at least get the first page up and running in a few hours and maybe I could
reuse some of the code.


<img src="/img/nativescript2/recipe_folder.png" style="width: 300px; border: 1px solid #000; margin: 10px auto" />
<span style="display: block; text-align: center; font-weight: bold">Recipe Folder List Recipes Page</span>


And it was pretty easy to get the Javascript going to get a list of recipes, however I found
it was basically impossible to style the listview.  As much as I played with the somewhat foreign widget set XML
I couldn't get it to look anything like what I wanted.  Creating a simple list, was easy, styling said list
was very hard (I don't know if it is impossible, but I gave up after a couple of hours).  The next thing I
wanted to add was a menu in the upper left corner to match the menu.  I found now way to add a menu in NativeScript,
there is a side-drawer menu that only works in iOS but there appears to be no way to create a drop down menu.
Next I wanted to color the ActionBar, but apparently that is still [not possible](https://github.com/NativeScript/NativeScript/issues/499) 
yet either.  So basically I had an ugly list of recipes, OK, maybe then I will get to the recipe view part.  So I added
an event to go to view the recipe.  Below is the page I wanted to duplicate:

<img src="/img/nativescript2/recipe_folder_2.png" style="width: 300px; border: 1px solid #000; margin: 10px auto" />
<span style="display: block; text-align: center; font-weight: bold">Recipe Folder View Recipe Page</span>

The GridLayout was working pretty well to create my view, and things were going swimmingly until 
I wanted to add a button that had an image on the right (the x that allows the user to remove tags form the recipes).  And
then I tried to get styling going for the Ingredients and Directions and realized that the lack of an HTML widget
was a bit of a killer.  I spent 6 hours trying to get something demoable out, and failed miserably.  I was left
with an app I wouldn't show to anyone.  In short I was frustrated with the appearance of the app, it looked juvenile
and unprofessional and I couldn't see an easy way to fix even I spent hours more working on the app.  It was at this
point I abandoned the effort and that will probably be my last experience with NativeScript and probably my
last experience with the MobileNativeJavaScript.

Trying to convince myself that I was just not comfortable or familiar enough with NativeScript I downloaded and
built all the sample apps, they all look terrible.   The best looking app [Friends](https://github.com/nativescript/sample-friends) (see below), 
still has an unstyled title bar:
 
 <img src="/img/nativescript2/friends.png" style="width: 300px; border: 1px solid #000; margin: 10px auto" />
 <span style="display: block; text-align: center; font-weight: bold">Friends Sample App</span>
 
 Sure they are sample apps, but, their [App Showcase](https://www.nativescript.org/showcases) has 4 apps.  Three of them
 are pretty ugly sample apps, only one is available in the AppStore -- and it crashes on my  phone: 
 
<img src="/img/nativescript2/telerik_next.png" style="width: 300px; border: 1px solid #000; margin: 10px auto" /><span style="display: block; text-align: center; font-weight: bold">Crashy Crashy</span>

and the rest are pretty feature barren.  Has no one in the six months that this has been a product released an app that
they can point to in one of the app stores to brag about?  The number one recommendation I gave in my last article was to 
dogfood this framework, and it is pretty clear that no-one is building real apps with it.   

## Conclusion

NativeScript, ReactNative, Tabris, Appcelerator and all of the MobileNativeJavaScript frameworks seem to have too much downside
for the small upside of being able to write in Javascript and create apps on multiple platforms (which hybrid apps do already).  
I truly believe that the "performance" of hybrid apps is a MacGuffin, and it is not said performance of hybrid apps that are the 
why people under value them.   Rather it is the fact that really good modern apps are becoming more and more platform dependent, 
using the best features of the platform and that is what you are missing by going hybrid.  You lose all the animations and UI that come with
frameworks and because of that hybrid apps appear to look and feel a little last year.   It is not the fact that they
are less performant but this dated and non-native feel that is the issue with hybrid apps.  So either you accept that
(heck the Facebook app looks and feels terrible to me, and it is native) and try to create a unique feel and look for your
app in HTML5 (and use all the power and features of HTML5, including the powerful animations and graphics that is possible in HTML), 
or go native to create the best possible app on each platform.  None of which can be easily achieved by these MobileNativeJavaScript platforms.


 


 
 
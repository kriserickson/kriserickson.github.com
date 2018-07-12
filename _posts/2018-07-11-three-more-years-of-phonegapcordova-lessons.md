---
layout: post
title: "Three More Years of PhoneGap/Cordova Lessons"
description: ""
category: Programming
tags: [Mobile,Programming,PhoneGap,Cordova]
imagefeature: blog/phonegap.jpg
featured: true
---

Has it really been more than three years since I wrote [Lessons Learned](/programming/2015/02/21/lessons-learned-from-5-years-of-phonegapcordova-development/), hard to believe.  So much time
has past and yet it is definitely still the most viewed article on this website.  After re-reading it I felt it was
time to update its recommendations to be more recent, and add some new ones. Also if you find that post interesting,
there are a couple other articles on PhoneGap/Cordova on this website that you might find useful:

- [Should I use Cordova / Phonegap or go Native?](/programming/2016/09/03/should-i-use-cordovaphonegap-or-go-native/), although a couple of years old is still a valid articles on the benefits of Native or Phone Gap.  I feel that with the rise of modern JavaScript (which you can actually use due to pre-processors like Babel) and TypeScript Hybrid apps have become much more maintainable and a reasonable choice for larger projects.
- [Phonegap, be Wary of Plugins](http://kriserickson.com/phonegap/2016/03/20/phonegap-be-wary-of-plugins/), plugins are the best and worst part of Cordova.  Some tips for choosing and using them.

I kind of see this series of articles as having the following arc, this article will take a brief look at what has changed
since I wrote the last article and review the suggestions (lessons as I called them) to see if they are still valid advice.
Article two will be some more tips (mostly for people starting out with Cordova) that I have learned in the past few years.
And article three will be some of the hard learned pain points from maintaining a large cordova codebase.   So lets begin:

### Lesson 1 - Node is your best friend.
One of the points I was trying to make here, which was never clearly spelled out is that you should probably do some
pre-processing on your code and use some form of node build tool (whether that be [gulp](http://gulpjs.com/), [grunt](https://gruntjs.com/), 
[brocolli](http://broccolijs.com/), or just a set of npm scripts in a build directory).  I didn't speak of [webpack](https://webpack.js.org/)
back then, as it wasn't really on my radar but you might consider it as an option as well.  I would definitely recommend
you organize your project directory something like:

```
+.git
+.idea          (I always use WebStorm for Cordova Development, but VsCode is great too)  
+app
  +css
  +js
  -cordova.js   (I genally write a cordova shim for when running in the apps directory). 
  -index.html
+cordova
  +node_modules
  +platforms
  +plugins
  +res
  +scripts
  +www
  -build.json   (see in Article 2)
  -config.xml  
  -package.json 
+dist           (sometimes required for grunt and non-streaming build systems, this is just a scratch directory).
+node_modules   
+tasks          
-.babelrc       (ignore if you are using typescript) 
-.eslintrc.js   (ignore if you are using typescript)
-.gitignore     
-changelog.md   
-Gruntfile.js   (ignore if you are using gulp)
-gulpfile.js    (ignore if you are using grunt)
-package.json   
-README.md      (always include readme instructions, future you will appreciate it).
-tsconfig.json  (if you are using typescript, ignore if Javascript or Flow)
-tslint.json    (if you are using typescript, ignore if Javascript or Flow)
 
```

Your pre-processing script should then output into cordova\www.  You should also have a .gitignore file that looks
something like the following:

```
# Logs and junk
logs
*.log
npm-debug.log*
yarn-debug.log*
yarn-error.log*
*.swp
*.bak
tmp

# Intellij
.idea 

# Node Modules 
node_modules

# Temprory
dist

# Corodova work product
cordova/plugins 
cordova/platforms
cordova/www
```

We will speak more about suggestions for build tooling and other build and JavaScript/Typescript hints in the following
articles in this series. 

### Lesson 2 - Node is your worst enemy.

Node (and especially Node on windows) is in a much better place than it was 3 years ago (good grief, we were talking about
node v0.12 and the mess that [io.js](https://iojs.org/) was).  Most (not all) of the windows issues are solved, and unless
you want to do some image minification (using [sharp](https://github.com/lovell/sharp) or [node-canvas](https://github.com/Automattic/node-canvas)
or [jimp](https://www.npmjs.com/package/jimp)) you should have no problems running on Windows -- with one exception.

Node on windows has tendency to lock files that either Cordova or Gradle need to build (this happens sometimes on
on OSX, but it is much rarer) - frequently running ```cordova build``` again will solve the problem, but sometimes
you have to [kill the node process](https://superuser.com/a/643312/1462) that is locking the file.

Also, node has got much more aggressive with unhandled excpetions in Promises, meaning that the cordova tooling error 
reports are hidden in a mess of node promise rejection errors. Here, for example, is an attempt at running cordova in the wrong
directory:

```
>cordova run android
(node:20692) UnhandledPromiseRejectionWarning: Unhandled promise rejection (rejection id: 1): CordovaError: Current working directory is not a Cordova-based project.
(node:20692) [DEP0018] DeprecationWarning: Unhandled promise rejections are deprecated. In the future, promise rejections that are not handled will terminate the Node.js process with a non-zero exit code.
```

The error is there (**CordovaError: Current working directory is not a Cordova-based project.**), but you have to look for it and 
know where it is going to be.  Sometimes you don't get an error, just a rejection.

Last important thing to note about node (and this is true for all node projects, not just cordova) is that the versioning
in node can cause a lot of heartache (especially if you are on a team).  The default behavior for ```npm install --save```
is to add a ^ to the version number -- in the case of a lot of immature node modules this is insanity.  For example, if you
install [gulp-cordova-builder](https://www.npmjs.com/package/gulp-cordova-builder) (I know nothing about this project, and have
never used it, but it has a very low version number of 0.0.1 which is appropriate for out example) through the npm command
line ```npm install gulp-cordova-builder --save``` it will get saved into your package.json as ```"gulp-cordova-builder" : "^0.0.1"```.
This means that if you update npm at some time, or someone else checks out your project and it's version has updated from 0.0.1 to 
0.1.0 (which allows for some breaking changes in SemVer as any project under version 1.0.0 can change anything for at any time as
it is not stable, and that is assuming the authors are respecting SemVer) you will get a new version of the package installed.
This can lead to huge debugging issues where projects are not the same.  I would recommend that, unless you are working by
yourself and you know when you do an ```npm update``` and what effects that may have, remove all the ~,^,>, etc modifiers from
your npm packages and only upgrade those packages explicitly, you will save your self a bunch of hair pulling.  If you don't
at least commit the [package-lock.json](https://docs.npmjs.com/files/package-lock.json) so that you all start in the same place.

### Lesson 3 - Test on real devices but develop in Chrome.

Chrome Dev tools have only gotten better over time, so spend the time to learn as many of their features as possible (most importantly
you should know about [Device Emulation](https://developers.google.com/web/tools/chrome-devtools/device-mode/), but the more
you know about Dev Tools the better.  Personally I would read the "What's New in Chrome Dev Tools" from 
[58](https://developers.google.com/web/updates/2017/03/devtools-release-notes), and watch all the [videos](https://developers.google.com/web/updates/2017/04/devtools-release-notes) 
(they are only 5 minutes or so) from that point on.  I learned a ton of features I didn't know about (and now have come quite
handy with Run Command, if you don't know about that, hit Control/Command Shift-P you will see a list of all the
commands you can perform from "Capture Screenshot" to "Help" which shows the latest Release Notes).

I usually run a simple node [http-server](https://www.npmjs.com/package/http-server) in the ```app``` directory (where I have a mocked
version of cordova.js), but you can also look at using the browser platform now for debugging:

```
>cordova platform add browser
>cordova run browser
```

Most of the plugins do not fully support browser, so it is not as useful as it could be, and frequently just mocking the
cordova.js in your app directory like this:

{% highlight javascript %}
(function () {
    if (!window.Connection) {
        window.Connection = {
            UNKNOWN: 'unknown',
            ETHERNET: 'ethernet',
            WIFI: 'wifi',
            CELL_2G: '2g',
            CELL_3G: '3g',
            CELL_4G: '4g',
            NONE: 'none'
        };
    }

    if (!navigator.connection) {
        navigator.connection = {type: window.Connection.ETHERNET};
    }

    navigator.app = {
        exitApp: function () {
            console.log('App exited');
        }
    };

    if (!window.device) {
        window.device = {
            name: 'DeviceBrowser',
            model: 'Browser',
            version: '7.1',
            platform: 'Browser',
            uuid: localStorage.cordovaFakeUUID
        };
    }

    window.cordova.InAppBrowser = {
        open: function (url, target, options) {
            return window.open(url, target, options);
        }
    };

    document.addEventListener('DOMContentLoaded', function () {
        $.getScript('js/fake-camera-gallery.js');
        setTimeout(function () {
            window.cordova.fireDocumentEvent('deviceready');
        }, 500);
    });

})();
{% endhighlight %} 

will produce results similar to the browser platform, but all for faster reloads as you don't have to do 

```
>cordova run browser
```
every time you want to reload the code.  Of course this requirement can be avoided by using [cordova-browser-sync](https://www.npmjs.com/package/cordova-plugin-browsersync)
with the --live-reload option, or [```phonegap serve```](http://docs.phonegap.com/references/phonegap-cli/serve/), 
but if you are taking my advice and working in the apps directory this requires you push a build from the apps directory 
to your cordova/www every time you want to update.  

### Lesson 4 - Genymotion for Android Development is awesome
  
[Genymotion](https://www.genymotion.com/) was great compared to the old Android Emulator, but Google has improved the 
Android emulator so much that it isn't necessary any more.  [Haxm](https://software.intel.com/en-us/articles/intel-hardware-accelerated-execution-manager-intel-haxm)
is installed automatically when you install Android Studio these days, and the new Emulator is fast, has almost all the
features of GenyMotion.  You might want to turn Snapshots off in the Emulator, as they seem to sometimes cause problems,
but other than that, ignore Lesson 4 from 2015.

### Lesson 5 - Multiple OSX Machines

Yeah, you pretty much need an OSX machine if you plan to release an iOS verson of your app, 
[GapDebug](https://www.genuitec.com/products/gapdebug-end-of-life-notice/) is long gone and the 
[ios-webkit-debug-proxy-win32](https://github.com/artygus/ios-webkit-debug-proxy-win32) is no longer maintained
and doesn't work on Windows 10 or with iOS 11.  So if you are planning to release an iOS version of your app, you need to either
use something like [MacInCloud](https://www.macincloud.com/), which is at best a painful experience, or your own OSX machine.
If you have a ton of money to burn, you could buy an iMac Pro (at $5000K plus), or a 2015 Macbook Pro (I can't recommend
the new MacBook Pros due to their [innate keyboard issues](https://www.imore.com/macbook-pro-butterfly-keyboard-effect)), or you
can pick up an old 2012 Mac Mini (don't get the currently for sale 2014 version as they are not upgradable) off of EBay and 
upgrade the RAM and replace the hard drive with an SSD (you can probably get a reasonable Mac Mini with 16GB of RAM and a 256GB SSD   
for under a grand this way if you are willing to do a little work).

### Lesson 6 - Remote Device Debugging

No question about it, it was new in 2015, but Remote Device debugging is a necessity.  Get to know the url [chrome://inspect/#devices](chrome://inspect/#devices).
[Weinre](https://people.apache.org/~pmuellr/weinre/docs/1.x/1.5.0/Home.html), thank god, has become a thing of the past that hopefully we will never have to deal with again.
If you, like me, find the Safari Web Inspector basically unusable (there still is no way to pick a file except with the 
alphabetical list in the Debugger or Resources Panel) you can debug in Chrome with the awesome 
[remotedebug-ios-webkit-adapter](https://github.com/RemoteDebug/remotedebug-ios-webkit-adapter) (there are pretty clear instructions in the Readme),
it doesn't work perfectly (but they do take pull requests to improve the experience), but does a pretty amazing job for what it is.  


### Lesson 7 - Avoid loading the Platform project in an IDE

This was true in 2015, as back then Cordova was using the deprecated [Ant](https://ant.apache.org/) for building on Android 
(it hadn't migrated to [gradle](https://gradle.org/) yet) and caused problems in XCode.  These days PhoneGap plays much better with both platforms 
(though on Android, the ADB and gradle daemon that Cordova uses can conflict with Android Studio, so you may have to do a 
clean and/or shutdown of Android Studio to get builds to work) so as long as you follow lesson 8, feel free to open your project
in your IDE as it now rarely causes problems.

### Lesson 8 - Always be prepared to blow away a platform

Good advice then, still good advice now.  If you have to change the code (AndroidManifest.xml, build.gradle, some *-Info.plist), do 
it in a [hook](https://cordova.apache.org/docs/en/latest/guide/appdev/hooks/) rather than manually changing a file.  At some point
yoou will need to blow away a platform and you shouldn't worry that you will lose changes when you do so.

### Lesson 9 - Use as Few Plugins As Possible

Also still good advice, plugins tend to be fragile (even the ones supported by Adobe/Apache that are part of cordova, though they 
tend to be the best of the bunch). See [Phonegap, be Wary of Plugins](http://kriserickson.com/phonegap/2016/03/20/phonegap-be-wary-of-plugins/),
for the pain I have experienced myself.  

### Lesson 10 - Don’t write your own Framework

Even more true today than in 2015.  There was a time when it would have made sense, but we are so past that time that you 
would have to be a masochist to develop your own Framework now.   If you are in the Angular world, use [Ionic](https://ionicframework.com/),
or if you (like me) prefer Vue look at [Quasar](https://quasar-framework.org/), [Framework7 Vue](https://framework7.io/vue/), or [Onsen](https://onsen.io/vue/).
If you like React then look at [OnSen](https://onsen.io/react/), or [Framework7 React](https://framework7.io/react/) and if you like
kicking it Old School without having a binding framework as such, you can go with the standard [Framework7](https://framework7.io/docs/).

As we have seen, some of these tips/lessons have held up better over time and some have not.  Hopefully updating this has made
it a bit more relevant for today and help you build awesome apps in Cordova.

 
   


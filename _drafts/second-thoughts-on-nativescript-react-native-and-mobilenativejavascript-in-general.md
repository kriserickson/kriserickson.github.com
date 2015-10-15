---
layout: post
title: "Second thoughts on NativeScript, React Native, and MobileNativeJavascript in general"
description: ""
category: Programming
tags: [Mobile,NativeScript,JavaScript]
---
{% include JB/setup %}

It's been 6 months since I wrote [First Thoughts on NativeScript](http://www.agingcoder.com/programming/2015/03/07/first-thoughts-on-nativescript/)
and you would think by now with my formidable blogging output I would have written dozens of articles following up on 
my initial thoughts.  Well, as they say the best laid plans of mice and men, but I finally spent several hours with
the latest build NativeScript build ([NativeScript 1.3](https://www.nativescript.org/blog/details/nativescript-1.3-release-is-live)
and I thought I would pass on my thoughts of how NativeScript progressing and my ongoing thoughts of NativeScript,
[React Native](https://facebook.github.io/react-native/), [Titanium](http://www.appcelerator.com/titanium/),
[TabrisJs](https://tabrisjs.com/) and what I am now dubbing the "MobileNativeJavaScript" movement (I know the MNJS name
is going to catch on and rock the world!)  

First off, updating NativeScript was a lot more painful than originally installing it; perhaps this was because when I last installed
NativeScript it was before the great [io.js](https://iojs.org) - [node.js](https://nodejs.org) merge where node version 0.10 was 
still the defacto standard and [node-gyp](https://github.com/nodejs/node-gyp)(the node build tool for compiling c extensions) was
a little more reliable.  I understand that there are lot of moving parts in the node world, npm is run by one company (and where the stable 
versions switched from 1.4.x to 3.3.5 in under a year), node is being run by a Foundation (where the stable versions of node in the past year
where 0.10.x, 0.12.x, and then 4.x but 0.10 was around for several years) and node-gyp relies upon Visual Studio in windows 
and the XCode Command Line tools on OSX.  The possible number of combinations to debug building is pretty large, but other complex
projects (cordova, typescript, node-inspector to name a few) don't seem to have the same problems that NativeScript has, I failed installing
it on 5 different boxes (two Macs and three windows machines, with different versions of node and npm).  
  
<img src="/img/nativescript2/failed_build.png" style="width: 690px; border: 1px solid #000; margin: 0 10px 10px 0" />
<div style="text-align: center; font-weight: bold">Install of Joy</div>

Eventually the only way I could get it to install was creating a clean VM and installing it there.  


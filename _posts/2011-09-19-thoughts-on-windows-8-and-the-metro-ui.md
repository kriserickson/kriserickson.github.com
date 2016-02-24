---
layout: post
title: "Thoughts on Windows 8, and the Metro UI"
description: ""
category: Windows
tags: [windows8,metro]
---


Microsoft is betting heavily on Metro and the Metro UI, however I feel that this is misguided attempt at one interface to rule them all.
Creating a brand new API [WinRT](http://www.i-programmer.info/news/126-os/3055-winrt-the-new-windows.html),
and a whole new way to develop applications has shackled the Metro UI with the intractable problem that is a lack of Applications.

Unless the tablet version of Windows 8 is a runaway success, no developer in their right mind is going to got through the pain of
learning a new API just to be able to create applications that is only going to run on new computers
[1/2 of the windows
desktops in the world still run XP and only just over 1/4 run Windows 7](http://news.cnet.com/8301-10805_3-20086776-75/windows-xp-market-share-dips-below-50-percent/),
which is two generations back, how long will it take for there to be a large install base of Windows 8 especially since Windows 7 is pretty darn good).


Now a lot of people will be saying that developers don't actually have to learn a new API as Metro applications can be
developed in 3 ways that developers are innately familiar with: [DotNet orC++](http://msdn.microsoft.com/en-us/library/windows/apps/br211380(v=VS.85).aspx)
(using Xaml similar but not exactly the same as Silverlight and WindowsRT) and [Html/Javascript](http://msdn.microsoft.com/en-us/library/windows/apps/br211385(v=VS.85).aspx)
(with a ton of new WindowsRT api's added to the standard Javascript libraries). Unless you are a Windows Phone developer most of these are going to come
with pretty steep learning curves, just looking at the boiler-plate code emitted when creating a Metro Html/Javascript made my head spin and reminded
me of the old Embrace/Extend/Eliminate Microsoft of the past (yes lets create Html5 applications that only run in the Metro WindowsRT world, please!).

Even if you are just converting a Windows Phone 7 application to Metro you are going to have to develop a second User Interface(or three if you create a
new UI for Desktop sized screens as well as tablet screens) as something designed for a 4" phone screen isn't going to scale well for 11" touchpad
screen and certainly isn't going to look good on a 24" monitor. There doesn't appear to be any way to create unified projects in Visual Studio 11 that allow for
multiple targeted platforms (Phone, Metro UI, etc) and this is a feature they should probably work on.

I see Metro's only hope of not being relegated to being the next Windows Gadgets or Microsoft Bob on the desktop is if the tablets truly take off making it highly
desirable to write Metro applications. But from what we have seen in the past year and a half is that in the tablet world there seems to be only two ways to high sales,
being an [iPad](http://www.mactrast.com/2011/08/ipad-sales-continue-to-rise-as-competitors-flounder/) or selling for
[$99](http://www.engadget.com/2011/08/19/let-the-liquidation-begin-hps-16gb-touchpad-on-sale-for-99/)
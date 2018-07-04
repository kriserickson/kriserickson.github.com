---
layout: post
title: "Making Windows 8.1 Usable"
description: "I just got a new computer, and joy of joys it came with Windows 8.1.  I was seriously considering downgrading (upgrading?) to Windows 7, but I figured that if I was going to stay in the Windows world for a little while I would have to get use to direction that Windows was going and I would tough it out with Windows 8.1."
category: Windows 
tags: [Windows]
---
I just got a new computer, and joy of joys it came with Windows 8.1.  I was seriously considering downgrading (upgrading?) to
Windows 7, but I figured that if I was going to stay in the Windows world for a little while I would have to get use to 
direction that Windows was going and I would tough it out with Windows 8.1.  That said, there was a bunch of things I had
to do to make this machine usable on Windows 8.1.  I was seriously tempted to make the jump to Windows 10 preview, but 
after trying it in a VM (and repeated warnings from one of the SA's at my work) I decided against it.  So here is how
I manage to be productive on Windows 8.1.

1. Install [Start 8](http://www.stardock.com/products/start8/) (or [Classic Shell](http://www.classicshell.net/) if you want
 to save yourself $5) immediately.  The Modern Windows (as they seem to be calling it now) desktop is barren wasteland
 of pain and heartache.  Avoid it as soon as you can, and getting a reasonable start menu is the first step towards that.</li>

2. Don't bother with [Modern Mix](http://www.stardock.com/products/modernmix/) as there is literally not a single program
 I have found worth running that is a Modern UI app.  The Modern App store is a disaster and I don't see it getting fixed
 any time soon.
 
3. Disable the Charms (this can be done with a Reg-Hack, though to a lesser extent can be achieved by right clicking on the
   taskbar, selecting Properties and then go to Navigation and Disable ("When I Point to the upper-right corner, show the charms".
   The more complete Registry hack is available [here in a zip file](/img/DisableCharms.zip) or you can enter it manually:
   
   
````
    HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\ImmersiveShell\EdgeUI; 
    ValueName: DisableCharmsHint; ValueType: dword; ValueData: 1
    ValueName: DisableTRcorner; ValueType: dword; ValueData: 1
    ValueName: DisableTLcorner; ValueType: dword; ValueData: 1
````
   
         
   BTW if you really need to get the charms back after this registry hack, you can still get them back by hitting Windows-Key C,
   but not you won't accidentally get them when moving your mouse cursor to a different Window, or trying to scroll a document.</li>
  
4. Learn the new Windows key commands (and some of the old Windows commands): 
   <dl>
       <dt>Win-D</dt><dd>Hide all Apps and show the Desktop (or get to the desktop if you somehow end up in the wasteland of a modern App)</dd>
       <dt>Win-X</dt><dd>Power User Options (include Admin Command Prompt, which I need all the time, wish Windows 7 had this).</dd>
       <dt>Win-C</dt><dd>Bring up the Charms (see above).</dd>
       <dt>Win-E</dt><dd>Explorer</dd>
       <dt>Win-R</dt><dd>Run</dd>
   </dl>         
    
5. If you are running HighDPI on a laptop, and are not running at 100% DPI Mode (my old eyes can't handle 1080P laptop at
    100%) you are going to have to do a couple of tricks to get a couple of Apps I can't live without running:
   
   * PHPStorm (and all Intellij IDE's).  Java doesn't play well with the display scaling in Windows 8.1, so right click 
     on the .exe and choose Properties.   Next go to the Comparability tab click on the "Disable display scaling on high DPI settings".
     This will work for all apps that appear blurry at 125% DPI.  Unfortunately it means that it will now not be cleanly
     scaled to 125% and you will have to do the scaling within the App itself (or deal with tiny app if it doesn't support
     scaling within the App).
     
   * Chrome (the old trick was to go to do the Disable scaling, but now you can do it with a command line option).  Now
     right click on the shortcut icon (you will need to find in the Start Menu), and add the following to the Target 
     field under the Shortcut tab: 
   
   ````
   /high-dpi-support=1 /force-device-scale-factor=1
   ````
        
        
        

That's mostly got it covered for me now, Windows 8.1 is running as well or better than Windows 7 (well I still haven't got
used to the new Explorer, but since that isn't going away I am going to have to get used to it.  Hopefully this helps someone
with discomfort of [Who Moved My Cheese](http://www.hanselman.com/blog/Windows8ProductivityWhoMovedMyCheeseOhThereItIs.aspx)
when starting with Windows 8.1.  
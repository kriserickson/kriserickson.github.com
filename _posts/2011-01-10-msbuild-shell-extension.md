---
layout: post
title: "MSBuild Shell Extension"
description: ""
category: Programming
tags: [vs,reghack]
---

After MSBuildShellExtension stopped getting developed (so that it won't really build .Net 4.0 any more, even with a fair 
bit of fiddling), and after trying MSBuild Launch pad and not digging it, I figured why go all high tech and not just 
create a simple Registry Shell command.  For posterity (and so I can find it in the future) here it is (copy the
following into a .reg file and update the location of vcvarsall.bat depending upon your installation of Visual Studio and
whether or not you are on 64Bit windows or not).


    Windows Registry Editor Version 5.00

    [HKEY_CLASSES_ROOT\VisualStudio.Launcher.sln\Shell\Build\Command]
    @="cmd /k \"\"C:\\Program Files (x86)\\Microsoft Visual Studio 10.0\\VC\\vcvarsall.bat\"\" x86 &amp;&amp; msbuild %1"

    [HKEY_CLASSES_ROOT\VisualStudio.Launcher.sln\Shell\Clean\Command]
    @="cmd /k \"\"C:\\Program Files (x86)\\Microsoft Visual Studio 10.0\\VC\\vcvarsall.bat\"\" x86 &amp;&amp; msbuild /target:clean %1"

    [HKEY_CLASSES_ROOT\VisualStudio.Launcher.sln\Shell\Rebuild\Command]
    @="cmd /k \"\"C:\\Program Files (x86)\\Microsoft Visual Studio 10.0\\VC\\vcvarsall.bat\"\" x86 &amp;&amp; msbuild /target:rebuild %1"

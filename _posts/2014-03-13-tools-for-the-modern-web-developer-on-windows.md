---
layout: post
title: "Tools for the Modern Web Developer on Windows"
description: ""
category: Programming
tags: [Programming,Windows]
---

Be a windows developer in the web world sucks.  Bring a windows laptop to conference or meet-up you feel like the
the not so bright kid in the corner eating paste.  Of course you could cover it with Linux stickers and [pretend
it's running Linux](http://dpcdpc11.deviantart.com/art/Maverick-for-Win7-194347855) but if you are going
to [make the uncool, cool](/geek%20life/2014/01/24/trying-too-hard-to-make-uncool-cool/) here is how to embrace
windows as modern web developer.

1. Get a decent editor, I personally swear by [Vim](http://www.vim.org) but [Sublime](http://www.sublimetext.com/) or
   event [Notepad++](http://notepad-plus-plus.org/). As long as it can do search with regular expressions, macros,
   has some kind of syntax highlighting, and can do column or block editing you should be good.  But get good
   at your editor of choice, I love VIM because it is available everywhere I want to be (Linux, Windows, Mac).  Even
   the most stripped down systems at least have a minimal vi installed, so you won't be completely lost.  Also make
   sure that editor is in your filepath, you can do that with
1. [Intellij Idea](http://www.jetbrains.com/idea)/[Webstorm](http://www.jetbrains.com/webstorm)/[Phpstorm](http://www.jetbrains.com/phpstorm)/
    [Rubymine](http://www.jetbrains.com/ruby)/[PyCharm](http://www.jetbrains.com/pycharm).  This may be heresy, and it
    is probably because I am getting old, but writing code without constant static analysis is cowboys who think
    that they are better programmers than they are.  Everybody makes mistakes and computers are getting better and
    better at finding them.  For me the JetBrains tools are the best finding errors, refactoring, and so many
    other things that installing them is one of the first things I do on any machine.  It even has a [VIM plugin](http://plugins.jetbrains.com/plugin/164).
    I may use a test editor a lot, but I write almost all of my code in Intellij.
1. You need some kind of Unix toolchain, this may be a full blown [cygwin](http://www.cygwin.com/) installation or just the tools from
    [msysgit](http://msysgit.github.io/)  In fact to be honest, although I used to be a total cygwin junkie, I almost
    never find myself in a cygwin console any more as the msysgit tools basically have all I need.  And the path
    confusion in cygwin especially when running non-cygwin utilities is more of a headache than it is worth.
1.  [Ninite](http://ninite.com) is a great tool to get up and running on a new PC, it basically packages a script to install
    a bunch of programs and then downloads and installs them.  A lot of the programs I am recommending are available on
    Ninite and I have yet to have it install any Malware (Toolbars, etc) when it installs a program.  Rather than
    jumping to 20-30 websites you can have it do its magic while you are doing something else (it doesn't even
    prompt you so you can actually work at your computer while it is installing things).  It isn't a package manager
    because it doesn't keep things up to date, but it is a lot better than the old way of doing thing.
1.  [Chocolatey](https://chocolatey.org/) - is another software package manager that help you install programs, though because
    it is a hack on top of NuGet that throws installers and exe's into a package manager it is not like a real package manager
    like apt, yum, ports, homebrew or macports, it doesn't really know too much about versions and thus is not great
    at keeping the versions up to date.  Also be aware that sometimes it has two installers, one that runs an exe installer
    and one that just installs the .exe into Chocolatey itself.  For something like Node you want to install the exe
    or you don't get NPM.  The Chocolatey package naming convention is that if there is a local install it will just have
    the name and if there is an installer run it gets the name + .install.  So you want to cinst nodejs.install not cinst nodejs.
1.  [Secunia](http://secunia.com/vulnerability_scanning/personal/) since we don't have nice package managers on windows, we
    have to rely on tools like Secunia to tell us when programs are out of date and potential security risks.
1. [Git](http://git-scm.com/) and [Github](http://github.com) work fine on Windows now, and Github is probably the
    greatest thing about open source these days.  I personally wounld't bother with [Github for windows](http://git-scm.com/),
    but [TortoiseGit](https://code.google.com/p/tortoisegit/) has finally gotten decent.  And as stated above
    [msysgit](http://msysgit.github.io/) is really good.  A big hint for using git though, unless you are willing to
    live in cygwin stick to https urls (i.e. choose https://github.com/kriserickson/topcoat-touch.git over git@github.com:kriserickson/topcoat-touch.git)
    as windows has a ton of problems with ssl (where it stores your keys, etc) that will lead to no end of problems.
1.  You need to install [Putty](http://www.chiark.greenend.org.uk/~sgtatham/putty/) and the related tools.  If you don't know how to use
    pageant, I would recommend [learning](http://winscp.net/eng/docs/ui_pageant), especially if you spend any time on remote machines
    through SSH. (Completely off topic, but I could never find why pageant is called pageant rather than pagent.)  While
    you a learning about pageant, you should probably pick up a copy of [WinScp]((http://winscp.net) for transferring files.
1.  I find I always need a graphics editor, and I personally install [Paint.Net](http://www.getpaint.net/) as one of the first
    programs on any machine I have, you could use [gimp](http://www.gimp.org/).  You don't necessarily need a screenshot
    tool (Snipping Tool is pretty good or just Ctrl-PrtScr), but you do need to swap out the atrocious Windows Photo Viewer as
    the default graphics viewer with [Irfanview](http://www.irfanview.com/).  **Warning: Irfanview default download is download.net,
    which wraps it's downloads in crapware, fosshob and tucows still to my knowledge do not. Be careful when installing
    some of these programs, most of the toolbars are installed by default when you select the default setup.  That warning
    goes for winscp as well as Sourceforge has started wrapping some of it's downloads as well.  Also if you do download
    these apps one at a time from Google search be very careful, malware companies are buying ads on google that look
    like the real software company and wrap the application in malware.  It is the scourge of windows and may be the main
    reason for Windows death. **
1.  [Nodejs](http://nodejs.org/), [Ruby](http://rubyinstaller.org/), and [Python](http://www.python.org/downloads/windows/).  You may
    never program in any of these languages, but lots of tools you will be using will require them.  Get the 1.9 ruby and the 2.7
    python unless you are actually working in the languages as all of the tools are still based off of the older versions. For Ruby
    you may be required to install the DevKit (http://rubyinstaller.org/downloads/) as well.
1.  [Rapid Environment Editor](http://www.rapidee.com), you really want a few programs in your path (your text editor for
   example), and this is the best tool I have found for setting up your Path and other environment variables.
1.  I always need a merge tool, and I use [Winmerge](http://winmerge.org/).  [Beyond Compare](http://www.scootersoftware.com/) is
    also excellent but does cost $30 (which is pretty reasonable).  The merge in TortoiseGit/TortoiseSVN is also good.
1.  If you are a serious developer you need serious passwords for the root account on your servers, and
    I use [KeePass2](http://keepass.info/) for storing those passwords and all my passwords.
1.  It took me a long time to get into the File sync flow (I used to use Hamachi as a vpn to manage files and then use RDP
    for remote desktop) but now that I have gotten on the bandwagon I couldn't live my life without it.  I personally use
    dropbox, but only because it is simple, it actually probably has more features than I want -- the more features the
    more chance there are for security issues, but [ondrive](https://onedrive.live.com/about/en-us/) (ne skydrive)] /
    [box.net](https://www.box.com) / [gdrive](https://drive.google.com/#shared-with-me) / or even [bittorrentsync](http://www.bittorrent.com/sync)
    are all equally good options.

I know this is more like a software list rather than some kind of Zen Guide to programming on windows (and not hating it),
but as you are a Windows guy, embrace your tools.  You may not have the prettiest hardware, but you do have the fact that
until the last few years tons of desktop was designed for windows that never got ported to Mac or Linux.  And don't get too
frustrated, if worse comes to worse you can always repave your PC or Laptop with Linux...



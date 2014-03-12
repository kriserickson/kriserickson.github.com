---
layout: post
title: "Tools for the Modern Web Developer on Windows"
description: ""
category: 
tags: Programmings,Windows
---
{% include JB/setup %}
Be a windows developer in the web world sucks.  Bring a windows laptop to conference or meetup you feel like the
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
2. [Intellij Idea](http://www.jetbrains.com/idea)/[Webstorm](http://www.jetbrains.com/webstorm)/[Phpstorm](http://www.jetbrains.com/phpstorm)/
    [Rubymine](http://www.jetbrains.com/ruby)/[PyCharm](http://www.jetbrains.com/pycharm).  This may be heresy, and it
    is probably because I am getting old, but writing code without constant static analysis is cowboys who think
    that they are better programmers than they are.  Everybody makes mistakes and computers are getting better and
    better at finding them.  For me the JetBrains tools are the best finding errors, refactoring, and so many
    other things that installing them is one of the first things I do on any machine.  It even has a [VIM plugin](http://plugins.jetbrains.com/plugin/164).
    I may use a test editor a lot, but I write almost all of my code in Intellij.
3. Unix toolchain, this may be a full blown [cygwin](http://www.cygwin.com/) installation or just the tools from
    [msysgit](http://msysgit.github.io/)  In fact to be honest, although I used to be a total cygwin junkie, I almost
    never find myself in a cygwin console any more as the msysgit tools basically have all I need.  And the path
    confusion in cygwin especially when running non-cygwin utilities is more of a headache than it is worth.
4. [Git](http://git-scm.com/) and [Github](http://github.com).  Don't bother with [Github for windows](http://git-scm.com/),
    but [TortoiseGit](https://code.google.com/p/tortoisegit/) has finally gotten decent and as stated above
    [msysgit](http://msysgit.github.io/) is really good.  Hint for using git though, unless you are willing to
    live in cygwin stick to https urls (i.e. choose https://github.com/kriserickson/topcoat-touch.git over git@github.com:kriserickson/topcoat-touch.git)
    as windows has a ton of problems with ssl (where it stores your keys, etc) that will lead to no end of problems.
5.  [Putty](http://www.chiark.greenend.org.uk/~sgtatham/putty/) and the related tools.  If you don't know how to use
    pageant, I would recommend [learning](http://winscp.net/eng/docs/ui_pageant) if you spend any time on remote machines
    through SSH. (Completely off topic, but I could never find why pageant is called pageant rather than pagent.)  While
    you a learning about pageant, you should probably pick up a copy of [WinScp]((http://winscp.net) for transferring files.
6.  Install [Paint.Net](http://www.getpaint.net/) and [Irfanview](http://www.irfanview.com/) and change the default
    image viewer from the atrocious Windows Photo Viewer to Irfanview.  **Warning: Irfanview default download is download.net,
    which wraps it's downloads in crapware, fosshob and tucows still to my knowledge do not. Be careful when installing
    some of these programs, most of the toolbars are installed by default when you select the default setup.  That warning
    goes for winscp as well as Sourceforge has started wrapping some of it's downloads as well.**
. [Rapid Environment Editor](http://www.rapidee.com)
.  Winmerge
.  Nodejs, Ruby, Python
.  Choclatey
.  KeePass2
.  File sync (dropbox/gdrive/skydrive/box.net/bittorrentsync).
.  Atlasian or Bitbucket
. Secunia




---
layout: post
title: "Typescript All The Things!  Lessons learned moving a large codebase to typescript"
description: "Lessons learned moving a large codebase to typescript"
category: TypeScript
imagefeature: blog/typescript.jpg
tags: [Programming, JavaScript, TypeScript]
---
Finally after three and a half years, I'm all in on [TypeScript](https://www.typescriptlang.org/).  What really
pushed me over the line was creating a fairly large SPA (single page app) in Angular and TypeScript.  Once you
got around the tooling (getting a good [gulp](http://gulpjs.com/) script 9 months ago was half the struggle
but there are excellent samples and even pretty good generators now), and spent the couple of hours it takes
to get comfortable with typescript and tsd (which is now superceded by [typings](https://github.com/typings/typings))
and I was sold.  Of course it makes less sense on a small project with few dependencies and just a few odd scripts,
but for any project of any size that I was to greenfield I would definitely start with TypeScript.  And then,
after yet another bug at work where two parameters where flipped in a call, and another where two object
properties (photoCount and photosCount) where used interchangeably throughout the code causing subtle bugs that
took days to track down, I decided that I was going to bite the bullet and port our JavaScript codebase to TypeScript.
I had just recently heard a great [interview](https://devchat.tv/js-jabber/209-jsj-typescript-with-anders-hejlsberg)
with [Anders](https://twitter.com/ahejlsberg) about how you can literally just take all your .js files and rename them
.ts and get some of the advantages of TypeScript, so I set off to do so.

#### Tip 1 -- Chrome Dev Tools and Source Maps

First, part of the reason I have become so attached to TypeScript is that since late 2014 (Chrome 39) [SourceMaps have been
enabled by default](https://developers.google.com/web/tools/chrome-devtools/debug/readability/source-maps?hl=en#source-maps-in-devtools-sources-panel)
and work really well with TypeScript, there is basically only 1 trick to learn about debugging in Chrome Dev Tools (or Firefox)
in SourceMaps and that is that sometimes 'this' is '_this'.  Which is to say, if you look at TypeScript output you will
discover that whenever you use an arrow function, it creates a reference to this in _this.  See the example silly class below:

``````
class TimedLogger {
	constructor(private msg:string) {}

    public output() {
		setTimeout(() => {
			console.log(this.msg);
		})
    }
}
``````

and that converts to :

```````
var TimedLogger = (function () {
    function TimedLogger(msg) {
        this.msg = msg;
    }
    TimedLogger.prototype.output = function () {
        var _this = this;
        setTimeout(function () {
            console.log(_this.msg);
        });
    };
    return TimedLogger;
}());
```````

So, when you are debugging in the Chrome Dev tools, and you set a breakpoint in the **output** function it will look like you can
type:

````````
> this.msg
  undefined
````````

which fails since this is actually bound to the window (global) scope, but if you type

`````````
> _this.msg
  "Hey Ma! It Works!"
`````````

you are all good.  This was learned quickly when we developed the Spa app, but it still trips me up every now
and then (especially when dealing with the dreaded scoping of this in classes -- more on that later) and it frequently
trips up our junior devs so I thought I would mention it at the top.

#### Tip 2 -- Set up a good tsconfig.json File

The first time I built a moderately large TypeScript application I omitted creating a tsconfig.json and did everything
with command line options called from a gulp file.  Do not make this mistake, while it is nice to have the control
over what typescript files get compiled through watchers and the other advantages of grunt, you are going to want to
tsconfig.json to be able to set various options of how typescript compiles your files.  While the default way to
specify all the files you are converting is to create a list of files

`````````
"files": [
   "core.ts",
    "sys.ts",
    "types.ts",
    "scanner.ts",
    "parser.ts",
    "utilities.ts",
    "binder.ts"
]
`````````

this is not good for us lazy programmers with hundreds of files to compile, especially if they are a bunch of old
javascript files that are being renamed and moved into more appropriate folders as we going through the process of
turning all our old JavaScript into TypeScript.  The better way is to use filesGlob, a la:

``````````
"filesGlob": [
    "typings/tsd.d.ts",
    "ts/**/*.ts"
  ]
``````````

however, here is the rub with fileGlob (which is hopefully fixed by the time you read this), it is clearly caching the
list files because when you add a new file to the ts directory it won't compile it.  My current solution is to change
the second glob ("ts/**/*.ts") to point directly to the file and run typescript again (or have [WebStorm](https://www.jetbrains.com/webstorm/)
run typescript on a watcher, see more about WebStorm and TypeScript later in this post).  Then change the filesGlob back
to "ts/**/*.ts" and it will have smartened up.

There are very useful options available to you in the tsconfig.json file:

**noEmitOnError** - Don't output the js file until there are no errors in the ts file.
**noFallthroughCasesInSwitch** - Don't allow fall throughs on case switches
**target** - The language to target, for now you want es5 but es6 should be soon.

A full list of compiler options can be found [here](https://www.typescriptlang.org/docs/handbook/compiler-options.html).

#### Tip 3 - Use Typings (definately typed)

To get proper IntelliSense or any kind of code completion and static type checking in your editor (whether it is WebStorm,
[Visual Studio Code](https://code.visualstudio.com/), or  [Vim with TypeScript support](https://github.com/leafgarland/typescript-vim))
you need to install with Typings all the libraries you are using (unless of course you are really creating VanillaJS TypeScript and
if you are [kudos](https://cdn.meme.am/instances/500x/56204219.jpg)).  It gives you more than code completion, of course,
it also tells the TypeScript compiler how you should be using various APIs and you will get warnings if you are using
them wrong.

If you aren't going to go all in, and are only going to convert a few of your JavaScript files you are going to want to
add your own my-typings.d.ts (or something much better named) where you can document the libraries you aren't going to
convert, and say, any JQuery plugins you might have written.  Included below, to get you started, is the definitions
for a hypothetical block/unblock jquery extension that allowed you disable access to some UI elements.  It would could be used
like:

``````
$('#okButton').block({toolTip: 'Please agree to terms and conditions'}});

// Or optionally
$.unblock('#okButton');
``````

The following should be pretty self-explanatory and this isn't an article on writing definitely typed sytax but quickly
going over it, the DefaultStatic allows selection through a selector string and takes an optional object for the options.
The DefaultJquery requires calling from a JQuery object and also takes an optional Object.  Of course you can make these
much more detailed (you can specify the potential options, you could make the DefaultStatic take an element or a
JQuery object, but the intention is pretty clear).  Also, note this does require having already installed the jquery.d.ts
file through typings.

``````
namespace MyJquery {

    interface DefaultStatic {
        (selector:string, options?:Object):JQuery;
    }


    interface DefaultJQuery {
        (options?:Object):JQuery;
    }

}


interface JQueryStatic {
    block:MyJquery.DefaultStatic;
    unblock:MyJquery.DefaultStatic;
}

interface JQuery {
    block:MyJquery.DefaultJquery;
    unblock:MyJquery.DefaultJquery;
}
``````

#### Tip 4 - Use tslint (optional)

To get even further benefits from TypeScript (and some help that might track down some of the errors you might
encounter if you are going to convert all of your old Javascript to Classes and the like) you may want to use
[TSLint](https://palantir.github.io/tslint/).   Spend some time looking at the [rules](http://palantir.github.io/tslint/rules/),
and the example [tslint.json](https://github.com/palantir/tslint/blob/master/docs/sample.tslint.json) file,
but I would recommend heavily altering the sample tslint.json file (it is **very** strict and has some
weird checks for things I think TypeScript removes the need for (trailing-comma, use-strict, etc)).  While you
may want to get everyting working first, and then run tslint, be aware that it is going to hurt your feelings about
your code if you aren't ready for it, especially if you use said sample config file.

#### Tip 5 - You don't have to turn everything into classes






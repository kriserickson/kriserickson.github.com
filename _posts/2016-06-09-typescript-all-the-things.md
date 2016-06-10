---
layout: post
title: "Typescript All The Things!  Lessons learned moving a large codebase to typescript"
description: "Lessons learned moving a large codebase to typescript"
category: TypeScript
imagefeature: blog/typescript.jpg
tags: [Programming, JavaScript, TypeScript]
featured: true
---
Finally after three and a half years, I'm all in on [TypeScript](https://www.typescriptlang.org/).  What really
pushed me over the line was creating a fairly large SPA (single page app) in Angular and TypeScript.  Once you
got around the tooling (getting a good [gulp](http://gulpjs.com/) script 9 months ago was half the struggle
but there are excellent samples and even pretty good generators now), and spent the couple of hours it takes
to get comfortable with typescript and tsd (which is now superseded by [typings](https://github.com/typings/typings))
and I was sold.  Of course it makes less sense on a small project with few dependencies and just a few odd scripts,
but for any project of any size that I was to greenfield I would definitely start with TypeScript.  And then,
after yet another bug at work where two parameters where flipped in a call, and another where two object
properties (photoCount and photosCount) where used interchangeably throughout the code causing subtle bugs that
took days to track down, I decided that I was going to bite the bullet and port our JavaScript codebase to TypeScript.
I had just recently heard a great [interview](https://devchat.tv/js-jabber/209-jsj-typescript-with-anders-hejlsberg)
with [Anders](https://twitter.com/ahejlsberg) about how you can literally just take all your .js files and rename them
.ts and get some of the advantages of TypeScript, so I set off to do so.

**Warning!  This article is a bit of a deep dive, with lots of source code.  Please let me know in the comments
  if this is useful or whether it is best to talk in generalities without getting into the weeds.**

#### Tip 1 -- Chrome Dev Tools and Source Maps

First, part of the reason I have become so attached to TypeScript is that since late 2014 (Chrome 39) [SourceMaps have been
enabled by default](https://developers.google.com/web/tools/chrome-devtools/debug/readability/source-maps?hl=en#source-maps-in-devtools-sources-panel)
and work really well with TypeScript, there is basically only 1 trick to learn about debugging in Chrome Dev Tools (or Firefox)
in SourceMaps and that is that sometimes 'this' is '_this'.  Which is to say, if you look at TypeScript output you will
discover that whenever you use an arrow function, it creates a reference to this in _this.  See the example silly class below:

{% highlight csharp%}
class TimedLogger {

    constructor(private msg:string) {}

    public output() {
        setTimeout(() => {
            console.log(this.msg);
        })
    }
}
{% endhighlight %}

and that converts to :

{% highlight csharp%}
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
{% endhighlight %}

So, when you are debugging in the Chrome Dev tools, and you set a breakpoint in the **output** function it will look like you can
type:

{% highlight shell %}
> this.msg
  undefined
{% endhighlight %}

which fails since this is actually bound to the window (global) scope, but if you type

{% highlight shell %}
> _this.msg
  "Hey Ma! It Works!"
{% endhighlight %}

you are all good.  This was learned quickly when we developed the Spa app, but it still trips me up every now
and then (especially when dealing with the dreaded scoping of this in classes -- more on that later) and it frequently
trips up our junior devs so I thought I would mention it at the top.

#### Tip 2 -- Set up a good tsconfig.json File

The first time I built a moderately large TypeScript application I omitted creating a tsconfig.json and did everything
with command line options called from a gulp file.  Do not make this mistake, while it is nice to have the control
over what typescript files get compiled through watchers and the other advantages of grunt, you are going to want to
tsconfig.json to be able to set various options of how typescript compiles your files.  While the default way to
specify all the files you are converting is to create a list of files

{% highlight JSON %}
"files": [
   "core.ts",
    "sys.ts",
    "types.ts",
    "scanner.ts",
    "parser.ts",
    "utilities.ts",
    "binder.ts"
]
{% endhighlight %}

this is not good for us lazy programmers with hundreds of files to compile, especially if they are a bunch of old
javascript files that are being renamed and moved into more appropriate folders as we going through the process of
turning all our old JavaScript into TypeScript.  The better way is to use filesGlob, a la:

{% highlight JSON %}
"filesGlob": [
    "typings/tsd.d.ts",
    "ts/**/*.ts"
  ]
{% endhighlight %}

however, here is the rub with fileGlob (which is hopefully fixed by the time you read this), it is clearly caching the
list files because when you add a new file to the ts directory it won't compile it.  My current solution is to change
the second glob ("ts/**/*.ts") to point directly to the file and run typescript again (or have [WebStorm](https://www.jetbrains.com/webstorm/)
run typescript on a watcher, see more about WebStorm and TypeScript later in this post).  Then change the filesGlob back
to "ts/**/*.ts" and it will have smartened up.

There are very useful options available to you in the tsconfig.json file:

**noEmitOnError** - Don't output the js file until there are no errors in the ts file.<br/>
**noFallthroughCasesInSwitch** - Don't allow fall throughs on case switches.<br/>
**target** - The language to target, for now you want es5 but es6 should be soon.

A full list of compiler options can be found [here](https://www.typescriptlang.org/docs/handbook/compiler-options.html).

#### Tip 3 - Use Typings (definitely typed)

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

{% highlight JavaScript %}
$('#okButton').block({toolTip: 'Please agree to terms and conditions'}});

// Or optionally
$.unblock('#okButton');
{% endhighlight %}

The following should be pretty self-explanatory and this isn't an article on writing definitely typed syntax but quickly
going over it, the DefaultStatic allows selection through a selector string and takes an optional object for the options.
The DefaultJquery requires calling from a JQuery object and also takes an optional Object.  Of course you can make these
much more detailed (you can specify the potential options, you could make the DefaultStatic take an element or a
JQuery object, but the intention is pretty clear).  Also, note this does require having already installed the jquery.d.ts
file through typings.

{% highlight csharp %}
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
{% endhighlight %}

#### Tip 4 - Use tslint

To get even further benefits from TypeScript (and some help that might track down some of the errors you might
encounter if you are going to convert all of your old Javascript to Classes and the like) you may want to use
[TSLint](https://palantir.github.io/tslint/).   Spend some time looking at the [rules](http://palantir.github.io/tslint/rules/),
and the example [tslint.json](https://github.com/palantir/tslint/blob/master/docs/sample.tslint.json) file,
but I would recommend heavily altering the sample tslint.json file (it is **very** strict and has some
weird checks for things I think TypeScript removes the need for (trailing-comma, use-strict, etc)).  While you
may want to get everything working first, and then run tslint, be aware that it is going to hurt your feelings about
your code if you aren't ready for it, especially if you use said sample config file.  Also you should note that if
you do use tslint, and you are obsessive about getting rid of all of the errors like me, converting to typescript
will take a **lot** longer.  Giving types to every variable, even if typescript can infer it's type may be overkill,
but it will give a lot more information to the static analysis engine in typescript (see Tip 5 below).

#### Tip 5 - Use an Editor with support for TypeScript

I love [WebStorm](https://www.jetbrains.com/webstorm/) and all the JetBrains IDE variants, and I would highly recommend
it for developing in TypeScript (you won't even need to write a Gulp/Grunt script it will do almost all of that work for
you out of the box) but there are a lot of editors (see Tip 3) that have plugins that work with the TypeScript compiler
to make you more productive, and help you automatically detect errors.  The built in [support for TypeScript](https://www.jetbrains.com/help/webstorm/2016.1/typescript-support.html)
and tslint makes me think that it is a no brainer, but if you prefer VS Code (where it works out of the box), or
Sublime [the plugin is here](https://github.com/Microsoft/TypeScript-Sublime-Plugin), Vim [plugin](https://github.com/Quramy/tsuquyomi),
or even ughh, Eclipse [plugin](https://github.com/angelozerr/typescript.java) make sure that you are getting all the help that the
[TypeScript Language Server](https://github.com/Microsoft/TypeScript/blob/master/bin/tsserver) can give you.

TypeScript was specifically written to enable  tooling improvements and you should take advantage of the fact that
computers are very good at [static analysis](https://en.wikipedia.org/wiki/Static_program_analysis)
if they have a language that is "strict" enough to support it.  TypeScript gives JavaScript the information that
static analysis requires to do its job (of course if you don't supply types or make every type 'any' then there is
less static analysis that can be done by the compiler and the utility of converting to TypeScript is greatly reduced.)

#### Tip 6 - Namespaces remove the need for iife's

The first thing I do when I convert a js file is turn the iife (immediately invoked function expression, or a [Resig](https://twitter.com/jeresig)
as I believe [Scott Hanselman](https://twitter.com/shanselman) used to call them) that surrounds all the code in the file
into a namespace.  So

{% highlight JavaScript %}
(function() {
    // Code here
})();
{% endhighlight %}

becomes

{% highlight csharp %}
namespace testproject {
   // Code here
}
{% endhighlight %}

Note: If you look at the output in JS you will note that every dot becomes a new iife with variables attached so don't use
Java style namespaces.  For example:

{% highlight csharp %}
namespace com.ericksoft.recipefolder {
    console.log('Hello Nurse!');
}
{% endhighlight %}

becomes:

{% highlight JavaScript %}
var com;
(function (com) {
    var ericksoft;
    (function (ericksoft) {
        var recipefolder;
        (function (recipefolder) {
            console.log('Hello Nurse!');
        })(recipefolder = ericksoft.recipefolder || (ericksoft.recipefolder = {}));
    })(ericksoft = com.ericksoft || (com.ericksoft = {}));
})(com || (com = {}));
{% endhighlight %}

#### Tip 7 - You don't have to turn everything into classes

The first couple of files I converted I decided that I would convert from our old style classes (we for the most part have
our classes built upon functions and have eschewed the speed of prototypical functions for the advantages of private
functions and variables -- I don't say that this is the best way to do classes (and it is not the way that TypeScript
impliments them under the hood), but it has worked for us in the past.  So we had a class like this:

{% highlight JavaScript %}
(function() {
    function Employee(initialName, id) {
        var name;
        var greetCount = 0;

        setName(initialName);

        function setName(val) {
            // Name validation goes here
            name = val;
        }

        this.greet = function() {
            return 'Hello ' + this.name + ', your employee id is ' + id;
        }
    }
})();
{% endhighlight %}

and after renaming it, adding the namespace and bunch of flipping it became this:

{% highlight csharp %}
namespace test {
    class Employee {
        private id:string;
        private greetCount:number = 0;
        public name:string;

        constructor(name:string, id:string) {
            this.id = id;
            this.setName(name);
        }

        public greet():void {
            this.greetCount++;
            return 'Hello ' + this.name + ', your employee id is ' + this.id;
        }

        private setName(val:string):void {
            // Name validation goes here
            this.name = val;
        }
    }
}
{% endhighlight %}

Which isn't a lot of work for small files, but it is a lot of Regex Replace /this\.(\w+) = function/public $1/ and
Regex Replace /function (\w+)\(/private $1(/ and Regex Replace /var (\w+);/private $1;/ and then manaully adding a lot
of this references.

#### Tip 8 - JQuery can be a nemesis

Then I started running into problems, because there are a lot of JQuery calls in our
code, and if something calls that anonymous function without correctly setting the scope of this then you are headed
into a heap of trouble.  For example, suppose we have some Controller that is using jQuery:

{% highlight JavaScript %}
(function() {
    function EmployeeController(name) {
        $('#nameField').val(name).on('blur', nameFieldChanged);

        function nameFieldChanged(e:JQueryInputEventObject):void {
            name = $(this).val();
            outputName();
        }

        function outputName() {
            console.log(name);
        }
    }

    var tmp = new EmployeeController('John Doe');
})();
{% endhighlight %}

We naively convert it to TypeScript

{% highlight csharp %}
namespace test {
    class EmployeeController {

        constructor(private name:string) {
            $('#nameField').val(name).on('blur', this.nameFieldChanged);
        }

        private nameFieldChanged(e:JQueryInputEventObject):void {
            this.name = $(this).val();
            this.outputName();
        }

        private outputName() {
            console.log(this.name);
        }
    }

    var tmp = new EmployeeController('John Doe');
}
{% endhighlight %}

But if we look in the console, we see that we get an error (you can see the converted Javascript and what happens at
this [fiddle](https://jsfiddle.net/ksoncan34/nbwn4Lka/)).

<code style="color:red; background: #e5e5e5; border: 1px solid #999; padding: 5px; width: 100%; display: inline-block">Uncaught TypeError: this.outputName is not a function</code>

So what is going on?  Those who look for a minute will quickly realize (and I added a hint, using the jQuery shorthand $(this).val())
that the scope of this is scoped to the jQuery element that was blurred, and not scoped to our EmployeeController class at all.
So not only can we not call the prive outputName function, but we are actually setting name on the nameField input element
and not changing the name of our user at all.  How to fix this?   Well, for one, **never** bind jQuery callbacks to private or
public class members (quick note, there is really no difference in typescript between private and public class members and
the only thing stopping you from calling private members of TypeScript classes is the compiler will complain).  Also, you
are going to ween yourself off of the this scope in jQuery -- it's confusing and leads to more unintentional bugs than you
probably realize.   And you are going to have to use an arrow function.  Let's look at our fixed class:

{% highlight csharp %}
namespace test {
    class EmployeeController {

        constructor(private name:string) {
            $('#nameField').val(name).on('blur', (e:JQueryInputEventObject):void => {
                this.nameFieldChanged(e);
            });
        }

        private nameFieldChanged(e:JQueryInputEventObject):void {
            this.name = $(e.currentTarget).val();
            this.outputName();
        }

        private outputName() {
            console.log(this.name);
        }
    }

    var tmp = new EmployeeController('John Doe');
}
{% endhighlight %}

Now everything works.  See the updated [fiddle](https://jsfiddle.net/ksoncan34/fwexam4h/).  Now you might not think that
this will be a problem to find, but if you are using a lot of these you will get burned missing a few (at least I did).

#### Tip 9 - Callbacks are also problematic, use Promises instead

Similar to the jQuery issues, is the issue of callbacks.  If you are used to passing in callbacks to a function to handle
asynchronous functions you might also have issues with TypeScript classes.  For example:

{% highlight csharp %}
namespace test {
    class UserController {

        public constructor(private toastService:ToastService, private jsonService:JsonService) {}

        public changeName(name:string):void {
            this.updateNameAsync(name, function (success) {
                this.toastService('Name updated');
            });
        }

        private updateNameAsync(name:string, callback:(success:boolean) => void):void {
            // Name validation amd other stuff happens here...
            this.jsonService.updateName(name, function (success:boolean):void {
                callback(success);
            });
        }
    }
}
{% endhighlight %}

would throw an error when the service was updated, since toastService doesn't exist in the global scope.  You have to
remember to perform all your class callbacks with [.call](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call)
or [.apply](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply).  So to properly
use a callback in a TypeScript class you must use arrow functions and either call or apply:

{% highlight csharp %}
namespace test {
    class UserController {

        public constructor(private toastService:ToastService, private jsonService:JsonService) {}

        public changeName(name:string):void {
            this.updateNameAsync(name, (success) => { // Note the fat-arrow
                this.toastService('Name updated');
            });
        }

        private updateNameAsync(name:string, callback:(success:boolean) => void):void {
            // Name validation amd other stuff happens here...
            this.jsonService.updateName(name, (success:boolean):void => {   // Note the fat-arrow
                callback.apply(this, [success]);
                // Optionally callback.call(this, success);
            });
        }
    }
}
{% endhighlight %}

However, a much better way to go is to use promises rather than callbacks, preferably the [Q](http://documentup.com/kriskowal/q/) library or
the $q service in Angular, or if [worse comes to worse](http://stackoverflow.com/questions/23744612/problems-inherent-to-jquery-deferred-jquery-1-x-2-x)
using [jQuery.Deferred](https://api.jquery.com/jquery.deferred/) (though if you are using [jQuery 3](http://blog.jquery.com/2016/06/09/jquery-3-0-final-released/),
its Deferred is [Promises/A+ compliant](https://github.com/promises-aplus/promises-tests)).

The above code becomes much nicer (especially with [Generics in TypeScript](https://github.com/Microsoft/TypeScript-Handbook/blob/master/pages/Generics.md))
using promises:

{% highlight csharp %}
namespace test {
    class UserController {

        public constructor(private toastService:ToastService, private jsonService:JsonService) {}

        public changeName(name:string):void {
            this.updateNameAsync(name).then((success) => {
                this.toastService('Name updated');
            });
        }

        private updateNameAsync(name:string):Q.Promise<boolean> {
            var defer = Q.defer<boolean>();

            // Name validation amd other stuff happens here...
            this.jsonService.updateName(name, (success:boolean):void => {   // Note the fat-arrow
                defer.resolve(success);
            });

            return defer.promise;
        }

    }
}
{% endhighlight %}


#### Tip 10 - Go with the spirit of TypeScript instead of trying to trick it

One of the advantages of JavaScript and other untyped languages is that you can easily mutate variables, a string can
be come a number, or even an object.  To get this working without the TypeScript compiler yelling at you, you will need
to make these types any.  Resist that impulse and think about refactoring your code.  While it is not the worst thing
in the world to have these types (in fact I used to do a lot of tricks to make optional args work this way), it will
make it much harder for the TypeScript compiler to help you validate your work.  If you work against the spirit of TypeScript
(which is that all variables should have a type) then you create areas in your code where you cannot rely on the TypeScript
compiler to check your work.  This is kind of like having large areas of code without UnitTests, it probably works, but you
are never really sure.

For example, suppose we had the following JavaScript function that took two optional arguments:

{% highlight JavaScript %}
/**
* @param url {String}
* @param x {Number}
* @param y {Number}
* @param [size] {Number}
* @param [options] {Object}
*/
function drawSquare(url, x, y, size, options) {
    if (typeof size === 'object' || !size) {
        size = -1;
        options = size || {};
    }
    // ... Draw the square
}
{% endhighlight %}

and we converted it TypeScript

{% highlight csharp %}
function drawSquare(url:string, x:number, y:number, size?:number, options?:Object) {
    if (typeof size === 'object' || !size) {
        size = -1;
        options = size || {};
    }
    // ... Draw the square
}
{% endhighlight %}

you are going to get a warning that a number can't be converted to an object.  So either you for the type:

{% highlight csharp%}
        options = (size as any) || {}; // <!---

{% endhighlight %}

**Note: use [as any rather than (<any>size) to allow for future use of JSX](https://github.com/Microsoft/TypeScript/issues/296).**

But a better way is to go with the spirit of TypeScript and not mutate types, so instead of changing the type of arguments,
create variables in the function and assign them the proper value.

{% highlight csharp %}
function drawSquare(url:string, x:number, y:number, inSize?:number, inOptions?:Object) {
    var size:number;
    var options:Object;

    if (typeof inSize === 'object' || !inSize) {
        size = -1;
        options = size || {};
    } else {
        size = inSize;
        options = inOptions || {};
    }
    // ... Draw the square
}
{% endhighlight %}

Obviously this is a simplistic example, but I think it helps to realize that in Javascript we are no longer trying to
compress as much code into as few lines as possible, and the addition of a couple lines (and a couple variables) will
provide more readable code that doesn't force the mutation of objects.  In our code we had some pretty crazy functions
that had a large number of optional variables and huge blocks of code that checked what parameters were passed in and
which optional parameters were omitted.  We made the decision to make none of the arguments optional, and found that there
were several places where the function was being called were the handling that adjusted parameters was only working
by fluke (the values of the parameters were actually invalid but the invalid value triggered a default behavior that was
the desired value).  Another way to go (rather than optional parameters) is to use a parameters object that is strongly typed.
For the above example:

{% highlight csharp %}
interface IDrawSquareParameters {
    url:string;
    x:number;
    y:number;
    size?:number;
    options?: {
        border?: boolean;
        borderColor?: string;
        borderWidth?:number;
    }
}


function drawSquare(parameters:IDrawSquareParameters) {
    parameters.size = parameters.size || -1;
    parameters.options = parameters.options || {};
}
{% endhighlight %}

The nice thing about using a parameters interface, is that the values are checked by the compiler, but the defination of
the interface takes no space in the compiled code.

#### Tip 11 - Enjoy

I know reading over this document it appears that switching from JavaScript to TypeScript seems like a lot of work,
and to be fair to get all the benefits from TypeScript it is a fair bit of work, but you don't have to do all the work
at once and once you have TypeScript up and running you will be living and working in a better world.  You can confidently
refactor and find code usages that were more string matching in the old JavaScript world.  You know what methods are available
 for every class (and you have proper JavaScript classes before ES6 arrives in all browsers).  You know exactly what arguments
are required for each function and what is returned just through intellisense rather than having to the code for the
function you are calling.  You can use namespaces, classes, inheritance, decorators, rocket functions, and a lot of the great features of ES6/7 without
waiting for browsers to support all these features.  You also get the advantages of [DefinatelyTyped](http://definitelytyped.org/)
for older libraries.  And since TypeScript is rapidly evolving you will see future Javascript features like async/await, JSX, generators,
mixins, non-nullable types, variadic types, and tons of other [features](https://github.com/Microsoft/TypeScript/wiki/Roadmap) coming
in the near future.  I highly recommend switching to TypeScript, you will be glad you did!

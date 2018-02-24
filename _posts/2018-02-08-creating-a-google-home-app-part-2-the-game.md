---
layout: post
title: "Creating A Google Home App Part 2 - The Game"
description: "In the previous article, Creating A Google Home App, I detailed how to get a very simple Google Home App up and running.  Mostly it was about setting up the node project, the Google Actions project, but in the end you had an App that when you talked to it, it would say -- 'Hey Ma, It Worked!'.  And while it wasn't much of an achievement, but I know I felt pretty cool when I got my Google Speaker in my kitchen saying things I wanted it to say.  Somehow it felt more impressive that just having a website that dumped out HTML, and now in this article we are going to learn how to actually create something (somewhat) useful, and learn a fair bit more about the GoogleActionSDK."
category: Programming
imagefeature: blog/rpsls.png 
tags: [Google Home, Google Assistant, Google Actions, Programming, Nodejs]
featured: true
---

### Introduction

In the previous article, [Creating A Google Home App](https://agingcoder.com/programming/2018/02/04/creating-a-google-home-app/) 
I detailed how to get a very simple Google Home App up and running.  Mostly it was about setting up the node project, the Google 
Actions project, but in the end you had an App that when you talked to it, it would say -- 'Hey Ma, It Worked!'.  And while it wasn't 
much of an achievement, but I know I felt pretty cool when I got my Google Speaker in my kitchen saying things I wanted it to say.  
Somehow it felt more impressive that just having a website that dumped out HTML, and now in this article we are going to learn how to
 actually create something (somewhat) useful, and learn a fair bit more about the GoogleActionSDK.

A couple of quick notes before we jump into the application, because we are handling all of the parsing of text (Google handles 
the Text to Speech for us, and does a very impressive job of that), this does not create the cleanest possible code as we are 
stuck using default intents.  If you want to have a cleaner set of intents to map to, and not have to manually parse responses 
you might want to look at [WebHooks in DialogFlow](https://dialogflow.com/docs/fulfillment), this is not that tutorial however.

Another note, I have been messing around with Google Actions Console for a while, and sometimes it is just buggy.  I've had to 
delete projects and create fresh projects to get things to work, hence I would recommend not filling out App Information section 
of the Overview until you are ready to go for two reasons.

1. It's frustrating to fill out the App Information multiple times.
2. The App Name you choose in their is like a URL, it has to be unique and if you have to recreate your app because it is 
acting funny remember to change the old apps name BEFORE you delete it.  Also you have to wait about an hour before changing 
an apps name to be able to create a new app with that name.

Also, a quite note: Google For Business accounts seem to work, until they don't.  
I spent over an hour trying to figure out why the app would stop sending requests after the first one.  
Finally after a lot of googling, I saw someone post about how they were having a similar problem until they blew away their app 
and recreated it on a gmail account (rather than a Google for Business Account) and all my problems went away 
-- you have been warned, not all Google Accounts are equal (and surprisingly the ones you pay for are less equal),
or it could be the act of creating a new project fixed things, as I have said a couple of times sometimes the only way
to fix a project is to create a new one.

### The Code

####  Changes to the index.js file

The index.js file is not going to change a lot, basically we are going to do all of the heavy lifting in a file called rpsls.js, so in the index file add a const reference to those exported functions before we create the expressApp.


{% highlight javascript %}
    const bodyParser = require('body-parser');

    const rpsls = require('./rpsls'); // <-- Add Me

    const expressApp = express();
{% endhighlight %}

You can remove the entire mainIntentHandler function from index.js (it is going to be expanded, improved in rpsls.js).  And then we have to update our actionMap a little.


{% highlight javascript %}
    // actionMap.set(actionApp.StandardIntents.MAIN, mainIntentHandler); COMMENT ME OUT OR REMOVE ME

    actionMap.set(actionApp.StandardIntents.MAIN,  rpsls.mainIntentHandler);
    actionMap.set(actionApp.StandardIntents.OPTION, rpsls.optionIntentHandler);
    actionMap.set(actionApp.StandardIntents.TEXT,  rpsls.textIntentHandler);
{% endhighlight %}

Ok, so we have two new standard Intents that we have added.  And that is all the changes we need to make to index.js.  

Lets quickly go over what we have done.  We've removed our old main handler and added one that we are going to add to the rpsls.js file.
We have also added two new handlers that are used when the user enters responses to our asks.  

The OPTION standard intent handles lists (and carousels, but since we are mainly focused on Google Home, we are going use the simple list for our demo).  

The TEXT standard intent gives us raw text to parse, which allows the user to text free form (thus be prepared to handle anything).

#### The rpsls.js file

Create a new file in the main directory called rpsls.js.  It is going to have three exported functions, so lets create those first (this will enable us
to run the app even though it isn't complete because all the pieces will at least be in place).

{% highlight javascript %}
function mainIntentHandler(app) {
    console.log('MAIN intent triggered.');
}

function optionIntentHandler(app) {
    console.log('OPTION intent triggered.');
}

function textIntentHandler(app) {
    console.log('TEXT intent triggered.');
}

module.exports = {
    mainIntentHandler: mainIntentHandler,
    optionIntentHandler: optionIntentHandler,
    textIntentHandler: textIntentHandler
};
{% endhighlight %} 

#### The Main Intent Handler

Just like our mainIntentHandler in previous version, all intents that are mapped from the main SDK get an instance of the
actionSDKApp object passed to them.  This is used for many things, and is pretty well documented at 
[https://developers.google.com/actions/reference/nodejs/ActionsSdkApp](https://developers.google.com/actions/reference/nodejs/ActionsSdkApp), and 
[https://developers.google.com/actions/reference/nodejs/AssistantApp](https://developers.google.com/actions/reference/nodejs/AssistantApp) -- it is 
important to note that ActionsSdkApp is a subclass of the AssistantApp.  The first thing we are going to do welcome our user and give them the option
 to either get instructions for Rock, Paper, Scissors, Lizard, Spock or play the game.  We could do this with text parsing, but since there are only two
  possible options this seems like the perfect place to ask for a list.   So lets update our mainIntentHandler:

{% highlight javascript %}
function mainIntentHandler(app) {
    console.log('MAIN intent triggered.');
    let list = app.buildList('Start Game or Instructions');
    list.addItems([
        app.buildOptionItem('Start Game', ['Start', 'New Game']).setTitle('Start Game'),
        app.buildOptionItem('Instructions', ['Help', 'Read Instructions', 'Tell Me Instructions', 
            'Repeat Instructions']).setTitle('Instructions')
    ]);
    app.askWithList(app.buildInputPrompt(true,
            `<speak>
              <p>
                  <s>Welcome to Rock, Paper, Scissors, Lizard, Spock.</s>
                  <s>If you need instructions, say Instructions.</s>
                  <s>To play the game, say Start Game</s>
              </p>
            </speak>`, ['Say Instructions or Start Game']), list);

}
{% endhighlight %}

First we are going to create a list of options we are going to present our user.  We do with the 
[buildList](https://developers.google.com/actions/reference/nodejs/AssistantApp#buildList) method of the ActionSdkApp, 
build list takes an optional title.  This obviously will not be visible on the Google Home, but it will show up on your phone.  
Plus it can be useful debug information, so we will include it.  Next we add items to the list, each item is constructed 
with the [buildOptionItem](https://developers.google.com/actions/reference/nodejs/AssistantApp#buildOptionItem) method.  
The buildOptionItem takes a key, and a list of synonyms.  Also, we are setting the title of the optionItem (optionItem methods 
and the buildOptionItem method are chainable).  Now that we have that list, we are ready to 
[askWithList](https://developers.google.com/actions/reference/nodejs/ActionsSdkApp#askWithList).  

The askWithList method, takes an InputPrompt and a list.  The buildInputPrompt takes an option 
(whether or not the text is [SSML](https://en.wikipedia.org/wiki/Speech_Synthesis_Markup_Language)), some text (either SSML or plain text),
 and a list of messages that can be output if the user fails to enter any text.  If you want the ability to properly read things fractions, 
 numbers, and have more control of the timing of the speech I would recommend producing your text in SSML.  Our SSML is very simple here, 
 we create a single paragraph (```<p>```), in which we have three sentences (```<s>```).

OK, now that we have a slightly better opening for application, lets make sure it worked.  The first thing we have to do is restart the app

```node index.js```

If there are no errors, then fire up ngrok, if ngrok is already running with the same url as last time, skip this step and the following 2 steps.

```ngrok http 5050```  

Next we need to change the url for our conversation in in rpsls.json.

```"url": "https://2f29038a.ngrok.io",```

And finally we have to update gactions:

```gactions update --action_package rpsls.json  --project rpsls-XXXXX```

Go to the gactions console and test the app:

<img src="/img/google-home/2-step1.png" style="border: 1px solid #000; margin: 10px auto 0" />

Note, if you are getting "My Test App Is Not Responding Right Now", try going to the Overview, and click on "Test Draft" 

<img src="/img/google-home/2-step2.png" style="border: 1px solid #000; margin: 10px auto 0" />

### The List Intent Handler

Of course, nothing else will work, so lets parse the response we are going to get.  This is handled by the actionApp.StandardIntents.OPTION, that we saw earlier.

{% highlight javascript %}
// React to list or carousel selection
function optionIntentHandler(app) {
    console.log('OPTION intent triggered.');
    const param = app.getSelectedOption();
    if (param === 'Instructions') {
        readInstructions(app);
    } else if (param === 'Start Game' || param === 'Again') {
        startGame(app);
    } else if (param === 'End') {
        app.tell('Bye');
    }
}
{% endhighlight %}

The option intent handler is also rather simple, the key thing is that to get text from an option, we use the getSelectedOption method.  This method will give
us back the exact string we used as the key when we built the list (even if the user types in 'start game' we will get back 'Start Game').  In fact, since we
need the exact string, lets replace all the string instances with constants.  At the top of the rpsls.js lets add the following constants:

{% highlight javascript %}
const OPTION_INSTRUCTIONS = 'Instructions';
const OPTION_START_GAME = 'Start Game';
const OPTION_AGAIN = 'Again';
const OPTION_END = 'End';
{% endhighlight %}

and lets fix the main intent, by replacing the list with said options:

{% highlight javascript %}
list.addItems([
    app.buildOptionItem(OPTION_START_GAME, ['Start', 'New Game']).setTitle(OPTION_START_GAME),
    app.buildOptionItem(OPTION_INSTRUCTIONS, 
        ['Help', 'Read Instructions', 'Tell Me Instructions', 'Repeat Instructions']
    ).setTitle(OPTION_INSTRUCTIONS)
])
{% endhighlight %}

and clean up the optionIntentHandler:

{% highlight javascript %}
// React to list or carousel selection
function optionIntentHandler(app) {
    console.log('OPTION intent triggered.');
    const param = app.getSelectedOption();
    if (param === OPTION_INSTRUCTIONS) {
        readInstructions(app);
    } else if (param === OPTION_START_GAME || param === OPTION_AGAIN) {
        startGame(app);
    } else if (param === OPTION_END) {
        app.tell('Bye');
    }
}
{% endhighlight %}

We will be using OPTION_AGAIN and OPTION_END when the game is over, so you can ignore those for now.  What happens when the Google Home
user responds with something that is not in the list?   Instead of firing the list intent handler, the app fires the text intent handler, 
which we will see [later in this tutorial](#the-text-intent-handler), so we will handle invalid choices in that portion of code.

#### Reading the Instructions

Reading the instructions is similar to our main intent, we create the same list (eventually we can factor out this
duplicated code and turn creating a list into a function), and give the user the instructions in an input prompt.  To
have the speech sound more natural I have added short breaks after each instruction sentence.  The break can be inside
or outside the [sentence](https://www.w3.org/TR/speech-synthesis11/), quoting from the W3C recommendation: 
<blockquote>The s element can only contain text to be rendered and the following elements: audio, break, emphasis, lang, lookup, mark, phoneme, prosody, say-as, sub, token, voice, w.</blockquote> 

{% highlight javascript %}
function readInstructions(app) {
    console.log('Read Instructions.');
    let list = app.buildList('Start Game or Instructions');
    list.addItems([
        app.buildOptionItem(OPTION_START_GAME, ['Start', 'New Game']).setTitle(OPTION_START_GAME),
        app.buildOptionItem(OPTION_INSTRUCTIONS, 
            ['Help', 'Read Instructions', 'Tell Me Instructions', 'Repeat Instructions']
        ).setTitle(OPTION_INSTRUCTIONS)
    ])
    app.askWithList(app.buildInputPrompt(true,
    `<speak>
      <p>
        <s>Scissors cuts Paper.</s><break time=".3s"/>
        <s>Paper covers Rock.</s><break time=".5s"/>
        <s>Rock crushes Lizard.</s><break time=".3s"/>
        <s>Lizard poisons Spock.</s><break time=".3s"/>
        <s>Spock smashes Scissors.</s><break time=".3s"/>
        <s>Scissors decapitates Lizard.</s><break time=".3s"/>
        <s>Lizard eats Paper.</s><break time=".3s"/>
        <s>Paper disproves Spock.</s><break time=".3s"/>
        <s>Spock vaporizes Rock.</s><break time=".7s"/>
        <s>(and as it always has), Rock crushes Scissors</s>
      </p>
      <break time="1s"/>
      <p>
        <s>To play the game, say Start Game</s>
        <s>To repeat the instructions, say instructions</s>
      </p>
    </speak>`), list);
}  
{% endhighlight %}

Once we done, you should feel free to play with elements like [prosody](https://www.w3.org/TR/speech-synthesis11/#edef_prosody), 
[say-as](https://www.w3.org/TR/speech-synthesis11/#edef_say-as), [emphasis](https://www.w3.org/TR/speech-synthesis11/#edef_emphasis),
[phoneme](https://www.w3.org/TR/speech-synthesis11/#edef_phoneme), and even the [audio](https://www.w3.org/TR/speech-synthesis11/#edef_audio)
tag to become comfortable with SSML.

To hear our instructions, restart the app, go back to the simulator, restart the interaction (if you are in bad a state you can
always type 'quit' in the simulator and then 'Talk to My Test App' to start it again), and choose instructions from the main interaction.

#### Starting the Game

To code in the startGame function, add 

{% highlight javascript %}
function startGame(app) {
    app.ask(app.buildInputPrompt(true,
   `<speak>
      <p>
        <s>Do you pick Rock, Paper, Scissors, Lizard or Spock</s>
      </p>
    </speak>`));
}
{% endhighlight %}

When starting a game, we aren't asking for a list anymore, we are asking for a text input (the difference between askWithList and ask is that
the response to an ask fires the actionApp.StandardIntents.TEXT intent).  While we easily could have used a list here (there are only 5
possible answers), I did want to demonstrate the difference between handling a list and handling a text response, plus our option
handler would have gotten pretty big.

#### The Text Intent Handler 
{: #the-text-intent-handler} 

Like the option intent handler, the text intent handler is pretty simple.  We grab the rawInput from the app, then we are going
to make sure we have valid input (being a rock, paper, scissors, lizard or spock) and pass that on to main game engine (returnResults).   

{% highlight javascript %}
function textIntentHandler(app) {
    console.log('TEXT intent triggered.');
    const rawInput = app.getRawInput();
    let res;
    if (res = rawInput.match(/^\s*(rock|paper|scissors|lizard|spock)\s*$/i)) {
        returnResults(app, res[1].toLowerCase());
    } else {
        app.ask(app.buildInputPrompt(true,
   `<speak>
      <p>
        <s>${rawInput} is not a valid choice.</s>
        <s>Do you pick Rock, Paper, Scissors, Lizard or Spock</s>
      </p>
    </speak>`));
    }
}
{% endhighlight %}

Currently we are not keeping track of any state, and we will wait until the next article to start maintaining state, so we
don't know here if the user has actually started the game or whether this was an invalid answer to the initial question of 
play game or instructions.  If the user had chosen an invalid list item (not start game or instructions) they are going to get
a nonsensical answer but, like I said, we will fix that in the next article.  Also note that we are not controlling the input
in the same way as we do with askWithList so we force our input to lower case for parsing.

#### The Game Engine

The returnResults game engine is overly long (we will improve it in the next article), but simple piece of code that randomly 
generates a choice of Rock, Paper, Scissors, Lizard or Spock and tells the user if they have won or not.  It plays fairly,
though there should probably be some added weight to throwing Rock or Spock more often.  At the top of the rpsls.js file, add the 
following constant:

{% highlight javascript %}
const CHOICE_ARRAY = ['rock','paper','scissors','lizard','spock'];
{% endhighlight %}

Next add the returnResults function.

{% highlight javascript %}
function returnResults(app, userChoice) {
    const computerChoice = CHOICE_ARRAY[Math.floor(Math.random() * CHOICE_ARRAY.length)];
    if (computerChoice === userChoice) {
        app.ask(app.buildInputPrompt(true,
    `<speak>
          <p>
            <s>I also picked ${userChoice}.</s>
            <s>Try again, do you pick Rock, Paper, Scissors, Lizard or Spock</s>
          </p>
        </speak>`));
    } else {
        let win = false;
        let result = '';
        if (userChoice === 'rock') {
            if (computerChoice === 'spock') {
                result = 'Spock vaporizes Rock';
            } else if (computerChoice === 'paper') {
                result = 'Paper covers Rocks';
            } else if (computerChoice === 'lizard') {
                win = true;
                result = 'Rock crushes Lizard'
            } else if (computerChoice === 'scissors') {
                win = true;
                result = 'as always, Rock crushes scissors';
            }
        } else if (userChoice === 'paper') {
            if (computerChoice === 'spock') {
                win = true;
                result = 'Paper disproves Spock';
            } else if (computerChoice === 'rock') {
                win = true;
                result = 'Paper covers Rocks';
            } else if (computerChoice === 'lizard') {
                result = 'Lizard eats Paper'
            } else if (computerChoice === 'scissors') {
                result = 'Scissors cuts Paper';
            }
        } else if (userChoice === 'scissors') {
            if (computerChoice === 'spock') {
                result = 'Spock smashes Scissors';
            } else if (computerChoice === 'rock') {
                result = 'as always, Rock crushes scissors';
            } else if (computerChoice === 'lizard') {
                win = true;
                result = 'Scissors decapitates Lizard'
            } else if (computerChoice === 'paper') {
                win = true;
                result = 'Scissors cuts Paper';
            }
        } else if (userChoice === 'lizard') {
            if (computerChoice === 'paper') {
                win = true;
                result = 'Lizard eats Paper';
            } else if (computerChoice === 'rock') {
                result = 'Rock crushes Lizard';
            } else if (computerChoice === 'spock') {
                win = true;
                result = 'Lizard poisons Spock'
            } else if (computerChoice === 'scissors') {
                result = 'Scissors decapitates Lizard';
            }
        } else if (userChoice === 'spock') {
            if (computerChoice === 'paper') {
                result = 'Paper disproves Spock';
            } else if (computerChoice === 'rock') {
                win = true;
                result = 'Spock vaporizes Rock';
            } else if (computerChoice === 'lizard') {
                result = 'Lizard poisons Spock'
            } else if (computerChoice === 'scissors') {
                win = true;
                result = 'Spock smashes Scissors';
            }
        } else {
            console.error('Impossible choice: ' + userChoice);
            app.ask('Something has gone wrong, you picked: ' + userChoice);
            return;
        }

        let list = app.buildList('Start Game or Instructions');
        list.addItems([
            app.buildOptionItem(OPTION_AGAIN, ['Start', 'Yes']).setTitle('Again'),
            app.buildOptionItem(OPTION_END, ['Stop', 'No']).setTitle('End')
        ]);

        const message = '<s>' + result + '</s>' + (win ? '<s>You Won!</s>' : '<s>You lost.</s>');

        app.askWithList(app.buildInputPrompt(true,
                `<speak>
          <p>
              ${message}
              <s>To play again, say again.</s>
              <s>To quit say end.</s>
          </p>
        </speak>`), list);
    }
}
{% endhighlight %}

It's long code, but it is simple code and was written for ease of readability, not for elegance (we will convert it into a
tighter array based engine next article).  There isn't anything new here, we determine the winner, build a list of whether
we want to play again or end.  Inform the user of whether they won or lost.  

Now that everything is done, lets start up the simulator again.
  
<img src="/img/google-home/2-step3.png" style="border: 1px solid #000; margin: 10px auto 0" />

Now that it is working in the simulator, try it on your Google Home device.  Also play around with SSML, and the various
inflections to improve the feel of our little game.

If you want to download the code for the state that it is in, it is [TAG PART_2_STEP_1](https://github.com/kriserickson/google-actions-rpsls/tree/PART_2_STEP_1) on
GitHub: <a href="https://github.com/kriserickson/google-actions-rpsls/tree/PART_2_STEP_1">https://github.com/kriserickson/google-actions-rpsls/tree/PART_2_STEP_1</a>. 

Next article we will start keeping score, add a login to our app, add account linking, and finish off some of the rough
edges in the app.    

As always, if you see any bugs, or have suggestions feel free to do so either in the comments below, or as an issue or pull request in the 
 [GitHub repo](https://github.com/kriserickson/google-actions-rpsls).
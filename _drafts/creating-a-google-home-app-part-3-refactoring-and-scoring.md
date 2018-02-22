---
layout: post
title: "Creating A Google Home App Part 3 - Refactoring and Scoring"
description: ""
category: Programming
imagefeature: blog/google-home.jpg 
tags: [Google Home,Programming, Nodejs]
featured: true
---
### Introduction

**Note:** This is the third article in a probably four part series, it will not make much sense without reading the other two:

* [Creating A Google Home App](https://agingcoder.com/programming/2018/02/04/creating-a-google-home-app/) where we get a very simple Google Home App up and running.
* [Creating A Google Home App Part 2 - The Game](https://agingcoder.com/programming/2018/02/08/creating-a-google-home-app-part-2-the-game/) where we turn that simple app into a game.

In the previous [article](https://agingcoder.com/programming/2018/02/08/creating-a-google-home-app-part-2-the-game/) we converted our very simple app into a version of Rock, Paper, Scissors, Lizard, Spock.  In this article we will refactor our game, and then add scoring so the app will keep track of your wins and losses (initially it will be per session, and eventually we will have it keep track for all time).

As we stated in the previous article, our if else engine for determining game winners was very ugly.  Let's replace it
with an array based engine, that will clean it up, reduce the amount of code, and remove a ton of hard coded strings.  First we will create a pseudo enum with Object.freeze that has all of the 10 possible combinations of two people playing Rock, Paper, Scissors, Lizard, Spock (place this at the top of the rpsls.js file, after the options):

{% highlight javascript %}
const GAME_CHOICES = Object.freeze({SCISSORS_VS_PAPER : 0, PAPER_VS_ROCK: 1, ROCK_VS_LIZARD: 2, LIZARD_VS_SPOCK: 3,
    SPOCK_VS_SCISSOR: 4, SCISSOR_VS_LIZARD: 5, LIZARD_VS_PAPER: 6, PAPER_VS_SPOCK: 7, SPOCK_VS_ROCK: 8, ROCK_VS_SCISSOR: 9});
{% endhighlight %}
    
If you haven't seen [Object.freeze](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze) before it is a new feature added to JavaScript 5.1, that allows us to force immutable objects (in case you hadn't noticed in the past, const isn't really const as
you can always add to or remove items from an array or object, with Object.freeze you will get an exception thrown if you try to mutate a frozen object).  Javascript doesn't really have enums, but this is pretty close.  Next we are going to create an array of text outcomes based on our 'enumeration' (this also goes near the top of the rpsls.js file):

{% highlight javascript %}
const OUTCOME_DESCRIPTIONS = {
    [GAME_CHOICES.SCISSORS_VS_PAPER] : 'Scissors cuts Paper.',
    [GAME_CHOICES.SCISSOR_VS_LIZARD]: 'Scissors decapitates Lizard.',
    [GAME_CHOICES.PAPER_VS_ROCK] : 'Paper covers Rock.',
    [GAME_CHOICES.PAPER_VS_SPOCK]: 'Paper disproves Spock.',
    [GAME_CHOICES.LIZARD_VS_SPOCK] : 'Lizard poisons Spock',
    [GAME_CHOICES.LIZARD_VS_PAPER]: 'Lizard eats Paper.',
    [GAME_CHOICES.SPOCK_VS_SCISSOR] : 'Spock smashes Scissors.',
    [GAME_CHOICES.SPOCK_VS_ROCK]: 'Spock vaporizes Rock.',
    [GAME_CHOICES.ROCK_VS_LIZARD] :'Rock crushes Lizard',
    [GAME_CHOICES.ROCK_VS_SCISSOR]: '(and as it always has), Rock crushes Scissors.'
};
{% endhighlight %}

This way instead of duplicating our results like we previously were, we can use the same text for either computer beating the player, or losing to the player.  Of course we could freeze this text too, as it won't change, but for reasons only known to the author at the time he wrote the code, we have decided not to.

Next, instead of repeating strings throughout the code (and having the chance of misspelling scissors as scisors or sissors somewhere), we turn all of the user choices into another frozen Object Collection (place this at the top of the rpsls.js file as well):

{% highlight javascript %}
const CHOICE_NAMES = Object.freeze({ROCK: 'rock', PAPER: 'paper', SCISSOR: 'scissors', LIZARD: 'lizard', SPOCK: 'spock'});
{% endhighlight %}

Next we create out choice matrix, this basically produces all the possible choices and contains their output.  The users choice is the first part of the key, and the computer's choice the second.  Each element in the collection contains an outcome which is a string, and win -- a boolean that indicates whether the player won or lost.  We are placing this matrix again near the top of the rpsls.js file:

{% highlight javascript %}
const CHOICE_MATRIX = {
    [CHOICE_NAMES.ROCK + CHOICE_NAMES.SCISSOR]: {outcome: OUTCOME_DESCRIPTIONS[GAME_CHOICES.ROCK_VS_SCISSOR], win: true},
    [CHOICE_NAMES.ROCK + CHOICE_NAMES.LIZARD]: {outcome: OUTCOME_DESCRIPTIONS[GAME_CHOICES.ROCK_VS_LIZARD], win: true},
    [CHOICE_NAMES.ROCK + CHOICE_NAMES.PAPER]: {outcome: OUTCOME_DESCRIPTIONS[GAME_CHOICES.PAPER_VS_ROCK], win: false},
    [CHOICE_NAMES.ROCK + CHOICE_NAMES.SPOCK]: {outcome: OUTCOME_DESCRIPTIONS[GAME_CHOICES.SPOCK_VS_ROCK], win: false},

    [CHOICE_NAMES.PAPER + CHOICE_NAMES.ROCK]: {outcome: OUTCOME_DESCRIPTIONS[GAME_CHOICES.PAPER_VS_ROCK], win: true},
    [CHOICE_NAMES.PAPER + CHOICE_NAMES.SPOCK]: {outcome: OUTCOME_DESCRIPTIONS[GAME_CHOICES.PAPER_VS_SPOCK], win: true},
    [CHOICE_NAMES.PAPER + CHOICE_NAMES.SCISSOR]: {outcome: OUTCOME_DESCRIPTIONS[GAME_CHOICES.SCISSORS_VS_PAPER], win: false},
    [CHOICE_NAMES.PAPER + CHOICE_NAMES.LIZARD]: {outcome: OUTCOME_DESCRIPTIONS[GAME_CHOICES.LIZARD_VS_PAPER], win: false},

    [CHOICE_NAMES.SCISSOR + CHOICE_NAMES.PAPER]: {outcome: OUTCOME_DESCRIPTIONS[GAME_CHOICES.SCISSORS_VS_PAPER], win: true},
    [CHOICE_NAMES.SCISSOR + CHOICE_NAMES.LIZARD]: {outcome: OUTCOME_DESCRIPTIONS[GAME_CHOICES.SCISSOR_VS_LIZARD], win: true},
    [CHOICE_NAMES.SCISSOR + CHOICE_NAMES.ROCK]: {outcome: OUTCOME_DESCRIPTIONS[GAME_CHOICES.ROCK_VS_SCISSOR], win: false},
    [CHOICE_NAMES.SCISSOR + CHOICE_NAMES.SPOCK]: {outcome: OUTCOME_DESCRIPTIONS[GAME_CHOICES.SPOCK_VS_SCISSOR], win: false},

    [CHOICE_NAMES.LIZARD + CHOICE_NAMES.SPOCK]: {outcome: OUTCOME_DESCRIPTIONS[GAME_CHOICES.LIZARD_VS_SPOCK], win: true},
    [CHOICE_NAMES.LIZARD + CHOICE_NAMES.PAPER]: {outcome: OUTCOME_DESCRIPTIONS[GAME_CHOICES.LIZARD_VS_PAPER], win: true},
    [CHOICE_NAMES.LIZARD + CHOICE_NAMES.ROCK]: {outcome: OUTCOME_DESCRIPTIONS[GAME_CHOICES.ROCK_VS_LIZARD], win: false},
    [CHOICE_NAMES.LIZARD + CHOICE_NAMES.SCISSOR]: {outcome: OUTCOME_DESCRIPTIONS[GAME_CHOICES.SCISSOR_VS_LIZARD], win: false},

    [CHOICE_NAMES.SPOCK + CHOICE_NAMES.SCISSOR]: {outcome: OUTCOME_DESCRIPTIONS[GAME_CHOICES.SPOCK_VS_SCISSOR], win: true},
    [CHOICE_NAMES.SPOCK + CHOICE_NAMES.ROCK]: {outcome: OUTCOME_DESCRIPTIONS[GAME_CHOICES.SPOCK_VS_ROCK], win: true},
    [CHOICE_NAMES.SPOCK + CHOICE_NAMES.PAPER]: {outcome: OUTCOME_DESCRIPTIONS[GAME_CHOICES.PAPER_VS_SPOCK], win: false},
    [CHOICE_NAMES.SPOCK + CHOICE_NAMES.LIZARD]: {outcome: OUTCOME_DESCRIPTIONS[GAME_CHOICES.LIZARD_VS_SPOCK], win: false},

};
{% endhighlight %}

Now we can greatly simplify our returnResults code: 

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
        const result = CHOICE_MATRIX[userChoice + computerChoice];
        if (!userChoice) {
            console.error('Impossible choice: ' + userChoice);
            app.ask('Something has gone wrong, you picked: ' + userChoice);
            return;
        }

        let list = app.buildList('Start Game or Instructions');
        list.addItems([
            app.buildOptionItem(OPTION_AGAIN, ['Start', 'Yes']).setTitle('Again'),
            app.buildOptionItem(OPTION_END, ['Stop', 'No']).setTitle('End')
        ]);

        const message = '<s>' + result.outcome + '</s>' + (result.win ? '<s>You Won!</s>' : '<s>You lost.</s>');

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

To see exactly what this looks like, you can look at the tag: [PART_3_STEP_1](https://github.com/kriserickson/google-actions-rpsls/tree/PART_3_STEP_1).  
Nothing here is particularly complicated, and it really has nothing to do with Google Actions so let's skip along to our next change.

Next we are going to add per session scoring, as well as a bit of state so that we can provide better responses when we don't get
an answer we want.  Our game state is going to be an enumeration, and there are basically 3 states: Initial, StartGame (when we are 
waiting for the user to choose Rock/Paper/Scissors/Lizard/Spock), and EndGame when we are waiting to see if they want to play again.  Let's 
create our version of an enumeration and place it at the top of the rpsls.js file:

{% highlight javascript %}
const STATES = Object.freeze({INITIAL_STATE: 0, START_GAME: 1, END_GAME: 2});
{% endhighlight %}

Next we need to keep the state somewhere, and this is done by adding the state to to every ask method (and askWIthList method).  If you don't
pass the state, it will revert to null so remember you have to set it everywhere, even if you don't change it!  The other thing to realize about 
state is that you are passing it back to the Google Servers and the Google Servers are passing it back to you with every request, so even though
you can store fairly large objects in it, it may not be the most efficient way of doing things (you might want to store large objects
in a local database instead).

The first place to add the state is in our mainIntentHandler.  Since this is only executed when a user begins their conversation with our game, we
can completely reset the state (including setting their wins and losses for this conversation to 0 -- we will use these wins and losses later in the article).

{% highlight javascript %}
function mainIntentHandler(app) {
    console.log('MAIN intent triggered.');
    const list = getStartList(app);
    app.askWithList(app.buildInputPrompt(true,
            `<speak>
              <p>
                  <s>Welcome to Rock, Paper, Scissors, Lizard, Spock.</s>
                  <s>If you need instructions, say Instructions.</s>
                  <s>To play the game, say Start Game</s>
              </p>
            </speak>`, ['Say Instructions or Start Game']), list, {state: STATES.INITIAL_STATE, wins: 0, loss: 0});

}
{% endhighlight %}

the only change in this function is the addition of the state at the end:

{% highlight html %}
</speak>`, ['Say Instructions or Start Game']), list);
{% endhighlight %}

becomes:            

{% highlight html%}
</speak>`, ['Say Instructions or Start Game']), list, {state: STATES.INITIAL_STATE, wins: 0, loss: 0});
{% endhighlight %} 

Now we have to 
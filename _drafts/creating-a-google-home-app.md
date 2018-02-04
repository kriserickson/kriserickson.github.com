---
layout: post
title: "Creating A Google Home App"
description: ""
category: Programming
imagefeature: blog/google-home.jpg 
tags: [Google Home,Programming, Nodejs]
featured: true
---
## Introduction

A while ago I got an email from a [Recipe Folder](https://recipe-folder.com) user asking how to get the Google Home
integration working with Recipe Folder.  I have no idea why they thought that there was an integration, but it got me
thinking, maybe I should add one.  I hadn't looked at [Google Home](https://en.wikipedia.org/wiki/Google_Home) or
[Amazon Alexa](https://en.wikipedia.org/wiki/Amazon_Alexa) development before, but I thought it might be fun to add
at least Google Home integration (I own a Google Home but not an Alexa yet) to Recipe Folder.  So I responded to the
user saying that there was currently no integration but it was something that I was going to look into.

So I started looking into writing a Google Home app.  A bit of research, and I discovered that you don't really write
Google Home app's, but you write [Google Actions](https://developers.google.com/actions/) that run on any of the Google Assistants (the Google Home being one,
but also there is an assistant built into all modern Android Phones and Tablets).  Most of the tutorials that I 
discovered were built around [api.ai](https://dialogflow.com/) which is now called dialogflow, and used Google
Cloud platform to run.  I needed access to all the data on my own servers, so I wanted to write a stand-alone that didn't
require outside services (other than the Google Action API, obviously).  While there were some example apps from
Google in the [Actions of Google Github Page](https://github.com/actions-on-google), these mostly seemed to be using
Firebase or Google cloud, so I figured that someone should write a simple tutorial on how to get a Google Action
running on your own server from nothing.  We are going to write a very simple game you can quickly play with your
Google Assistant, [Rock, Paper, Sicissors, Lizard, Spock](http://bigbangtheory.wikia.com/wiki/Rock_Paper_Scissors_Lizard_Spock) that
keeps track of your score.  To this end we are going to include OAuth, so we can store some information (and
because one of the larger hassles I had writing my integration was OAuth integration).

## Required Tooling

We are going to do this in nodejs, using the [Action on Google Node Client Library](https://github.com/actions-on-google/actions-on-google-nodejs),
[ngrok.io](ngrok.io) to provide a tunnel from the open web, to our application.  In the end, we will us [MongoDb](https://www.mongodb.com/) to store 
that user login and the score from the games.  The web server that servers both the JSON, and the login web pages is going to be Express, and we will be using modern
Javascript so you will need NodeJS at least 8 installed.  The more OAuth and Mongo is coming in a later installment, so
for now just make sure that you have the following installed:

1. [NodeJS LTS](https://nodejs.org/en/) (8.9.4 at the time of writing this, but feel free to go with 9.5 which is the current).
2. [NGrok client](https://ngrok.com/download) and have that available on your path.
3. [GActions CLI](https://developers.google.com/actions/tools/gactions-cli) and have that available on your path.

I'm doing all of this on Windows, but it will certainly work on OSX or Linux.  I'm also using [WebStorm](https://www.jetbrains.com/webstorm/), 
but any editor can be used, however I recommend one like WebStorm or [Visual Studio Code](https://code.visualstudio.com/) where you 
can debug in the same IDE that you are editing in but there are [relatively clear instructions](https://nodejs.org/en/docs/inspector/) on how to get up and debugging on the NodeJS site.

## Getting Started

### Package.json

First thing we are going to do is make a ```package.json``` file.  

{% highlight json %}
{
    "name": "google-actions-rpsls",
    "description": "Rock Paper Scissors Lizard Spock as a Google Action",
    "version": "0.0.1",
    "dependencies": {
        "actions-on-google": "^1.7.0",
        "express": "^4.16.2",
        "body-parser": "^1.18.2",
        "ejs": "^2.5.7",
        "mongoose": "~4.13.6"
    },     
    "scripts": {
        "start": "node index.js"
    }
}
{% endhighlight %} 

Since there are no comments in JSON, let's go through the various dependencies.  

#### Actions on Google

Actions-on-google is the library from Google that is going to allow us to quickly communicate with Google Actions without having to manually parse all the input from Google Action, and having to write all the JSON responses.  It provides a fairly nice, and [relatively well documented](https://developers.google.com/actions/reference/nodejs/AssistantApp) API.

#### Express

Although actions-on-google appears to be designed for the [Google Cloud Platform Http Functions](https://cloud.google.com/functions/docs/writing/http), according to documention, the Google Cloud Platform have the same properties as the ExpressJS [Request](http://expressjs.com/en/4x/api.html#req) and [Response](http://expressjs.com/en/4x/api.html#res) objects.  Thus instead of installing the Google Cloud Platform simulator, or running on the Google Cloud Platform we can use [ExpressJS](http://expressjs.com) instead.  

#### Body Parser

In version 4 of Express, it was componentized.  Body parser allow reading of the HTTP Posts and placing their contents in req.body, there are a lot of other
enhancements and niceties (serve-favicon, compression, session handling, etc) that could be added to improve the app but we'll leave those as exercises for the user to keep the code as simple as possible.

#### Ejs

We are going to need a login page eventually, and I am using [EJS](http://ejs.co/) as the templating engine, we won't need it until a couple of articles down the line, but lets set up the package.json now.

#### Mongoose      
  
Eventually we are going store our user accounts in Mongo, and [Mongoose](http://mongoosejs.com/) is nice [ORM](https://en.wikipedia.org/wiki/Object-relational_mapping) wrapper around Mongo.

### RPSLS.json

Since our app is Rock Paper Lizard Spock we are going to use the acronym rpsls all over the place.  The first place we are going to do that is for the project.json file for Google Actions (or gactions).  Create a file ```rpsls.json``` and populate it with:

{% highlight json %}
{
  "actions": [
    {
      "description": "RPSLS Welcome Intent",
      "name": "MAIN",
      "fulfillment": {
        "conversationName": "main"
      },
      "intent": {
        "name": "actions.intent.MAIN"
      }  
    }
  ],
  "conversations": {
    "main": {
      "name": "main",
      "url": "https://CHANGE-ME.ngrok.io",
      "fulfillmentApiVersion": 2
    }
  }
}
{% endhighlight %}   

Note the CHANGE-ME in the conversations, eventually when we get your NGROK connection setup, you will have to change that URL.  We are also going to be adding authentication to this file eventually but for now this will do.  This file is currently divided into 2 sections, actions and conversations and only describes one action.  The actions described in [ActionPackage](https://developers.google.com/actions/reference/rest/Shared.Types/ActionPackage) are actions that are available without having started a conversation (we will code other Actions later, but they will not need to be described in the actions file since they are only available once a conversation is started).  Each action must have a name, and should have an intent, a fulfillment and a description -- though according to the documentation they do not have to if the name is a [built-in intent](https://developers.google.com/actions/reference/rest/intents), for example action.intent.MAIN.  The fulfillment must have a field conversationName, and that has to point to a name in the conversations section.  

The conversations section has a collection of conversations, which have a name, a url and fulfillmentApiVersion.  Make sure the name of the conversation matches the collection name, and the fulfillmentApiVersion is set to 2 (Api 1 was very different, and will not be supported much longer and doesn't work with actions-on-google npm module).

### Set Up A Project

Go to the "Actions on Google Console" by going to [https://console.actions.google.com/](https://console.actions.google.com/).   

<img src="/img/google-home/step1.png" style="border: 1px solid #000; margin: 10px auto 0" />

Click on Add/Import Project, and call it rpsls.  Click on Create Project.

<img src="/img/google-home/step2.png" style="border: 1px solid #000; margin: 10px auto 0" />

Now click on the "Actions SDK" build button:

<img src="/img/google-home/step3.png" style="border: 1px solid #000; margin: 10px auto 0" />

And you will see that your project has been created.

<img src="/img/google-home/step4.png" style="border: 1px solid #000; margin: 10px auto 0" />

Now copy the piece of text from the second step and paste it into a command prompt in the directory where you created the ```rpsls.json``` and ```package.json```.  It should look something like:

```gactions update --action_package PACKAGE_NAME --project rpsls-74009```

Where the 74009 will be a unique number assigned to you by Google.  Replace PACKAGE_NAME with rpsls.json and hit enter:

```gactions update --action_package rpsls.json  --project rpsls-74009```

If everything goes right, you will be told:

```
Gactions needs access to your Google account. Please copy & paste the URL below into a web browser and follow the instructions there. Then copy and paste the authorization code from the browser back here.
Visit this URL:
 https://accounts.google.com/o/oauth2/auth?access_type=offline&c.....
```

Once you have visited the URL paste the code into the command prompt and your  




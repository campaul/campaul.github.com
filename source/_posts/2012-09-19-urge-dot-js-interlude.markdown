---
layout: post
title: "Urge.js Interlude"
date: 2012-09-19 01:04
comments: true
categories: [Video Games, JavaScript, HTML5, Urge.js]
---

In my [last post](/blog/2012/09/03/creating-a-video-game-from-scratch-part-1/) I introduced [Urge.js](https://github.com/campaul/urge.js), a simple game engine I am building as part of a series on creating a video game. Unfortunately I haven't had the time to create the next screencast, but I have made some modifications and corrections to the project since the first video that I would like to go over.

## Clarification on "From Scratch"
Some of you might be wondering why the project has dependencies if it is being built from scratch. What I mean by "from scratch" is that I will not be using any existing code designed for producing video games or other similar applications. JavaScript is a small language, and the libraries I have included provide functionality similar to what you would find in the standard library of a more robust language. Any concepts central to the development of video games will be covered.

## Collection vs. Model
The first mistake I made was assigning the Scene collection to the Game view's *model* attribute, when I should have assigned it to the *collection* attribute. While JavaScript is dynamic enough to work fine either way, it's always good to follow convention whenever possible.

## Wrapping and Namespacing
Something I forgot to do was wrap all the code in *urge.js* in a function and only expose elements through a namespace. If you are unfamiliar with this practice, the basic idea is to wrap all your code in an immediately executing function so it has its own scope, and then put anything you need to be globally accessible inside one object. It looks something like this:

``` javascript
(function($, undefined) {
    // Create "Urge" namespace
    var Urge = window.Urge = {};

    // Add objects to namespace
    Urge.Entity = ...;
    Urge.Scene = ...;
    Urge.Game = ...;
})(jQuery);
```

It's a good idea to pass jQuery (or Zepto) as an argument if you are using it because *$* can sometimes be overwritten. I also like to add a final argument called *undefined* that isn't supplied. Since unsupplied arguments have the value *undefined*, this will guarantee the name *undefined* has the value you expect, even if something has tried to reassign it.

## Game vs. Game Engine
In the screencast, I misspoke and said *Urge.js* would contain all the code for the game I was building. This is incorrect. *Urge.js* will only contain the code for the game engine. The code for specific games will reside in separate files and reference *Urge.js*.

## Example Project
In the first screencast I created a simple test file that displayed a couple of blue squares on the screen. I decided to not include this file in the repository, and instead go ahead and create an example game. *Pumpkin Quest*, the Halloween themed RPG I imagined, resides in the *example/pumpkin* directory. Right now there is only some basic scaffold code that, rather predictably, draws a blue square. The screencasts will primarily follow the development of this game, with features being added to the *Urge.js* engine as the game needs them.

It is my hope that as *Urge.js* becomes more developed, others will submit their own example games in the form of pull requests.

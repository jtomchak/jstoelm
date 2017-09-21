---
layout: post
title: '6: Elm Architecture with Effects'
date:   09-19-2017
audioURL: 'e006-Elm-Effects'
categories: episodes
excerpt_separator: <!--more-->
---
We will take a look at the some of the deeper features of the Elm Architecture. So instead of producing Html from from update in the Elm runtime, we're going to produce Commands and Subscriptions. Like Htlm, we are going to describe what we want with some data, and let the Elm runtime do the actual work for us. Isn't this great?!
<!--more-->
<!-- TOC -->

- [News and updates](#news-and-updates)
- [Elm Architecture with Effects](#elm-architecture-with-effects)
- [Picks](#picks)
- [Follow](#follow)

<!-- /TOC -->


## News and updates
* 


## Elm Architecture with Effects
* We're gonna need a few more things in our app setup
  * Update so far has taken a Msg and Model and returned a new Model. We'll now need it to return a Model **AND** Command (Cmd). 
  * **Commands** will come right back to our update as a Msg. Which makes sense when you think about it. Update always takes 2 parameters. The first of type Msg, and the next of type Model.
  * **Subscriptions** will also come right back to our update as a Msg. So now we have Html, Cmd, and Sub Msg that our update can take. Given a model, these are event sources you'd like to subscribe to. 
  * Now we've got an init that does a bit more than return our initial model. It returns a model and Cmd Msg, just like the output of an update! that makes sense, right? This allows for starting value, and some https requests or whatever else we need to do, i don't know. 
* Just Data
  * Commands and Subsccriptions are just data.
  * Create the data cmd or sub, and then let the Elm runtime have at it. You don't actually run the command or subscription. But i was to invoke or call it myself? 
  * Effects as data have all sorts of upsides
    * time-travel debugger
    * same input == same output
    * easier testing update logic, no teardown / or mockup. ewwww
    * cache and batch effects, let the elm runtime handle it. we have enough to worry about
* Random Example
  * Sometime it's the simple things, don't name your module Random, bc there is a core module called....Random. lol
  * In fact, any time our program needs to get unreliable values (randomness, HTTP, file I/O, database reads, etc.) you have to go through Elm.
  * introduces a two step process for writing apps like this and (1) bare bones (2) and then the cool stuff. I've often said in class, you have to finish step 2, before you can tackle step 5. But I like the bare bones, and then the cool stuff phrase. 
  * Starting with the snippet, keeps elm fmt from running until you get all the way done. may need to make a good snippet for that!
* Giphy
  * so other than the cats. lol
  * getting something on the page, reducing that feedback loop, so important
  * The point is just to get something on screen!
  * **HTTP Request** 
    * oh boy. I see Json.Decoder, likely gonna need a whole on this guy soon
    * while I can't elequently explain every piece of this yet, I can sort of pick out what it's doing. 
    * damn it ! Comma's ```NewGiphy ( Err, _ )``` gotta remember this is a tuple if you put a comma in it!!
    * By the numbers
      1. create an HTTP request 
      2. turn that into a command so Elm will actually do it (Http.send)
  




## Picks
* [Elm Seeds](https://elmseeds.thaterikperson.com/elm-webpack-loader)
  * [Erik Person](https://twitter.com/thaterikperson)
* [It's a tangram for a logo!](https://en.wikipedia.org/wiki/Tangram)
* [Elm Language Server](https://github.com/hakonrossebo/elm-language-server-requirements-specification)

## Follow
* JavaScript to Elm
  * Twitter: [@jstoelm](https://twitter.com/jstoelm)
  * Email: [hello@jstoelm.com](mailto:hello@jstoelm.com)
* Jesse Tomchak
  * Twitter: [@jtomchak](https://twitter.com/jtomchak)

---
layout: post
title: '5: Elm Architecture with Effects'
date:   09-17-2017
audioURL: 'e005-Elm-Arch-Effects'
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
  * Create the data cmd or sub, and then let the Elm runtime have at it. You don't actually run the command or subscription. 
  * Effects as data have all sorts of upsides
    * time-travel debugger
    * same input == same output
    * easier testing update logic, no teardown / or mockup. ewwww
    * cache and batch effects, let the elm runtime handle it. we have enough to worry about
  




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

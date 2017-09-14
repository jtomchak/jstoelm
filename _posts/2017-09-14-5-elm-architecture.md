---
layout: post
title: '5: Elm Architecture'
date:   2017-09-12
audioURL: 'e005-Elm-Architecture'
categories: episodes
excerpt_separator: <!--more-->
---
Looking into the elm architecture in detail, what is, how it evolved, and more importantly how to apply it to our elm projects. 
<!--more-->
<!-- TOC -->

- [News and updates](#news-and-updates)
- [Elm Architecture](#elm-architecture)
- [Picks](#picks)
- [Follow](#follow)

<!-- /TOC -->


## News and updates
* Up til now it's been a sort of soft launch, last week I did an announcement on elm slack, and twitter. And the support and feedback are nothing short of amazing. This community is fantastic, so thank you.
* [Elm Conf](https://www.elm-conf.us/talks/)



## Elm Architecture 
![alt elm architecture](https://guide.elm-lang.org/architecture/effects/beginnerProgram.svg)
* The [architecture](https://guide.elm-lang.org/architecture/) seems to be a consequence of the design of Elm itself, so it will happen to you whether you know about it or not. This has proven to be really nice for onboarding new developers.
  * Evan has often talked bout seeing this pattern from talks. 
    * Picture of yogi bear centered!(felt like a very cool thing)
    * [ElmTown](https://elmtown.github.io/2016/12/01/The-Founding-Story-Ep-6.html)
    *  Wasting time with the sort of bugs are coming up
  * Pattern looks has these 3 parts
      * Added the beginning scaffold in the show notes 
      * Where's my MVC? 
        * So model, view, controller is often what goes in the controller? All the things that can't be put in the model or view! 
        
  1. **Model** — the state of your application
      * What do we need right out of the gate. Start with the model. 
      * Does it need to be a record, list, just an int ?
  2. **Update** — a way to update your state, using a Message (like an action)
      * How will the model need to change over time ? That is what we will define with the update. Like actions. You might be used to working in this direction, even with the react / redux I've done, it's still not quite as second nature as I'd like it to be. 
      * Update is going to take a msg and model and return a new model. it's immutable by it's very nature remember?
      * *insert long talk comparing update to redux* (confess to man crush on dan abramov)(explain what a man crush is)
      * if you want to an amazing talk about this comparison check out [Evan's React Rally talk](https://www.youtube.com/watch?v=jl1tGiUiTtI)
      * So update takes a msg & model and returns a new model. This is where the case match happens, like our 'reducer' from redux
  3. **View** — a way to view your state as HTML
      * The view is written with regular Elm functions, check last episode
      * Meaning we can use any of the Elm lang to build the view, this is why I was so drawn to React. While the JSX looked odd for like a whole minute, it was really being able to use just regular JS to make the view, and not some template symantec. Reguardless if that was Jade, Mustache, or Angular. It was the extra template 'programming' logic in addition to using JS that I didn't like. I didn't really understand my disstain for specific template logic, until Micheal Jackson (React Router) explained React from the point of view of building and maintaining Mustache.js, you know, the super popular templating language. 
      * The view code is entirely declarative
      * **NO** manual DOM manipulation. I really think this time has passed
      * That is the beauty of letting the Elm runtime handle it. amazing.
  * [Add the reset](https://ellie-app.com/4jcx724MH5va1/2)
    * add a new possibility to your Msg Type: Reset
    * then move on to the update and make a case for it, here it just returns 0 for the new model
    * now add a button onClick that takes that type 'Reset'
    * it's so straight forward to add additional features. a lot of the same feeling, after I get the whole redux boiler plate set up
  * [Reverse the text](https://ellie-app.com/4jdcfbZqBTJa1/3)
    * onInput, start with the same template, start with model then update, and finally view. Which feels so backwards from normal dev. 
    * Do I need console.log ? I have this sense that I'm missing something.
    * So this was super simple, it is not bound two way, if you've done any AngularJS or Angular [()] Event and Property binding I'm looking at you!
    * It's kinda like the handleOnChange that you see in React with that method calling setState when an event is sent to it, updating the state property
    * Took the code from Ellie to local, and couldn't stop naming the files '.js'. lol
    * **WOW** explore history ?!?! oh man, it's like redux chrome tools. I knew I picked the right lang to learn. This is such a pleasure. 
  * Programs
    * beginnerProgram
      * follows the Elm Architecture principles
    * program
      * with Commands and subscriptions.
    * programWithFlags
      * It works just like program but you can provide “flags” from JavaScript to configure your application.

```js
import Html exposing (..)

-- MODEL

type alias Model = { ... }

-- UPDATE

type Msg = Reset | ...

update : Msg -> Model -> Model
update msg model =
  case msg of
    Reset -> ...
    ...

-- VIEW

view : Model -> Html Msg
view model =
  ...

```


## Picks
* [Elm Slack](http://elm-lang.org/community)
* [Chris Krycho](https://twitter.com/chriskrycho) from New Rustacean [podcast](http://www.newrustacean.com/)


## Follow
* JavaScript to Elm
  * Twitter: [@jstoelm](https://twitter.com/jstoelm)
  * Email: [hello@jstoelm.com](mailto:hello@jstoelm.com)
* Jesse Tomchak
  * Twitter: [@jtomchak](https://twitter.com/jtomchak)

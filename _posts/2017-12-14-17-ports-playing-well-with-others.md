---
layout: post
title: '17: Ports: Playing well with others'
audioURL: e017-ports
categories: episodes
excerpt_separator: <!--more-->
---

Working on Elm, but we still want to leverage our favorite library or something else from the vast ecosystem that is JavaScript or other languages. Is there a way to communicate across the boundaries from Elm into JavaScript, and back, safely. There sure is, Ports! It is like JavaScript-as-a-Service.

<!--more-->

<!-- TOC -->

* [Ports](#ports)
  * [Evan's call to action](#evans-call-to-action)
  * [JavaScript Interop](#javascript-interop)
  * [Border Protection](#border-protection)
* [Picks](#picks)
* [Resources](#resources)
* [Follow](#follow)

<!-- /TOC -->

## Ports

### Evan's call to action

* So in listening to the latest [ElmTown](https://overcast.fm/+HSqyPZagc/31:23), episode 22, with Evan
  * Help needed: High on the google search results. Blog Posts in dealing with Ports. Similar to SPA in Elm, more documentation became available.
* JavaScript alternative, not a different approach to FrontEnd development.
* **NOT** making JS better as a goal, but rather FrontEnd Better all together.
* If Ports can't work for you, then Elm may not be for you, and that's ok.
* Love to see Elm on other platforms, is the usual comment.
* Web Storage, I hear, a more generalized approach, rather than tying Elm to specific API. Portability.
* Ecosystem Reliability
* Foreign Function Interface / Interop ?
* _actual solving the problem in another way, not just replicating or shoehorning the JS solution into Elm_

### JavaScript Interop

* Not your regular language interop. When C++ was designed, it was a conscious design choice that all C, was valid C++, this provides **FULL** backward compatibility. That is the easy, and popular choice. Java/Scala or JavaScript/TypeScript. The catch is you get all the baggage of the old language dumped right into your new language!!! Damn it!
* Right out of the docs:
  > Elm's interop is built on the observation that by enforcing some architectural rules, you can make full use of the old language without making sacrifices in the new one.
* This system of messages keeps JS at arms length, and the 'crazy' our of our Elm code.

1. embedding Elm in HTML
2. sending messages back and forth between Elm and JavaScript:

* Ok that sounds pretty straight forward. We're coming at this from a mostly JS background, with little FP experience. But what does this look like?

1. Some Set up on the Elm side creating a port Cmd, and port Sub.
2. Cmd for sending messages/data to JS, and the Sub to receive messages/data from JS.
3. Our Elm module needs to be declared as `port module` **NOTE** you should not have a ton of port modules in your Elm app!!! (Very few modules should have ports in them!) Why? Well if you require lots of ports from Elm to JS, then maybe Elm is not the right tool for the job? And, the best part? That's ok!

### Border Protection

* Types allowed

  * Booleans and Strings – both exist in Elm and JS!
  * Numbers – Elm ints and floats correspond to JS numbers
  * Lists – correspond to JS arrays
  * Arrays – correspond to JS arrays
  * Tuples – correspond to fixed-length, mixed-type JS arrays
  * Records – correspond to JavaScript objects
  * Maybes – Nothing and Just 42 correspond to null and 42 in JS
  * Json – Json.Encode.Value corresponds to arbitrary JSON

* What happen's if there is an type :: List String and JS send us an Number!
* Elm throws a runtime exception immediately when you call send with invalid data. We can't fix JS, but we can protect our Elm environment from being contaminated with invalid data!!!
* **NOTE** ports is not allowed in a published Elm package. Why? Consider downloading an Elm package, only to realize that it requires some funky JS work on the outside to get it to work! Poor user experience for sure.

## Picks

* [The Haskell Book, You code to learn to learn to code with this book!](http://haskellbook.com/)
* [Mostly Adequate Guide](https://github.com/MostlyAdequate/mostly-adequate-guide)
* [Synchronizable abstractions for understandable concurrency
  Or: what is Concurrent ML all about? by Adam Solove](https://medium.com/@asolove/synchronizable-abstractions-for-understandable-concurrency-64ae57cd61d1)

## Resources

* [ElmTown Episode 13](http://elmtown.audio/2017/05/09/history-in-elm-town-ports-episode-13.html)
* [ElmTown Episode 22 A call to action](http://elmtown.audio/2017/11/10/elm-town-episode-22-how-do-i-write-js-in-elm.html)
* [Murphy Randle — The Importance of Ports](https://www.youtube.com/watch?v=P3pL85n9_5s&t=5s)
* [Elm Docs JavaScript](https://guide.elm-lang.org/interop/javascript.html)

## Follow

* JavaScript to Elm
  * Twitter: [@jstoelm](https://twitter.com/jstoelm)
  * Email: [hello@jstoelm.com](mailto:hello@jstoelm.com)
* Jesse Tomchak
  * Twitter: [@jtomchak](https://twitter.com/jtomchak)

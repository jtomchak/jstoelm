---
layout: post
title: '12: Fetch & Decoding JSON Part-2'
date:   2017-10-25
audioURL: e011-fetch-decoding-json-part-2
categories: episodes
excerpt_separator: <!--more-->
---
One of the fundemental tasks of any web app, is to get, display, capture, save, manipulate, or otherwise man handle data from an http request. We are gonna dive into what that means for our model, our update function, and our sanity. 
<!--more-->
<!-- TOC -->

- [Finally Decoding](#finally-decoding)

<!-- /TOC -->

## Finally Decoding
* But first if we google Elm decoding json, we get these gems:
  * [Decoding Cheatsheet](https://gist.github.com/yang-wei/0a1cea1194a244aa9be6)
  * [json decoding in elm is still hard](https://medium.com/@eeue56/json-decoding-in-elm-is-still-difficult-cad2d1fb39ae)
* The Json.Decode.decodeString function returns a Result. It has a type of:
```decodeString : Decoder val -> String -> Result String val``` so what does that mean? Well, more or less that we need Json.Decode to convert the JSON values into Elm values. And by elm values I mean, types safe, friendly compiler, you're there when I assume you are, and if not, it's handled accordingly type values. :-) 
* Json.Decode exposing (..) gives us primitives bool, float, int, string, and null. 
```bash
> decodeString bool "true"
Ok True : Result.Result String Bool
> decodeString bool "false"
Ok False : Result.Result String Bool
```
* So what about really JSON, like arrays, objects, or arrays of objects!!!!! The idea would be to coralate an array of things to a things of _particular_ things, right? 
* At this point, Richard's book says, "...simplest is with a function like map2"
Excerpt From: Richard Feldman. “Elm in Action MEAP V05.” iBooks. And to that I respond, oh crap. Now I need to stop and look up map2, I'm hoping it's as simple as learning that a fold is just a JavaScript reduce method. I however doubt that very much. 
* Insert Pipeline to the rescue! ```elm-package install NoRedInk/elm-decoder-pipeline``` learned that it's case sensitive!!


## Picks
## Resources
* [Intro Elm decode json](https://guide.elm-lang.org/interop/json.html)
* [NoRedInk elm decode pipeline](https://github.com/NoRedInk/elm-decode-pipeline)

## Follow
* JavaScript to Elm
  * Twitter: [@jstoelm](https://twitter.com/jstoelm)
  * Email: [hello@jstoelm.com](mailto:hello@jstoelm.com)
* Jesse Tomchak
  * Twitter: [@jtomchak](https://twitter.com/jtomchak)

---
layout: post
title: '12: Fetch & Decoding JSON Part-2'
date:   2017-10-25
audioURL: e012-fetch-decoding-json-part-2
categories: episodes
excerpt_separator: <!--more-->
---
One of the fundemental tasks of any web app, is to get, display, capture, save, manipulate, or otherwise man handle data from an http request. We are gonna dive into what that means for our model, our update function, and our sanity. 
<!--more-->
<!-- TOC -->

- [Finally Decoding](#finally-decoding)
- [Picks](#picks)
- [Resources](#resources)
- [Follow](#follow)

<!-- /TOC -->

## Finally Decoding
* But first if we google Elm decoding json, we get these gems
  * [Decoding Cheatsheet](https://gist.github.com/yang-wei/0a1cea1194a244aa9be6)
  * [json decoding in elm is still hard](https://medium.com/@eeue56/json-decoding-in-elm-is-still-difficult-cad2d1fb39ae)
* The Json.Decode.decodeString function returns a Result. It has a type of:
```js 
decodeString : Decoder val -> String -> Result String val
``` 
  so what does that mean? Well, more or less that we need Json.Decode to convert the JSON values into Elm values. And by elm values I mean, types safe, friendly compiler, you are there when I assume you are, and if not, it's handled accordingly by type values.
* Json.Decode exposing (..) gives us primitives bool, float, int, string, and null. 

```bash
> decodeString bool "true"
Ok True : Result.Result String Bool
> decodeString bool "false"
Ok False : Result.Result String Bool
```
* So Json.Decode has a 'list' function that Decoder and a(value) and returns a Decoder of (List a)

```bash
> import Json.Decode exposing (list, bool, string, int)
> list
<function> : Json.Decode.Decoder a -> Json.Decode.Decoder (List a)
> bool
<decoder> : Json.Decode.Decoder Bool
> string
<decoder> : Json.Decode.Decoder String
```

* So what about really JSON, like arrays, objects, or arrays of objects!!!!! The idea would be to coralate an array of things to a thing of _particular_ things, right? 
  *  Easy mode. Running 3 conditional checks (bridge of death)
    1. Are you an object ?
    2. Do you have an property 'email' ?
    3. Is the value of email of type string ?
    4. [What is your favorite color ?](https://www.youtube.com/watch?v=pWS8Mg-JWSg)
```js
decoder : Decoder String
decoder = 
  field "email" string 
```
* So great. That's a single field. When was the last time our json payload returned us a single field. ummm, close to never. lol
* At this point, Richard's book says, "...simplest is with a function like map2"
Excerpt From: Richard Feldman. "Elm in Action MEAP V05." iBooks. And to that I respond, oh crap. Now I need to stop and look up map2, I'm hoping it's as simple as learning that a fold is just a JavaScript reduce method. I however doubt that very much. 
* Insert Pipeline to the rescue! ```elm-package install NoRedInk/elm-decoder-pipeline``` learned that it's case sensitive!!
* This chapter we'll refer to as a glut for punishment. For me, often if I am forced to do things the hard way, and then introduce a 'simplier' or more conventent shorthand way of doing something I tend to remember it better. So I skipped over the pipeline part and we straight to http.get instead of http.getString. 
  * This forces me to think a little more about my what i'm writing. Less of type it out, and will invole a bit of debugging. 
  * Forces me to become more familiar with the language syntax, if it breaks, the answer isn't comparing it to the tutorial,it's to comb over the code itself. And yes this has lead to hours of time finding small mistakes. Some would call it time wasted. I consider it lessons learned. Whenever this happens, I'll try dozens of things that don't work. This is the process of learning for me. It's very hands on, it's very messy, and time intensive. 
* hour or two later......The struggle is real. [google it](http://package.elm-lang.org/packages/elm-lang/core/5.1.1/Json-Decode#map2)
* map2-map3 is a function of Decoder...... **NOT** List. lol type mismatch. See what I mean about learning by just pounding on it.
> I am a hammer, every book, my nail
* So sweet jesus, optional fields, what have I gotten myself into. I have to note, at this point, I am strongly considering ```git reset --hard``` and just taking the red pill and following pipeline. 
* So it turns out there is a plethera of methods to expose from Json.Decode. And we haven't even gotten to Fancy Decoding!!!!

* So which is a more Elm convention ? Maybe.withDefault, or separate function with a case expression ? 
```js
viewThumbnail : Maybe String -> Photo -> Html Msg
viewThumbnail selectedUrl thumbnail =
    img
        [ src (urlPrefix ++ thumbnail.url)

        -- , hasTitle thumbnail.title thumbnail.size
        , title ((Maybe.withDefault "None" thumbnail.title) ++ " [" ++ toString thumbnail.size ++ " KB]")
        , classList [ ( "selected", selectedUrl == Just thumbnail.url ) ]
        , onClick (SelectByUrl thumbnail.url)
        ]
        []


hasTitle : Maybe String -> Int -> Attribute msg
hasTitle maybeTitle size =
    case maybeTitle of
        Nothing ->
            title "None"

        Just photoTitle ->
            title (photoTitle ++ " [" ++ toString size ++ " KB]")
```

* Thinking about a couple bonous interviews, thoughts, Elm Town is already there. Are there peeps you'd like to hear from ? 

## Picks
* [Elm in action](https://www.manning.com/books/elm-in-action)
* [Lessons Learned From a Year of Elm -- William Makley](https://gist.github.com/wmakley/710183095662dae473092a0e5f294f24)
* [Time Well Spent -- Kyle Shevlin](https://kyleshevlin.com/time-well-spent/)

## Resources
* [Intro Elm decode json](https://guide.elm-lang.org/interop/json.html)
* [Check the Docs](http://package.elm-lang.org/packages/elm-lang/core/5.1.1/Json-Decode)
* [NoRedInk elm decode pipeline](https://github.com/NoRedInk/elm-decode-pipeline)
* [Decode Extra](https://robots.thoughtbot.com/decoding-json-structures-with-elm)
* [inconsistent structure](http://package.elm-lang.org/packages/elm-lang/core/5.1.1/Json-Decode#inconsistent-structure)
* [optional maybe](http://rundis.github.io/blog/2016/elm_maybe.html)

## Follow
* JavaScript to Elm
  * Twitter: [@jstoelm](https://twitter.com/jstoelm)
  * Email: [hello@jstoelm.com](mailto:hello@jstoelm.com)
* Jesse Tomchak
  * Twitter: [@jtomchak](https://twitter.com/jtomchak)

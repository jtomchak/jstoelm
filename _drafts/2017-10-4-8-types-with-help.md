---
layout: post
title: '8: Types with Help'
date:   2017-10-04
audioURL: 'e008-Types-with-Help'
categories: episodes
excerpt_separator: <!--more-->
---
Compiler help. The promise of Elm is no runtime errors. This has been proven in large code bases like that of NoRedInk. But how can it make such a claim? Elm has a strong, static type system. So let's understand it better, and leverage to get the most of Elm. 
<!--more-->
<!-- TOC -->

- [News and updatesd](#news-and-updatesd)
- [Types with that for can haz help](#types-with-that-for-can-haz-help)
  - [Current work on Photo Groove from Elm in Action](#current-work-on-photo-groove-from-elm-in-action)
- [Picks](#picks)
- [Follow](#follow)

<!-- /TOC -->


## News and updatesd
* Elm conf was last week, and it was fun to follow via slack and twitter. It sounds like it was as amazing as I expected it to be. Really wish I could have made it. Brian Hicks, the organizer, has started releasing the videos of the talks. I was hoping to binge watch them all, but they are being released 2 per day. I like this idea. Gives me a chance to focus on just 2 for that day, and enjoy them. Rather than skipping around from some to others. The motivation was really to give all the speakers due credit for their hard work, and not get buried in an avalanche style release. Once they are all releases, I've been making notes on each video as they're coming out, and hopfully I'll be able to incorporate it into an upcoming episode soon.
* Looking forward, [Elm Europe 2018](https://2018.elmeurope.org) is next Engineering School in Villejuif (near Paris, France) on July, 5-6th. Calling for papers.... 


## Types with that for can haz help
* You can't save yourself from .... yourself (SELECTED_PHOTO not SELECT_PHOTO)!!!!
  * Spent probably 40 minutes wondering why it wasn't working.
  * Which is good, in the long run. I started using the ```Debug.log "tag" value``` which you can't just willy nilly drop in anywhere you want!
```js
    let
        _ =
            Debug.log "Message Data" msg.data
    in
```
  * Now if you're out there gilbert, yes, union types. I got it, I just haven't gotten to that yet!!
* Creating view model functions
  * if then, else syntax
* Elm is curried, what's that mean? Haskell Brooks Curry. Where do I know that name from? At this point should probably pick up a     biography of this guy!
  * Understand partial function application
  * JS in contrast is not. It's tupled, meaning it expects all the arguments upfront. 
  * Remember to put in the what does that look like in JS, Richard does a very good job of this. 
* Type Annotations
  * these I feel like are pretty straight forward. 
  * ```greetings : String -> String```
    * This would read as function greetings takes type of string and returns a string
  * ``` map : (a -> b) -> List a -> List b ```
    * The parens help to disambiguate and direct order of operations, just like in map. So here we'd say, map takes a function, that function takes a type and returns a different type, and map also takes a List of type a, then returns a List of type b.
* Type variables
  * A type variable represents more than one possible type. Type variables have lowercase names, making them easy to tell them apart from concrete types like String, which are always capitalized.
  * ```List a -> Array a``` Would read, List of type a, where 'a' is whatever, strings, numbers, records. List of type a will return an Array of type a. This Array of type is the same as the List type that we started with. 
* Type aliases 
  * allow you to attach human readable names to existing types.
  * now instead of using that whole record for a type, we can use 'User', and have a better understanding of what the record is refering to, but also make our types more concise. 

```js
  type alias User =
  { name : String
  , hobbies : List String
  , age : Int
  , beard : Bool
  }
```
* Union Types
  * Also known as: Union types are sometimes called tagged unions. Some communities call them ADTs.
  * Feel like we can do a whole show on union types. So, that's what we'll do!
  
### Current work on Photo Groove from Elm in Action
<iframe src="https://ellie-app.com/embed/5dZZQYynxa1/1" style="width:100%; height:400px; border:0; border-radius: 3px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>




## Picks
* [Robert Bethencourt for the shout out during his talk](https://github.com/robbethencourt/elm-rethink-http)
* [Ellie](https://ellie-app.com/new)
  * Newly opensourced Live at ElmConf
  * Luke Westby
* [Murphy Egghead.io](https://egghead.io/lessons/elm-make-an-http-request-in-elm)
* [Elmconf Videos](https://www.youtube.com/watch?v=P3pL85n9_5s&list=PLglJM3BYAMPFTT61A0Axo_8n0s9n9CixA)
* [Functional Professor](https://drboolean.gitbooks.io/mostly-adequate-guide/content/ch4.html)

## Follow
* JavaScript to Elm
  * Twitter: [@jstoelm](https://twitter.com/jstoelm)
  * Email: [hello@jstoelm.com](mailto:hello@jstoelm.com)
* Jesse Tomchak
  * Twitter: [@jtomchak](https://twitter.com/jtomchak)
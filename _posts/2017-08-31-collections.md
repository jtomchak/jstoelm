---
layout: post
title: '3: Collections'
date:   2017-08-28
audioURL: 'e003-Collections'
categories: episodes
excerpt_separator: <!--more-->
---
We look at the basic collections in Elm, lists, records, and tuples and how they compare to JavaScript arrays and objects that we are more familiar with. 


<!--more-->
<!-- TOC -->

- [News and updates](#news-and-updates)
- [Collections](#collections)
- [Picks](#picks)
- [Follow](#follow)

<!-- /TOC -->
## News and updates
* Elm Conf Sept 28th [Link](https://www.elm-conf.us/)
* [Elm discuss Google and Elm Slack](http://elm-lang.org/community)
  * Community Packages
  * Reddit
  * Slack
  * Twitter
  * Real Life
  * Mailing list
  * Contributing
* [Elm Town Eposide 18, Mario Rogic](https://elmtown.github.io/2017/08/28/spotlight-on-margio-rogic-episode-18.html)
* I went to React Rally 2017
  * Amazing
  * Sean Larkin, Shirley Wu, Lin Clark, Max Stoiber, Preethi Kasireddy, Henry Zhu, Michael Jackson
  * Live streamed, but the presentations are up.
  * Learned that Elm is compiled in Haskell
  * Would like to see Elm compile to webassembly .wasm

## Collections
* Lists
  * First and formost **IMMUTABLE**
    * So we don't push, we .append and that returns a new List value
    * Super rad compiler, helping out the noob [Gist](https://gist.github.com/jtomchak/f17ca7589b877a483be60df4398b478d)
    * Don't add a string to a string collection, you append a List String, to a List type of String
  * Can concat with the '++' like a string
  * It has no methods or build in functionality
    * Use the List module like List.map or List.filter
    * This can be a bit strange. We are often used to running/appling/calling something kind of method on a type. Well types don't have methods, JS objects do, and we're not in JS Land anymore. 
  * Must be of the same type. List of strings or numbers only, no mixing
    * Make a list of both strings and numbers with a sort of wrapper can be done, it's called a Union Type, that is for another time
  * It is also a *linked list* so you can get the first item, but not get an item in the list by index position. Now you are likely thinking, wha? How is that even useful, the whole reason to have a list of items is that the position is important, otherwise we'd use a Set. Right? 
    * What is a [*linked list*](https://en.wikipedia.org/wiki/Linked_list)
    * >  benefit of a linked list over a conventional array is that the list elements can easily be inserted or removed without reallocation or reorganization of the entire structure because the data items need not be stored contiguously in memory or on disk, while an array has to be declared in the source code, before compiling and running the program. Linked lists allow insertion and removal of nodes at any point in the list, and can do so with a constant number of operations if the link previous to the link being added or removed is maintained during list traversal.
    * Not totally sure at this point what the over all advantage of using List over Array is. But Elm does in fact have Array's. But so far, from a beginner level, there is very little I can find on them. List seems to be the prefered collection type. So I'm willing to buy in. 
    
* Records
  * A collection of named fields, each with an associated value. kinda like an object, but not
  * Also **IMMUTABLE**
  * Only accessed with dot notation. Sweet! Always a bit thrown when I see JS [value] called with square brackets
  * Stilling the {}, but without the ':', just use '=' the assigment operator. So simple!
  * No secret _prototype chain. What you see is what you get
  * So while everything in Javascript is an Object with a capital 'O', records are just to hold the data we provide it.
  * So far so good, it's the updating part that is interesting. Let's see!!
    * [Gist](https://gist.github.com/jtomchak/620e713218b5d269c2e5b999d098680a)
    * Since it's immutable we can't modifiy it, only return a new one
    * Create a new record and use the existing record and the  pipe operator to change any of the properties we'd like. Order up changes, does not matter. Think about it like the spread operator in ES2015

* Tuples
  * A tuple is an ordered collection of values, which can consist of two or more elements.
  * A record with no key name
  * Called using position, like Tuple.first or Tuple.second there is no .third for Tuple
    * Then you need destructuring
    * ("skittles",12,"brown") : ( String, number, String )
    * (name, age, color) = meow
  * A tuple and a parenthetical function call. One has a comma, one is a function that takes an argument. I see trouble ahead, when I will want my curly brackets.
  * Examples would be lat & longitude, or Error Tuple (True/Flase, "With a message Meow")
  * [Additional info](https://dennisreimann.de/articles/elm-data-structures-record-tuple.html)


* Next up, I think the Elm Architecture. Model - View - Update or where's the Controller? 

## Picks
* React Rally [Link](http://www.reactrally.com/)
* Evan Czaplicki - Convergent Evolution [Link](https://www.youtube.com/watch?v=jl1tGiUiTtI)

## Follow
* JavaScript to Elm
  * Twitter: [@jstoelm](https://twitter.com/jstoelm)
  * Email: [hello@jstoelm.com](mailto:hello@jstoelm.com)
* Jesse Tomchak
  * Twitter: [@jtomchak](https://twitter.com/jtomchak)

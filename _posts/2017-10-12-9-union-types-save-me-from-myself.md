---
layout: post
title: '9: Union Types, save me from myself'
date:  2017-10-12 
audioURL: 'e009-union-types'
categories: episodes
excerpt_separator: <!--more-->
---
A dive into Union Types, with it's ability to represent complex data type, we are gonna really want to understand and leverage this power when the data in our app can take on different forms at different times. When you have uniquely shaped data, reach for a union type. 
<!--more-->
<!-- TOC -->

- [Union Types](#union-types)
- [Maybe, as a container](#maybe-as-a-container)
- [Picks](#picks)
- [Follow](#follow)

<!-- /TOC -->

## Union Types
* Known as tagged unions or ADTs
  * Tagged Unions: a data structure used to hold a value that could take on several different, **BUT** fixed types. 
  * Only **ONE** of the types can be used at any single given time. The 'tag' field indicates explicitly which one is currently in use. 
  * Referred to as datatypes or algebraic data type (ADT). Leveraged in functional languages like what we're doing now. Probably why I haven't heard of them in nearly a decade yet.
    * *aside* man, being a n00b is hard. I think it's to quickly forgotten that feeling of being overwhelmed at every turn. Thinking, man I'll never get this. I brush those feelings off everytime I work in Elm, Haskell, Rust, or any else that I am not intimately familiar with, the kind of familiarity that only comes after years of working with something. Having been down this road before, I know, that if i keep at it, it will come. It will snap into place for me, slowly, piece by piece. Now think about those who are possibly working on understanding their first language? Without having those previous successes beyond them? It's a struggle. Anyway, it's important to practice empathy with anyone coming to your particular community for the first time. Big props to all those in Elm slack, the beginner channel especially, I haven't seen those turse, "read the docs" posts that I've encountered other times. </rant>
  * Fun fact: Alegbraic data types were introduced in Hope, a small functional programming language developed in the 1970s at Edinburgh University. 
  * Often has a type constructor, which is like a constructor for a class. Guessing it takes an argument and returns one of several defined types as a tagged union type. **BOOM** For our case in Elm, we'd use a constructor function that would return that particualr type. 
  * Enumerated type. This is something I know about. We used enum's in objc a lot to help define the single state of a particular object. This would considered a tagged union of unit types, as it returns the tag, but doesn't and **can't** hold any additional data. For those of you keeping score at home, objc was my first language I learned to develop for iPhone. Swift did have associated values with it's enums. Man, as I learn Elm and Haskell, I am constantly going back to my swift books, and being like, "hey, that looks familar" and sure enough, there is just an ever so slit sprinking of functional langage in swift. I also feel like you can't go full FP in iOS, as you have to live within the [Cocoa Touch Environment](https://developer.apple.com/library/content/documentation/General/Conceptual/DevPedia-CocoaCore/Cocoa.html), that includes Foundation and UIKit, an imperitive house holde built with objc and C++. Which is fine, to say that imperitive bad, functional good, I don't think is a health way to present fp or anything else for that matter. I think so many of us have been frustrated with OOP and the design patterns, that it's natural for us to present functional as *better* way of doing things, but there is a lot of power in object oriented thinking. I want to try and focus on the *differences* that functional programming and langages that embrace it. If you catch me bagging OOP, call me out, please. </rant> 
  
Objective-C Enum 
```objc
typedef enum playerStateTypes
        {
            PLAYER_OFF,
            PLAYER_PLAYING,
            PLAYER_PAUSED
        } PlayerState;
```  
[Swift Enum](https://developer.apple.com/library/content/documentation/Swift/Conceptual/Swift_Programming_Language/Enumerations.html)
```swift
enum Barcode {
    case upc(Int, Int, Int, Int)
    case qrCode(String)
}
```
Rust, also allows matching on unions
```rust
enum Tree {
  Leaf,
  Node(i64, Box<Tree>, Box<Tree>)
}
```
* There is a pattern match on the given argument or variant and then the return of the correct union.Do not confuse these patterns with regular expression patterns used in string pattern matching. The purpose is similar: to check whether a piece of data matches certain constraints, and if so, extract relevant parts of it for processing. However, the mechanism is very different. This kind of pattern matching on algebraic data types matches on the structural properties of an object rather than on the character sequence of strings. 
```Haskell
 depth :: Tree -> Int
 depth Empty = 0
 depth (Leaf n) = 1
 depth (Node l r) = 1 + max (depth l) (depth r)
```
* Advantages of Union Types is clearly all accesses to the data are **SAFE** the compiler has your back, and will even validate that all cases are handled. If you'll remember last weeks episode, I lost a good chuck of time, trying to figure out why my onClick msg passed to the update function wasn't working, it was bc I missed type it! Had it been a union type, and not just a string, this would have been picked up by the compiler right way. The only down side I've come across is that that the tag of a union type takes up additional space. And to that I really have to say, wha? We're not coding for [Apollo 11](https://github.com/chrislgarry/Apollo-11) anymore. One could argue that size constrants at such a low level are silly. One could also argue that with such constrants, is when we are truly at our most creavtive. Left up to the listener. 

Elm compiler Letting me know that I can't pass ExtraLarge to the function viewSizeChoose because it takes a Thumbnail as an argument, and Thumbnail can only be Small, Medium, Large. 'ExtraLarge' does not exist!
```Elm
type ThumbnailSize
    = Small
    | Medium
    | Large

viewSizeChoose : ThumbnailSize -> Html Msg

Failed to compile.

./src/Main.elm

-- NAMING ERROR - /Users/jtomchak/Documents/Elm/photoGroove-podcast/src/Main.elm

Cannot find variable `ExtraLarge`

98|             (List.map viewSizeChoose [ Small, Medium, Large, ExtraLarge ])
                                                                 ^^^^^^^^^^


Detected errors in 1 module.
```
* So what about in JS ? 
  * I'm glad you asked, when working with Redux, I will also make 'ActionTypes', which are nothing more than a string assigned to a variable of the same name. Doing so let's us do ```import * as types from './ActionTypes'``` then we can use ```case types.ADD_TODO:``` instead of the error prone ```case "ADD_TOOD":```
  * [Modeling union types using only function](https://brehaut.net/blog/2013/unions_as_functions) an interesting take on trying to leverage union types within JS. 
* Let's put it all together. 
  * Solve each subprobelm you have first and formost.
  * Use union types to put togeher all the solutions, creating a unquiely formed data type.
  * Creating a union type generates a bunch of *constructors* 
  * These constructors *tag* the data so that we can differentiate it at runtime. (<3 to the compiler)
  * A *case* expression lets us tear data apart based on these tags, using pattern matching, 
  * **Msg as a Union Type**
    * Because it's rad
    * Save me from typos
    * Each Msg now has only the data that it needs. And for all the other good reasons out there. 

## Maybe, as a container
* maybe verus *undefined* Ready Fight!
* Maybe is the representation of the potential absence of a value.
* In Swift we called them optionals



## Picks
* [Actor Model](https://en.wikipedia.org/wiki/Actor_model). Man has this phrase shown up in spades in my tech feed in the last couple weeks. Fatal Error podcast, Murphy's Elmconf talk. 
* [CoffeeScript 2](http://coffeescript.org/announcing-coffeescript-2/). Further speculation that we may not all be writing 'raw JavaScript' in a few short years...
* [Docs](https://guide.elm-lang.org/types/union_types.html) that echo the compiler: "(As you get more experience, you will see that Elm wants you to build programs out of small, reusable parts. It is weird.)"
* Special shout out to Richard for [Elm in Action](http://elm-in-action.com)


## Follow
* JavaScript to Elm
  * Twitter: [@jstoelm](https://twitter.com/jstoelm)
  * Email: [hello@jstoelm.com](mailto:hello@jstoelm.com)
* Jesse Tomchak
  * Twitter: [@jtomchak](https://twitter.com/jtomchak)


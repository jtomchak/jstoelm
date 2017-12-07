---
layout: post
title: '16: Haskell for greater Elm'
audioURL: e016-haskell-for-greater-elm
categories: episodes
excerpt_separator: <!--more-->
---

We Turn our attention back to Haskell to help us get the best possible
foundation for really diggin' into functional programing. For me, only after
doing piles of short examples, does it sink in for me, it's the repetition and
console output that is key.

<!--more-->

<!-- TOC -->

* [Haskell for a greater Elm](#haskell-for-a-greater-elm)
  * [Types](#types)
  * [Polymorphism](#polymorphism)
  * [Small Details](#small-details)
* [Picks](#picks)
* [Resources](#resources)
* [Follow](#follow)

<!-- /TOC -->

## Haskell for a greater Elm

The more Elm I do, the more I feel like I'm reading a story, and missed a
chapter. There feels like some infered knowleadge, that I simply do not possess.
Like you missed a key plot point in a movie, and you totally miss the big
reveal!

You might be a very visual person. That's awesome. I am not. I often here hear
in teaching, that get the students to get something, anything up on the DOM, as
soon as possible. This accomplishs a couple things. It gives them a sense of
accomplishment, which is great, sucesses, at every level should be celebrated,
but it also gives them some visual feedback, a thing,a tangable thing to look at
and manipulate. I am not that type of student. I would rather do 20 commandline
`println "Hello World` than a single visual output. And for me, the reason is
repitition. I need the quickest, shortest, black and white feedback. I don't
want to switch applicaitons, I don't even want to switch window focus. I want to
type out a thing, and as quickly as I can, get some regualr text feedback. Like
a println, or console.log, anything that does not require me to `inspect
element`.

### Types

* A way of categorizing values
* 'a' :: Char -- this reads string 'a' has of type Char
* '::' is a type signature, this defines the type for that value, function,
  expression, whatever it might be.
* single quotes is a char, but double denotes a string. In JS, it doesn't
  matter, the rule is to just be consistant. I **feel** like JS has given me the
  room, to either be really sloppy, or to express myself very well?
* _String_ is a type alias. We use it as a convienance to refer to the actual
  type. In this case, String is really _[Char]_ a list of Char. We can also use
  it to denote something like `:type Title` as
* infix (++) & concat
  * _has the type of list of lists_
  * remember a string is just a list of char
  * what's foldable? [[a]], _foldable_ instances of the Foldable typeclass, to
    come...
  * if we concat a list of lists, it will simply flatten them into a single list
  * in the below example _ everything to the right of the '::' is strictly about
    our types, not values _ the 'a' in the [] is called a **type variable** _ it
    does not know(i put cared here, but explicit knowleadge i think is more
    appropriate) _ it simply doesn't know, that that it doesn't care _ it will
    get a value for 'a' during the running of the program at some point, it
    won't always be a mystery, then it can be a concrete type like `[Char]` _ bc
    the type signature is using `a` for placeholder of the value to come, it is
    explicit that the list type must be the same `a == a` \* and the final `[a]`
    of the 3 is the return type is also, surprise, a list of `a`
    > _Typeclasses_ provide definitions of operations, or fucntions, that can be
    > shared across sets of types

```hs
λ :t (++)
(++) :: [a] -> [a] -> [a]
λ : concat
concat :: Foldable t => t [a] -> [a]
```

### Polymorphism

* Boy, didn't think I'd see you here. I first learned of you when programming
  Objc.
  > Objective-C polymorphism means that a call to a member function will cause a
  > different function to be executed depending on the type of object that
  > invokes the function
* Haskell
  1. **Parametric polymorphism**
  * Parametric polymorphism refers to when the type of a value contains one or
    more (unconstrained) type variables, so that the value may adopt any type
    that results from substituting those variables with concrete types.
  2. **Ad-hoc polymorphism**
  * Ad-hoc polymorphism refers to when a value is able to adopt any one of
    several types because it, or a value it uses, has been given a separate
    definition for each of those types.

### Small Details

* Things you only get from working with a lang, like the implicit return from a
  `=>` in JS
* These are hard to quanitify and communicate, they are rather picked up along
  the journey.
* _where_ and _let_ in Haskell introduce local binding to a name. Giving us the
  ability to reuse it with

## Picks

* [Partial application lamda parameters for js by Bo Lingen](https://medium.com/@citycide/partial-application-lambda-parameters-for-js-aa16f4d94df4)
* [ReasonML Dr. Axel Rauschmayer](http://2ality.com/2017/11/about-reasonml.html)

<script src="https://gist.github.com/citycide/de05c3f47a347c1b64cb7a7c548f6b7c.js"></script>

## Resources

* [The Haskell Book](http://haskellbook.com/faq.html)
* [The Joy of Haskell](https://joyofhaskell.com/)
* [Hakyll](https://jaspervdj.be/hakyll/)
* [Reflecting on Haskell in 2017](http://www.stephendiehl.com/posts/haskell_2018.html)
* [On Understanding Data Abstraction, Revisited](http://www.cs.utexas.edu/~wcook/Drafts/2009/essay.pdf)

## Follow

* JavaScript to Elm
  * Twitter: [@jstoelm](https://twitter.com/jstoelm)
  * Email: [hello@jstoelm.com](mailto:hello@jstoelm.com)
* Jesse Tomchak
  * Twitter: [@jtomchak](https://twitter.com/jtomchak)

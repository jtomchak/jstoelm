---
layout: post
title: '19: More than Just Functions'
audioURL: e019-more-than-just-functions
categories: episodes
excerpt_separator: <!--more-->
---

The idea of functional programing is more than just the use of functions, or functions as first class citizens. It is a real paradigm shift in the way we think about tackling problems with code. A lot of what brings me, and others, to Elm is the desire to learn and even more importantly use techniques that FP puts forth in our daily programing. While trying to tackle static types, curring, partial application, and a bucket of other important concepts, it's the idea of FP that brought a lot of us here in the first place, less we forget it.

<!--more-->

<!-- TOC -->

* [Functions](#functions)
  * [Procedural/Imperative programming](#proceduralimperative-programming)
  * [Output](#output)
  * [Side Effects](#side-effects)
  * [Inputs](#inputs)
  * [Why Functional](#why-functional)
  * [Final Thoughts](#final-thoughts)
* [Picks](#picks)
* [Resources](#resources)
* [Follow](#follow)

<!-- /TOC -->

## Functions

* A function takes inputs and **ALWAYS** returns output
  * I have definitely _NOT_ always done this.
  * Many cases where I've initWithId or initWithArray, that all return void. Ewwww
  * Part of this, is the idea that in order to help retrain my thinking. I need to do more functional thinking in my daily javascript
  *

```objc
 + (void)initialize
    {
        if(self == [WhateverClass class])
        {
            ...perform initialization...
        }
    }
```

### Procedural/Imperative programming

* simply contain a series of computational steps to be carried out.
* Any given procedure might be called at any point during a program's execution, including by other procedures or itself.
* declarative code communicates more effectively than imperative code. Don't at me.

```js
//imperative
function meow(props) {
  var x = props[0],
    y = props[1],
    arr = props.slice(2);
  //...
}

//declarative
function soup([x, y, ...args] = []) {
  //.. that's it??
}
meow([2, 4, 6]); //i guess I can figure out which is which
soup([1, 3, 5]); //shorter yeah, but really more concise, and less error prone
```

* meow works really hard on the **HOW** all the parameters are assigned
* soup uses deconstructing the _hide_ the details how the parameters are assigned, left to focus on the **WHAT** we're trying to do.

### Output

* Undefined is the value returned implicitly if you have no return or if you just have an empty return
* Holy moly!?!?!? really. Had no idea
* We want to be explicit! Not sneaky

### Side Effects

* I think this is the winning feature of FP for me. So many times, I've been bitten by a function call that does this thing, and just happens to do this other thing too.
* This goes hand in hand with immutability. The inablitiy to change the value of something implicitly.

### Inputs

* unary: consisting of or involving a single component or element
* idenity: function that returns the input
* partial application

```js
function unary(fn) {
  return function onlyOneArg(arg) {
    return fn(arg);
  };
}

const _unary = fn => arg => fn(arg);

// ["1","2","3"].map( unary(parseInt) );
["1", "2", "3"].map(_unary(parseInt));
```

### Why Functional

* Why Functional Programming Matters by John Hughes
  * 2 Points:
  1. Higher order functions
  2. Lazy Loading

### Final Thoughts

* the complexity and cognitive overhead of your program grows exponentially as you add more local mutable state and side effects.

> There are two ways of constructing a software design: One way is to make it so simple that there are obviously no deficiencies, and the other way is to make it so complicated that there are no obvious deficiencies.

C.A.R. Hoare, 1980 ACM Turing Award Lecture

## Picks

* [Day One](http://dayoneapp.com/)
* [Why Why Functional](http://raganwald.com/2014/12/20/why-why-functional-programming-matters-matters.html)
* [Why Functional Programming Matters](http://www.cse.chalmers.se/~rjmh/Papers/whyfp.html)
* [Clojure: Programming with Hand Tools](https://www.youtube.com/watch?v=ShEez0JkOFw)

## Resources

* [Kyle Simpson. “Functional-Light JavaScript.”](http://fljsbook.com/)
* [Professor Franklin Risby](https://github.com/MostlyAdequate/mostly-adequate-guide)
* [Functional Javascript workshop](https://www.npmjs.com/package/functional-javascript-workshop)

## Follow

* JavaScript to Elm
  * Twitter: [@jstoelm](https://twitter.com/jstoelm)
  * Email: [hello@jstoelm.com](mailto:hello@jstoelm.com)
* Jesse Tomchak
  * Twitter: [@jtomchak](https://twitter.com/jtomchak)

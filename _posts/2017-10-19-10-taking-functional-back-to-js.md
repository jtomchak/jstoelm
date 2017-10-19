---
layout: post
title: '10: Taking Functional Back to JS'
date:   2017-10-18
audioURL: 'e010-taking-functional-back-to-js' 
categories: episodes
excerpt_separator: <!--more-->
---
We're gonna look at some of the core functional principles that we've learned thus far in using Elm. And how we can, as JS developers, leverage these in our day to day jobs with JavaScript. The idea being that a lot of us aren't writing Elm or Haskell for work, those that are, I am genuinely happy and excited for, it not a bit jealous.  
<!--more-->
<!-- TOC -->

- [Functional Principles](#functional-principles)
  - [function currying](#function-currying)
  - [function composition](#function-composition)
- [Picks](#picks)
- [Follow](#follow)
- [Resources](#resources)

<!-- /TOC -->

## Functional Principles 
* What we're not talking about. Using flow or Typescript will give us types,(I even linked CoffeeScript 2 in last weeks show) and that can be a lot of help in the loose wild west that JS can be. But this is less about tooling, and more about methods, thoughts, problems solving ideas that we use in languages like Elm and Haskell, languages that encourage us to think about the model design first and the declaritively write our view. These are the things we're gonna try and focus on, and yeah, it will likely touch on tooling to help us. 
* What better way to help us reinforce this new ideas then to using them in our daily work. 
* What does functional solve for us?
  * State and mutable values are hard to follow, or reason about.
  * Composition
* lodash
  * > The lodash library, by John-David Dalton, offers many things JavaScript doesn’t: consistency, performance and a suite of functions for doing common or otherwise error-prone tasks. There are almost 300 functions in lodash, with the package receiving over 20 million downloads per month. It’s a fantastic piece of work.
  * Web applications that include lodash can be big, best to import only what you need. _code splitting_
  * Now I have typically avoided util libs like lodash, I didn't want to become dependant on a 3rd party lib for working with JS. I wanted to always be able to knock it out in vanilla javascript. But at this point, if we really want to leverage the fundumental ideas of functional programming we're gonna need some help with it. 
* Features to bring back to the dark side (JS)
### function currying
  * A function that takes a function with multiple parameters as input and returns a function with exactly one parameter.
  * We've talked about curring before, but here's a quick overview. Named after [Haskell Curry](https://en.wikipedia.org/wiki/Haskell_Curry). And yes, I finally when to his wiki page. Fun fact: he was born September 12, 1900, Millis, Massachusetts, U.S.—died September 1, 1982
  * currying is the technique of translating the evaluation of a function that takes multiple arguments (or a tuple or more of arguments) into evaluating a sequence of functions, each with a single argument. Remembering that the previous argument values are still available in the lexical scope of the function.
  * Partial application **NOT THE SAME THING** as curry! takes a function with multiple parameters and returns a function with fewer parameters.Here we are returning a function that takes the remaining arguments. Subtle, but gotta know. fundumentals are FUN. 
  * in JS, I often hear it described as a function that returns a function. ugh.

```js
import _ from 'lodash';
funtion addBy(x){
  return function(y){
    return x + y
  }
}
const addByTen = addBy(10);
addByTen(3) //--> 13

//Now in lodash
const add = (x, y) => x + y
const addByTen = _.partial(add, 10); 
//now a function where the the first 
//argument in add is bound with 10
addByTen(7); //--> 17

/*
We could also right it like
Lots of ES2015 here, but just a 
function that returns a 
function, akin to the first version
*/
const add = x => y => x + y
add(10)(4) //--> 14
```

### function composition 
* Follow along at home [JSBin](http://jsbin.com/jixaduy/6/edit?js,console)
* pass results from one step to the next
* Put simply, a composition of functions `f` and `g` can be defined as `f(g(x))`, which evaluates from the inside out — right to left. In other words, the evaluation order is: x _then_ g _then_ f. 😡
* I've struggle with definitions like this while I learn fp, Elm, and Haskell. To me it feels like when you ask someone the definition of a word, and then use **that** same word in the definition!!! 😡😡 Double rage face!! sometimes a Circular definition. For those of us onboarding, it's using the exact parts we don't understand to try and explain things to us! That's when you get double angry face.
* Anywho. Regular mode.
* compositional - This is where we would want to pass the output of inside function to the next function and so on and so forth. But rather than nexting it and have it 'bubble up'. bc it's silly hard to read. 
* compositional with fp.compose: So with reduce(), we have a list that applies a function to each one and accumulates the results. But it does it from left to right. D'oh. we need it to run from right to left, so it's inside to out. Oh, cool, there's something called reduceRight()! for lodash, it's called compose()
* what's cooler than compose from right to left, pipe that compositional works from left to right! (drops mic). umm, but wait where is the value or referance that compose and pipe are working on? From JS, this looks a bit weird, unsettling even. in reg mode we get a referance to current input most levels. 

```js
/*
The idea here is to turn the string passed to 
this function into a url slug. 
we split to array by word, map over each 
word and lower case,then squish it 
back together with a dash inbetween it
*/

// Use `noConflict` to restore the pre-fp variant.
var fp = _.noConflict();
const trace = label => {
  return fp.tap(x => console.log(`--> ${ label }:  ${ x }`));
};

//Regular mode
const toSlug = input => encodeURIComponent(
  input.split(' ')
  .map(word => word.toLowerCase())
  .join('-')
)
console.log(toSlug("JS To Elm"));


/*
Nested, and also Ewwwww
so this evaluates from right to left, inside out.
Pretty hard to read?
*/
const toLowerCase = str => str.toLowerCase();
const ew_toSlug = input => encodeURIComponent(
  fp.join('-')(
    fp.map(toLowerCase)(
      fp.split(' ')(
        input
      )
    )
  )
);
console.log(ew_toSlug("JS To Elm"));


//lodash FP using reduceRight, or compose
const _toSlug = fp.compose(
  encodeURIComponent,
  fp.join('-'),
  fp.map(toLowerCase),
  fp.split(' ')
); 
console.log(_toSlug("JS To Elm"));



//lodash FP using reduce with composition, or pipe
const _pipetoSlug = fp.pipe(
  trace("input"),
  fp.split(' '),
  fp.map(toLowerCase),
  fp.join('-'),
  encodeURIComponent
);
console.log(_pipetoSlug("JS To Elm"));
```

## Picks
* [Haskell for teaching](http://profsjt.blogspot.ca/2017/10/is-haskell-right-language-for-teaching.html)
* [Pixel Kit](https://kano.me/store/us/products/pixel-kit)

## Follow
* JavaScript to Elm
  * Twitter: [@jstoelm](https://twitter.com/jstoelm)
  * Email: [hello@jstoelm.com](mailto:hello@jstoelm.com)
* Jesse Tomchak
  * Twitter: [@jtomchak](https://twitter.com/jtomchak)

## Resources
* [Professor Frisby TV](https://egghead.io/courses/professor-frisby-introduces-composable-functional-javascript)
* [Professor Frisby Book](https://drboolean.gitbooks.io/mostly-adequate-guide/content/)
* [lodash fp](https://github.com/lodash/lodash/wiki/FP-Guide)
* [chain for lodash](https://medium.com/making-internets/why-using-chain-is-a-mistake-9bc1f80d51ba)
* [Eric Elliot](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-function-composition-20dfb109a1a0)
* [Partial Application](http://benalman.com/news/2012/09/partial-application-in-javascript/)



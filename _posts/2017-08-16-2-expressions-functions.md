---
layout: post
title: '2: Expressions & Functions'
date:   2017-08-21
audioURL: 'e002-Expressions-And-Functions'
categories: episodes
excerpt_separator: <!--more-->
---


<!--more-->
<!-- TOC -->

- [News and updates](#news-and-updates)
- [Expressions](#expressions)
- [Functions](#functions)

<!-- /TOC -->
## News and updates
* reach out, send a message to me on twitter @jstoelm
* [Elm Conf](https://www.elm-conf.us)
* thank Greg and Jason, the amazing guys over at [Dawn of the Dev](https://itunes.apple.com/us/podcast/dawn-of-the-devs-podcast/id1256007479?mt=2) for all their work in educating, helping, and promoting new developers from all walks of life into our fantastic community.


## Expressions
Using the elm-repl (read, evaluate, print, loop)
* Building with '+' for numbers and '++' for strings
	* No ability to add numbers and strings, '+' only for numbers. sweet.

	"hello " ++ "world"
	"hello world" : String --output

* "Double quotes in Elm represent string literals, just like in JavaScript, but single quotes in Elm represent **character** literals."
* Comments using -- instead of // and for blocks {- -} instead of using /* */ like in JS. And you'll hear me do this sort of comparison a lot through this process of learning Elm. I want to relate it to something that I know, but I hope that I can tie it into something that you might be familiar with.
* Math, yep it works the same.
* Assigning constants
  * The equal sign, or assignment operator `=`
  * no 'var' or 'let' keyword
  * name must begin with a lowercase letter
  * not a rule, but convention is uninterupted letters, mp3: ok, mp3cassette: nope
  * more convention is camelcase, not snakecase, or **SMCREAMING_SNAKE_CASE**
  * you can also assign, not only a literal value, like "kitten" or 6, but also expressions
>Expression: anything that evaluates to a single value
* Elm has if-expressions, **NOT** if-statments
  * bc it must evalutate to a value, it cannot just be a regular statement
* Booleans and Conditionals
  * only 2 values, True and False, capitalized bc it's a type
  * subtle differences
```elm
age = 30
age == age --True
age /= age --False
not (age == age) --False, using the keyworkd not
age <= 0 || age >= 10 --True, using || pipe operator
age > 0 && age < 100 --True, using && and operator
```
  * Conditionals
```elm
--if expression
miceValue = if blindMice == 1 then
  "mouse"
else
  "mice"
```
```javascript
//JS ternary
const miceValue = blindMice === 1 ? "mouse" : "mice"
```
  1. A condition
  2. A section to evaluate if the condition passes
  3. A section to evaluate to the thing if it fails
  * also have else if, Elm will use nested expressions quite a lot as we'll see in the future
```elm
if blindMice == 1 then
  "mouse"
else if blindMice >= 0 then
  "mice"
else
  "cat"
```
  * Only True and False, no truthy, thank god
    * Javascript has type conversion, which we'll dive into far more detail later on, but at it's basic level, the following will evaluate to false, or 'falsy'
```javascript
if (false)
if (null)
if (undefined)
if (0)
if (NaN)
if ('')
if ("")
if (document.all) [1]
//random browser detection for legacy reasons. Thanks IE!
```

## Functions
[Elm from Javascript Docs](http://elm-lang.org/docs/from-javascript)
>Elm functions represent reusable logic. They are not objects. They have no fields, no prototypes, and no ability to store state. All they do is accept values as arguments, and then return a value. [^1]

>(Javascript)... function is composed of a sequence of statements called the function body. Values can be passed to a function, and the function will return a value. In JavaScript, functions are first-class objects, because they can have properties and methods just like any other object. [^2]

* Let's unpack this, but first, my struggle. Where are the blocks?? Instead of wrapping all arguments in parentheses and separating them with commas, we use spaces to apply the function. So (add(3,4)) becomes (add 3 4) which ends up avoiding a bunch of parens and commas as things get bigger. Does it look cleaner? A better question is, can I get used to it.

* Let's unpack those. Elm functions are not objects, have no special properties, they take input and return output. Not an object, so no prototypal inheritance.

* All functions in Elm are curried by default. If you have "a function of 2 arguments", it's really a function that takes one argument and returns a function that takes another argument.
```elm
> fullName fName lName = fName ++ " " ++ lName
<function> : String -> String -> String

> fullName "Jesse"
<function> : String -> String

> lastName = fullName "Jesse"
<function> : String -> String

> lastName "Tomchak"
"Jesse Tomchak" : String

> superName fname lname = (String.append fname " ") ++ lname
<function> : String -> String -> String
> superName "Jesse" "Tomchak"
"Jesse Tomchak" : String
```




[^1]:Excerpt From: Richard Feldman. 'Elm in Action MEAP V05.'
[^2]:Functions in JavaScript from MDN

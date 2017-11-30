---
layout: post
title: '15: Maybe, Just, and Nothing'
audioURL: e015-maybe
categories: episodes
excerpt_separator: <!--more-->
---

Maybe is a container, union type, type constructor. So, um, what does that mean?
In Elm, null and undefined are not valid types, so what do we do when we might
not have something? Let's figure it out, and when it's useful.

<!--more-->

<!-- TOC -->

* [Maybe Type](#maybe-type)
  * [Historical](#historical)
  * [Practical](#practical)
  * [Then we have Maybe.andThen](#then-we-have-maybeandthen)
  * [Pipe Operator](#pipe-operator)
  * [So why is Maybe important?](#so-why-is-maybe-important)
* [Picks](#picks)
* [Resources](#resources)
* [Follow](#follow)

<!-- /TOC -->

## Maybe Type

`type Maybe a = Just a | Nothing`

### Historical

* It's just a union type, nothing scary, right? It's gonna be Just with a value,
  or Nothing. Notice that I have typed these with capital letters. They are
  types, not values.
* The Maybe type encapsulates an optional value. A value of type Maybe a either
  contains a value of type a (represented as Just a), or it is empty
  (represented as Nothing). Using Maybe is a good way to deal with errors or
  exceptional cases without resorting to drastic measures such as error.
* The Maybe type is also a monad. It is a simple kind of error monad, where all
  errors are represented by Nothing. A richer error monad can be built using the
  Either type.
* What did you say? Mona-wanta-who-now?
  > Monads in Haskell can be thought of as composable computation descriptions.
* [More info - Lambdacast](https://soundcloud.com/lambda-cast/18-monads)

### Practical

* How do I get something out of this thing to work with ?
  * The maybe module to the rescue! Let's look at a simple example

```bash
> fruit = ["apple", "banana", "mango"]
["apple","banana","mango"] : List String

# we know that the head of a a list will return Maybe String

> listHead = List.head fruit
Just "apple" : Maybe.Maybe String

# ok so listHead gives us back 'Just "apple"'
# Which is of type Maybe.Maybe String
# So what if we want the actual tangable value.
# We can't very well put Just Apple to the DOM!

> Maybe.withDefault "None" (List.head fruit)
"apple" : String

# Here we're able leverage the Maybe module with
# Maybe.withDefault which will 'unwrap' the
# maybe and if it's a type Nothing, then give us the default,
# otherwise it will give use the
# value from the Just.
# Now we have the actual string "apple" to render to the DOM.
# This is a bit better than a
# case expression everytime we want to unwrap a maybe
```

* That works if we know we're gonna get a maybe and have a default value. What
  if we have a situation like our Json decoding where we need to map3 or map4
  and transform value a -> b? Good question. The answer map.maybe
* map.maybe will transform any maybe value if it's a Just type, otherwise it
  will return nothing. In this way, it will take the maybe a and transform it
  and return a Just b or Nothing. From the source code.
  > Apply a function if all the arguments are `Just` a value.

```bash
> fruit
["apple","banana","mango"] : List String

# Even though these are maybe types, we are able to transform them, as long as all of them are Just values and not Nothing!
> Maybe.map2 (\a b -> (a ++ ", " ++ b)) first second
Just "apple, banana" : Maybe.Maybe String

#And if we have a Nothing instead of a Just value
> Maybe.map2 (\a b -> a ++ ", " ++ b) (List.head nope) (Just "Ted")
Nothing : Maybe.Maybe String
```

### Then we have Maybe.andThen

* `> Maybe.andThen <function> : (a -> Maybe.Maybe b) -> Maybe.Maybe a ->
  Maybe.Maybe b`
* So what does this thing do? Let's break it down, reading the Type annotation.

1. The first argument is a function, that takes 'a', and returns 'Maybe b'
2. The second argument is value of type Maybe
3.

* So if we want the head of a (Maybe (List String)), we can't just call
  `List.head tail`.....nope.

```bash
> List.head tail
-- TYPE MISMATCH ------------------------------ repl-temp-000.elm

The argument to function `head` is causing a mismatch.

3|   List.head tail
               ^^^^
Function `head` is expecting the argument to be:

    List a

But it is:

    Maybe (List String)
```

* So what do we do ?

```bash
> Maybe.andThen List.head  tail
Just "banana" : Maybe.Maybe String

# Snuck a pipe operator in there on you
> Maybe.andThen List.head  tail \
| |> Maybe.andThen (\s -> Just (String.toUpper s))
Just "BANANA" : Maybe.Maybe String
```

### Pipe Operator

* Used to use infix, falled out of favor for readablility
* See the backticks. ewwwwwwwww

```bash
Just[]`Maybe.andThen`List.head`Maybe.andThen`(\s -> Just (String.toUpper s)) -- ->
  Nothing
#or just as bad
Maybe.andThen (\s -> Just (String.toUpper s)) (Maybe.andThen List.head  (Just[]))
```

* Think of the pipe as feeding or passing a value into the next function.
* This is prefered to nesting. We do this in JS all the time. Sort of evaluate
  from the inside out, tracking the value manaully in our heads. Gross

### So why is Maybe important?

* We can't avoid possiblly not getting a value, like we can in JS. **_cough_**
  **_cough_** _undefined_. Elm forces us to deal with any edge cases where
  maybe, might not actually be there. I for one, have become very good at lying
  to myself about the 'possible' values in JS. Phrased like, "oh, I didn't know
  that could happen", or "what in the world, how did you get that"
*

## Picks

* [Daily Drip](https://www.dailydrip.com/topics)
  ![inline](https://elixirforum.com/uploads/default/original/2X/e/e705946bc6c7478088528ce4bd76ff7c51531b85.png)
  * 1890 minutes of video in 90 sections. wowzer, that's a lot of elm
* [wasm32-unknown-unknown landed & enabled](https://www.hellorust.com/news/native-wasm-target.html)

## Resources

* [Offical Docs, Maybe](https://guide.elm-lang.org/error_handling/maybe.html)
* [Haskell Docs](https://hackage.haskell.org/package/base-4.10.0.0/docs/Data-Maybe.html)
* [Dealing with maybe](http://rundis.github.io/blog/2016/elm_maybe.html)
* [Where did undefined and null go?](https://github.com/elm-guides/elm-for-js/blob/master/Where%20Did%20Null%20And%20Undefined%20Go.md)
* [Elm Maybe](https://dennisreimann.de/articles/elm-maybe.html)
* [Elm Core](https://github.com/elm-lang/core/blob/master/src/Maybe.elm)
* [Elm Pipes](https://github.com/elm-lang/elm-lang.org/blob/master/src/examples/pipes.elm)

## Follow

* JavaScript to Elm
  * Twitter: [@jstoelm](https://twitter.com/jstoelm)
  * Email: [hello@jstoelm.com](mailto:hello@jstoelm.com)
* Jesse Tomchak
  * Twitter: [@jtomchak](https://twitter.com/jtomchak)

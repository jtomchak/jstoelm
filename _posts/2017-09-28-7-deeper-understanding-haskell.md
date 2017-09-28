---
layout: post
title: '7: Deeper Understanding with Haskell'
date:   2017-09-27
audioURL: 'e007-Deeper-Understanding-Haskell'
categories: episodes
excerpt_separator: <!--more-->
---
We take a slight detour with this episode from the Elm Architecture to dive into the Language Haskell. Elm is very Haskell like, and borrows a lot of types, terminology, and syntax from this pure functional language. So it's a good idea to understand where Elm is coming from, so we have a better understanding of where we're going. 
<!--more-->
<!-- TOC -->

- [News and updates](#news-and-updates)
- [Learning Haskell](#learning-haskell)
- [Picks](#picks)
- [Follow](#follow)

<!-- /TOC -->


## News and updates
  * Keeping these short, and make sure that these episodes remain focused on the goal...learning Elm by doing. 
  * Elm Conf is anyday now. I'm hoping to binge watch them all, and will likely to a bonous episode on all the talks, in addition to my weekly learning. 


## Learning Haskell
![inline](https://imgs.xkcd.com/comics/haskell.png)
* Why I think it might be important?
  * (Elm compiler)[https://github.com/elm-lang/elm-compiler] is written in Haskell
  * Nothing 'Truthy' *Haskell cannot compare two values that have different types.* No coercion.
  * I am seeing some 'Swifty' things in Elm, like the maybe or as I learned it, the optional. Also the let .. in expression is something I learned from Swift. Infact, the more I learn, the more I think, oh man, that was borrowed from Haskell! Where did Haskell get if from? So why not go to the source?


* [Learning Haskell](https://www.futurelearn.com/courses/functional-programming-haskell)
  * University Of Glasgow, Future Learn dot com
  * Setting up Haskell for Mac [LINK](https://medium.com/@dogwith1eye/setting-up-haskell-in-vs-code-on-macos-d2cc1ce9f60a)
    * Wk 1
      * Defining a function: a function defines an expression with variables
      * Lambda functions: functions don't need a name
      * The list datastructure: the key datastructure in Haskell
      * Constructing lists: the (:) and (++) operators, sequences, comprehensions
      * Manipulating lists: indexing, head and tail
    * Wk 2
      * Infix operators. But these have been removed from Elm, if I remember correctly
      * Equality and Comparison Operators
      * Input and output (I/O) operations are impure. They influence and interact with the ‘outside world’. Essentially, this is the only way to make computers do interesting things. Ah, this is because the order if (I/O) is so very important.
      * The **do** notation allows us to sequence actions.
      * The *bind* operator accomplishes this function sequencing. It is a key part of the IO *monad*. Getting into some heavy stuff!!
      * described as *in the IO Monad*
      * I think this sums it up very well:
      > the type system keeps us honest.

      * Zip that list
        * The zip function is used to combine a pair of lists into a list of pairs. 
        * As long as the length of the shortest list
        * zipWith in use ``` zipWith (\x->(\y->(x,y))) [1,2,3] [0,2,4] ```
      * 'list comprehension expression', a wha?
      * <- is for associating names with values in do blocks whereas -> is used for defining functions
      * Monads are a powerful tool for sequencing operations.
      * Installing locally [Installer and Docs](https://www.haskell.org/platform/mac.html#osx-homebrewcask)
        * That part for me is fairly straight forward. . I like configuration and setup, I've done fair amount of it in the past working as a sysAdmin.
      * Building starman the game,
        * [Gist](https://gist.github.com/jtomchak/7ecf0d358c4b6fab5055ed37db6abcb6)
        * It’s always helpful to work out the type of a function first.(good tip, lol) *specification before implementation*
        * Man this was tough. Baby steps. I like starting with the types, and thinking about the data and the model first. What i'm taking in, and what I am expecting out. It feels more thought out, and pragmatic. It is also going to take a dumpster load of practice before I feel comfortable with this. 

```haskell
--starman super game

--the arrow pointing left is throwing me for a loop i am hoping that syntacticly it will grow on me, it's read as 'x is given the value of word'
starman :: String -> Int -> IO ()
starman word n = turn word ['-' | x <- word] n

--checking the guessed letter against the word
check :: String -> String -> Char -> (Bool, String)
check word display c =
  ( c `elem` word --if c is in the word, 
  , [ if x == c
      then c
      else y
    | (x, y) <- zip word display
    ]) --not entirely sure where the x is coming from

--increment turn count, either end with win/loss or invoke make guess function
turn :: String -> String -> Int -> IO ()
turn word display n = do
  if n == 0
    then putStrLn "You Lose"
    else if word == display
        then putStrLn "You Totally Win"
        else mkguess word display n

--make a guess from the user, get input from terminal
mkguess :: String -> String -> Int -> IO ()
mkguess word display n = do
  putStrLn (display ++ "  " ++ take n (repeat '*'))
  putStr "  Enter your guess: "
  q <- getLine
  let (correct, display') = check word display (q !! 0)
  let n' =
        if correct
          then n
          else n - 1
  turn word display' n'
```
        



## Picks
* [Make the Leap from JavaScript to PureScript – Hacker Noon](https://hackernoon.com/make-the-leap-from-javascript-to-purescript-5b35b1c06fef?gi=5c3feba5b1b) by Alex Kelley
* [Haskell Pretty Print](https://github.com/commercialhaskell/hindent)
* Learning Books for Haskell
  * [Haskell Programming](http://haskellbook.com/)
  * [Haskell: the Craft of Functional Programming](http://www.haskellcraft.com/craft3e/Home.html)
  * [Programming in Haskell](http://www.cambridge.org/9781316626221)
  * [Learn You A haskell](http://learnyouahaskell.com/)
  * [Real World Haskell](http://book.realworldhaskell.org/) --this one is older using v6.8 and fairly out of date at this point. 



## Follow
* JavaScript to Elm
  * Twitter: [@jstoelm](https://twitter.com/jstoelm)
  * Email: [hello@jstoelm.com](mailto:hello@jstoelm.com)
* Jesse Tomchak
  * Twitter: [@jtomchak](https://twitter.com/jtomchak)

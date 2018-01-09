---
layout: post
title: '20: Building a compiler. Part 1'
audioURL: **MP3TRACK**
categories: episodes
excerpt_separator: <!--more-->
---

Something I've wanted to know more about, having missed out on the usual opportunity during a CS degree, is the process of a compiler. How we get from source code to running byte code on the other end. The process of writing Elm that compiles to JavaScript using a compiler written in Haskell, was the tipping point for me. Compound that with webpack walking the Abstract Syntax Tree, and learning the term 'lexical scope' from Kyle Simpson in his YDYJS series.

<!--more-->

<!-- TOC -->

* [Compilers aren't scary.](#compilers-arent-scary)
* [What is it Compiler or Interpreter, what's the difference?](#what-is-it-compiler-or-interpreter-whats-the-difference)
* [Steps of a](#steps-of-a)
  * [Compiler](#compiler)
  * [Interperter](#interperter)
* [What we're actually building](#what-were-actually-building)
* [Lexical Analyis](#lexical-analyis)
  * [Defining Tokens](#defining-tokens)
  * [Actual Lexer](#actual-lexer)
  * [REPL](#repl)
* [Parsing](#parsing)
  * [Parse Generator](#parse-generator)
  * [Actual Parsing](#actual-parsing)
  * [Read-Parse-Print-Loop](#read-parse-print-loop)
* [Picks](#picks)
* [Resources](#resources)
* [Follow](#follow)

<!-- /TOC -->

## Compilers aren't scary.

Frankly, this topic, for me, above all others, has been wildly unapproachable. And this might be a case where I know more than I think, but I think the reality is, the materials I've found explaining compilers come with nothing short of a dump truck of implied knowledge, that I simply do not process. You can check the resources for an extensive list of books that've started with varing degrees of success, one that stuck, that we are going to use extensively is Thorsten Ball's "Writing an Interpreter in Go." I know what you're thinking, Go? I'll defer to Thorsten's points.

1. Go standard lib has all the things we need, including built in testing. No 3rd libs needed.
2. Go tooling is pretty great, lets us get a ton of mileage from the standard lib.
3. Easy to understand syntax, pretty C like. It's not going to be a head scratcher to read the code.
4. gofmt, is built **INTO** the language!! Sold.
5. Did I mention testing is built into the language?!?!?! How great is that!!!!

## What is it Compiler or Interpreter, what's the difference?

* A compiler takes entire program and converts it into object code which is typically stored in a file.
  * C or C++
* An Interpreter directly executes instructions written in a programming or scripting language without previously converting them to an object code or machine code.
  * Perl or Python

## Steps of a

### Compiler

1. Lexical Analysis
2. Parsing
3. Abstract Syntax Tree(AST)
4. Semantic Analysis
5. Translation to Intermediate Code
6. Code Optimizer
7. Code Generator

### Interperter

8. Lexical Analysis
9. Parsing
10. Abstract Syntax Tree(AST)
11. Evaluate code.

* We are going to go from AST to evaluating our written program. And for getting started that's great, bc I don't really know what I don't know.

## What we're actually building

* Our guide builds our a new language made for the book, it's called Monkey. I've decided to call my Meow.
* We're gonna tackle Lexing and Parsing in part 1, and evaluation will take up a majority of part 2.
* Remind me how this gets us to Elm again?
  * A fair question.
  * If there's one concert thing I learned in 2017, it's that regardless of your specific domain of knowleadge, learning more about ideas, patterns, and concepts relating to your domain, will absolutly without a doubt make you better and broaden your abilities within that specific domain.
  * For example, learning Elm has made me a better JS programmer. Learning (or struggling with) Haskell has helped when learning Elm and Functional Programming. Learning by building a compiler can only help to serve us while we try to understand the high level abstractions.

## Lexical Analyis

* the cool kids call it 'Lexing'
* First I heard of it, Kyle Simpson refers to Lexical Scope in YDYJS.
* This is the process of turning the source code into a more managable form, tokens.
* The process of going from source code -> tokens is called 'lexing' other street names include tokenizer or scanner.
* We will take the tokens and feed them into the parser, which in turn will hopfully produce the AST to be evaluated.

### Defining Tokens

### Actual Lexer

### REPL

## Parsing

### Parse Generator

### Actual Parsing

* Let Statements
* Return Statements
* Expressions
* Top Down Operator Precedence or PRATT by Vaughan Pratt
* Vocabulary
* Preparing the AST
* Implement the PRATT
* Identifiers
* Integer Literals
* Prefix / Infix Operators
* Boolean Literals
* Grouped Expressions
* Function Literals
* Call Expressions

### Read-Parse-Print-Loop

## Picks

## Resources

* [AST Explorer](https://astexplorer.net/)
*

## Follow

* JavaScript to Elm
  * Twitter: [@jstoelm](https://twitter.com/jstoelm)
  * Email: [hello@jstoelm.com](mailto:hello@jstoelm.com)
* Jesse Tomchak
  * Twitter: [@jtomchak](https://twitter.com/jtomchak)

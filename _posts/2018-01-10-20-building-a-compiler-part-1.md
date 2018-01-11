---
layout: post
title: '20: Building a compiler. Part 1'
audioURL: e020-building-a-compiler-1 
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
  * [Interpreter](#interpreter)
* [What we're actually building](#what-were-actually-building)
* [Bit of what Meow Lange will look like](#bit-of-what-meow-lange-will-look-like)
* [Lexical Analysis](#lexical-analysis)
  * [Defining Tokens](#defining-tokens)
  * [Actual Lexer](#actual-lexer)
    * [Additional Character Implementation](#additional-character-implementation)
* [Picks](#picks)
* [Resources](#resources)
* [Follow](#follow)

<!-- /TOC -->

## Compilers aren't scary.

Frankly, this topic, for me, above all others, has been wildly unapproachable. And this might be a case where I know more than I think, but I think the reality is, the materials I've found explaining compilers come with nothing short of a dump truck of implied knowledge, that I simply do not process. You can check the resources for an extensive list of books that i've started with varying degrees of success, one that stuck, that we are going to use extensively is Thorsten Ball's "Writing an Interpreter in Go." I know what you're thinking, Go? I'll defer to Thorsten's points.

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

### Interpreter

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
  * If there's one concert thing I learned in 2017, it's that regardless of your specific domain of knowledge, learning more about ideas, patterns, and concepts relating to your domain, will absolutely without a doubt make you better and broaden your abilities within that specific domain.
  * For example, learning Elm has made me a better JS programmer. Learning (or struggling with) Haskell has helped when learning Elm and Functional Programming. Learning by building a compiler can only help to serve us while we try to understand the high level abstractions.

## Bit of what Meow Lange will look like

```sh
let five = 5;
let ten = 10;

let add = fn(x, y){
  x + y;
};

let result = add(five, ten);
!-/*5;
5 < 10 > 5;

if (5 < 10) {
  return true;
} else {
  return false;
}

10 == 10;
10 != 9;
```

## Lexical Analysis

* the cool kids call it 'Lexing'
* First I heard of it, Kyle Simpson refers to Lexical Scope in YDYJS.
* This is the process of turning the source code into a more manageable form, tokens.
* The process of going from source code -> tokens is called 'lexing' other street names include tokenizer or scanner.
* We will take the tokens and feed them into the parser, which in turn will hopefully produce the AST to be evaluated.

### Defining Tokens

* defining the tokenType to be a string. easy to debug, we could use int or byte for more preformate, but string works for us. let's walk before we run. #preoptimizing
* Illegal, EOF,
* Identifiers and literals, like INT or IDENT (1, 2, 3) or (minus, foobar, _otherfunctionname_)
* Operators, = + ,
* Delimiters, (, ;, (, ), {, })
* Keywords, FUNCTION or LET

### Actual Lexer

* gonna read through the source code one character at a time, and 'translate' it all into tokens. every '+' or 'LET' keyword. will be tokenized.
* Only supporting ASCII, and not the full Unicode range. Fully Unicode & UTF-8 would need to not an increment, but a rune? bc each character could be several bytes!!!
* rune: 'The Go language defines the word rune as an alias for the type int32, so programs can be clear when an integer value represents a code point. Moreover, what you might think of as a character constant is called a rune constant in Go. The type and value of the expression'
  * so like the '⌘' is rune with integer value 0x2318.
* These tests are super nice to have. Man, so nice
* Need to walk the word to see if it's an lang identifier and then
* Gotta account for the white space between keywords and identifiers.
* Then we've got to handle numbers, like 5,6, or 239048

#### Additional Character Implementation

* '==', '!', '!=', '-', '/', '\*', '<', '>'
* these will fall into one of 3 categories
  1. one-character token
  2. two-character token
  3. keyword token
* Side note, Go Lang will not test/run/compile if you are importing unused packages like 'fmt'

- Let Statements
- Return Statements
- Expressions
- Top Down Operator Precedence or PRATT by Vaughan Pratt
- Vocabulary
- Preparing the AST
- Implement the PRATT
- Identifiers
- Integer Literals
- Prefix / Infix Operators
- Boolean Literals
- Grouped Expressions
- Function Literals
- Call Expressions

## Picks

* [Rexpad](https://www.rexpad.com/)
* [Papers I read and loved](https://pixel-druid.com/blog/papers-i-read-and-loved-in-2017/)
* [Serverless Haskell](https://github.com/seek-oss/serverless-haskell)

## Resources

* [Writing An Interpreter In Go](https://interpreterbook.com/)
* [Go Docs](https://golang.org/)
* [AST Explorer](https://astexplorer.net/)
* [Meow Lang](https://github.com/jtomchak/Meow)
* [Dragon Book](https://www.amazon.com/Compilers-Principles-Techniques-Tools-2nd/dp/0321486811)
* [Super Tiny Compiler](https://github.com/thejameskyle/the-super-tiny-compiler)

## Follow

* JavaScript to Elm
  * Twitter: [@jstoelm](https://twitter.com/jstoelm)
  * Email: [hello@jstoelm.com](mailto:hello@jstoelm.com)
* Jesse Tomchak
  * Twitter: [@jtomchak](https://twitter.com/jtomchak)

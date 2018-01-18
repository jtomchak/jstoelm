---
layout: post
title: '21: Building a compiler. Part 2'
audioURL: e021-building-a-compiler-part-2
categories: episodes
excerpt_separator: <!--more-->
---

In full swing building our ~~compiler~~ interpreter. We've got our lexer working nicely. Now for the meaty part of it. The process of taking all the source code that is now tokenized, and outputting into a data structure is the job of the parser. This output structure is called a 'syntax tree' or 'abstract syntax tree', did you checkout last week's pick?

<!--more-->

<!-- TOC -->

* [Parsing](#parsing)
  * [Technical details of Meow's parser](#technical-details-of-meows-parser)
  * [Parse Generator](#parse-generator)
  * [The actual parsing...](#the-actual-parsing)
  * [Recursive Descent Parser](#recursive-descent-parser)
    * [Parsing Expressions](#parsing-expressions)
  * [Abstract Syntax Tree](#abstract-syntax-tree)
* [Picks](#picks)
* [Resources](#resources)
* [Follow](#follow)

<!-- /TOC -->

## Parsing

### Technical details of Meow's parser

* Two main ways to tackle parsing
  1. top-down
  * building the root node of the AST and then working downward and out
  * When the parser starts constructing the parse tree from the start symbol and then tries to transform the start symbol to the input, it is called top-down parsing.
  2. bottom-up
  * goes the other way. lol.
  * As the name suggests, bottom-up parsing starts with the input symbols and tries to construct the parse tree up to the start symbol.
  * Within this are a few variations.
* Meow will be a recursive descent parser
  * top down operator precedence,
  * called the "Pratt parser", after Vaughan Pratt

### Parse Generator

* Dude, I know, well I didn't know, but now I vaguely know.
* Sort of defeats the purpose of learning to just use the off the self parse generator.

### The actual parsing...

* starting with 'let'
  valid Meow code

```js
let x = 10;
let y = 15;

let add = fn(a,b){
  return a + b;
}
```

* Statements and Expressions

1. Simply put, expressions produce values - statements don't. **SIMPLE**

* What a node for a variable binding in the `let x = 5;` would be ?

### Recursive Descent Parser

* Parsing token and tokenPeek to see what the next token is to invoke the right parsing function
* Then calling parsing function based on the token type.
* `parseLetStatement` or `parseIdentifier`
* As we start to parse we are checking tokens, and peeking at the next token, but there are troubles!

  * prefix operators `!true`
  * infix operators `5 + 5`
  * comparison operators `x == y`
  * call expressions `add(2,3)` or `add(add(2,3), 12)`
  * oh noes, identifiers are expressions too! `bar * foo / foobar`
  * first class functions & function literals

* But it gets tricky when you get to expressions as you can see.
* You have to write separate functions for each level of precedence (JavaScript has 17 of them, for example),
* Pratt to the rescue.
  * > BNF grammars and their various offspring.
  * He's talking about parsing generators. where we feed them some formal description, and they output the parser for you.
  * > technique is simple to understand, trivial to implement, easy to use, extremely efficient, and very flexible
  * Douglas Crockford, "Another explanation is that his technique is most effective when used in a dynamic, functional programming language."
  * Douglas Crockford, "JavaScript is an ideal language for exploiting Pratt's technique"

#### Parsing Expressions

* a bit more difficult bc a let can only appear once at the beginning of statement. **HOWEVER** in an expression, tokens of the same type, can appear in multiple positions!!!!!
* association of parsing functions called "semantic code" with token types.
* whenever these token types are encountered the parsing functions are called
* each token type can have up to two parsing functions associated with it, depending if the token is in prefix or infix
* so we have two parsing functions
  1. prefixParseFn - 'nuds' or 'null denotations'
  2. infixParseFn(ast.Expression) - 'leds' or 'left denotations'
* Both return an ast.Expression, but notice that infixParseFn takes an argument, prefixFarseFn does not.
  * the argument is to the left of the infix operator
* parsingExpression we use an enum iota, so that we can assign precedence for infix's like `>= + * !X`
  * Automate enum values with: iota
    → A numeric universal counter starting at 0
    → Used only with constant declarations
* Executing Pratt's Parser

  * don't represent every operator / operand, but rather nest the nodes correctly
  * treat the expression as a whole and then loop over it from left to right, using a set of conditionals
    if the next token is a not SEMICOLON **&&** the precedence of the the following token is greater than the precedence of the current token.
  * higher precedence is to be deeper in the AST.
  * right-binding power
  * left-binding power
  * these are the parts of `precedence < p.peekPrecedence` where right-binding power is precedence and left-binding is peekPrecedence

### Abstract Syntax Tree

What we're shooting for, more or less.
![AST](https://www.researchgate.net/profile/Peter_Fritzson/publication/228792639/figure/fig1/AS:393782852898820@1470896556105/Figure-1-Abstract-syntax-tree-of-the-while-loop.png)

## Picks

* [Interview with Simon Peyton-Jones](http://www.cs.cmu.edu/~popl-interviews/peytonjones.html)
  * Simon Peyton-Jones (Microsoft Research Cambridge) researches the implementations and applications of functional programming languages. He was heavily involved in the design of the Haskell programming language and the development of the Glasgow Haskell Compiler (GHC). We talk about seeing functional programming go from intellectual revolution to practical reality and the importance of investing in programming education.
* [The Good War](https://thenib.com/the-good-war)
  * How America’s infatuation with World War II has eroded our conscience by Mike Dawson and Chris Hayes

## Resources

* [Top Down Operator Precedence](https://web.archive.org/web/20151223215421/http://hall.org.ua/halls/wizzard/pdf/Vaughan.Pratt.TDOP.pdf)
* Left Recursion: A grammar becomes left-recursive if it has any non-terminal ‘A’ whose derivation contains ‘A’ itself as the left-most symbol.
* Associativity: If an operand has operators on both sides, the side on which the operator takes this operand is decided by the associativity of those operators.
* [EcmaScript AST](http://tomcopeland.blogs.com/EcmaScript.html)
* [JSLint](http://www.jslint.com/)
* [JS the Good Parts](https://www.amazon.com/exec/obidos/ASIN/0596517742/wrrrldwideweb)
* [Pratt Parsers: Expression Parsing Made Easy](http://journal.stuffwithstuff.com/2011/03/19/pratt-parsers-expression-parsing-made-easy/)
* [Douglos Crockford Top Down Operator Precedence](http://crockford.com/javascript/tdop/tdop.html)

## Follow

* JavaScript to Elm
  * Twitter: [@jstoelm](https://twitter.com/jstoelm)
  * Email: [hello@jstoelm.com](mailto:hello@jstoelm.com)
* Jesse Tomchak
  * Twitter: [@jtomchak](https://twitter.com/jtomchak)

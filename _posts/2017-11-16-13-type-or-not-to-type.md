---
layout: post
title: '13: To Type or Not to Type'
date:   2017-11-15
audioURL: e013-type-or-not-to-type
categories: episodes
excerpt_separator: <!--more-->
---

Coming from JavaScript, as a tool I use everyday, one that powers so much of the
web and beyond, I wanted to look at a comparison of what we get out of using
static types in a language like Elm versus JavaScript. This was spured by a
paper
[To Type or Not to Type: Quantifying Detectable Bugs in JavaScript _Software Engineering (ICSE)_ by Zheng Gao, Christian Bird, Earl T. Barr.](http://ieeexplore.ieee.org/document/7985711/)

<!--more-->

<!-- TOC -->

* [Static v Dynamic Types](#static-v-dynamic-types)
  * [Definitions First](#definitions-first)
* [Picks](#picks)
* [Resources](#resources)
* [Follow](#follow)

<!-- /TOC -->

## Static v Dynamic Types

### Definitions First

* Static type systems perform type checking at compile-time, while dynamic type
  systems distinguish types at run-time. In our case JS is dynamic and Elm <3 is
  static.
* The For Static: detects bugs before execution, increases run-time efficiency,
  improves program understanding, and enables compiler optimization
* The For Dynamic: is well-suited for prototyping, since it allows a developer
  to quickly write code that works on a handful of examples without the cost of
  adding type annotations. **THE COST OF ADDING TYPE ANNOTATIONS !??!**
* Now this is pretty much where the agreement ends. This is not an attempt to
  demonize the other, which is better argument, or sermon to get you to convert
  to my side. The reason we started the intro off with a academic published
  paper, is we want to look at this comparison head on. There is a reason we
  have taken a liking to things like Elm or PureScript. There are pains in our
  daily development lives, where the tools we have, just aren't helping, or in
  some case's actively hindering use in being as productive as we can be.
  ### To Type or Not to Type?
* This paper attempts to quantify what percent of bugs could be avoided by
  introducing types into JavaScript. This is using 2 static type systems
  TypeScript and Flow.
* The process basically looks like this.
  1. They find bugs that have been fixed in public source JS projects.
  2. They go back to the previous commit hash with the bug.
  3. They introduce both type systems, to see if adding specific type notation
     to the path of the known bug, will be caught in the compiler. And thus
     prompting the developer to fix it before it was every released.
* The goal is to:
  > "Thus, this experiment under-approximates static type systems’ positive
  > impact on software quality, "
* It's worth noting that introducing static typing to JS is not a new concept,
  in fact, it appears to be a pretty well worn path. Beside TypeScript and Flow,
  which you are likely aware of, here are a couple more:
  1. Google's
     [Closure Compiler](https://developers.google.com/closure/compiler/) the
     main goal of this project was to optimize JS code with a) reduces the size
     of your JavaScript files and makes them more efficient b) provides warnings
     for illegal JavaScript and warnings for potentially dangerous operations.
     It had 3 ways of interaction: An open source Java application that you can
     run from the command line. a simple web application or a RESTful API.
  2. Facebook's [Prepack](https://prepack.io) with the goal of getting rid of
     most intermediate computations and object allocations. Prepack operates at
     the AST level, using Babel to parse and generate JavaScript source code.
     Bug Finding — finding unconditional crashes, performance issues, ... Effect
     Analyzer, e.g. to detect possible side effects of module factory functions
     or to enforce pureness annotations Type Analysis
* So what does it say when several of largest tech companies are actively
  working to mitigate the side effects of JS with static typing and optimized
  compiling ahead of the JIT? I think the answer lies in the finds of this
  paper. Now yes, it's just one small paper, and yes it echo's our feelings
  already, well my feelings, and if you're listening, pretty good change yours
  too.
* By the numbers: On 19/08/2015, there were 3,910,969 closed bug reports in
  JavaScript projects on GitHub. We set the confidence level and confidence
  interval to be 95% and 5%, so with 400 bugs for a sample we have our pool.

So with that disclaimer....

> The core contribution of this work is to quantify the public bugs that static
> type systems detect and could have prevented: 15% for both Flow 0.30 and
> TypeScript 2.0, on average. Our experimentation artefacts are available at:
> http://ttendency.cs.ucl.ac.uk/projects/type_study/.

* **HOLY COW** that is a pretty big percentage!
* Bad actors eliminated up by static types:
  1. Type mismatches, possibly hidden by JS coercion
  2. Undefined properties
  3. method accesses
  4. Undeclared variables
* Type shim: a set of type bindings for the free identifiers. You can think of
  it as a interface T.
* **Important for thought** some of the pain, that we as JS developers run up
  against is beyond just types. Consider the following excert:
  > complicated module dependencies, the lack of annotated interfaces for some
  > modules, tangled fixes that prevented us from isolating the region of
  > interest, and the general difficulty of program comprehension.
* man, does that not sound like most JS projects you've worked on? I think this,
  this is the why I am so drawn to Elm, and have such buy-in to the Elm
  Architecture.
* And if that wasn't enough for convincing, this study was done during the
  update from TypeScript 1.8 -> 2.0 which introduced strict null checking.
  > We reviewed our corpus and found that 22 bugs, an increase of 58%, are
  > detectable under TypeScript 2.0 but not under TypeScript 1.8. This result
  > decisively and quantitatively demonstrates the value of TypeScript 2.0’s
  > strict null checking.
  ### Free as in Beer
      * nothing comes for free, so what was the cost this study found for developers to add type annotation to their JavaScript code ?
      * **Token** "The token tax rests on the intuition that each token must be selected, so this proxy measures the number of decisions a programmer must make when adding type annotations"
      * **Time** That one is pretty self explanitory. lol

|            | Token Tax Mean | Token Tax Median | Time Tax (s) Mean | Time Tax (s) Median |
| ---------- | :------------: | ---------------: | :---------------: | ------------------: |
| Flow       |      1.7       |                2 |       231.4       |                 133 |
| TypeScript |      2.4       |                2 |       306.8       |                 262 |

> handling modules was the most time-consuming aspect of annotating buggy
> versions

    * There is a whole section on related work, threats to validity, I encourage you to read this article, and see what points you agree with our disagree with.

## Picks

## Resources

* [To Type or Not to Type: Quantifying Detectable Bugs in JavaScript _Software Engineering (ICSE)_ by Zheng Gao, Christian Bird, Earl T. Barr.](http://ieeexplore.ieee.org/document/7985711/)
* [Also located Here](http://ttendency.cs.ucl.ac.uk/projects/type_study/)
* [Clousure Compiler](https://developers.google.com/closure/compiler/)
* [Prepack](https://prepack.io)
* [Flow and static type checking](https://www.lullabot.com/articles/flow-for-static-type-checking-javascript)
* [What to know before debating types](http://blogs.perl.org/users/ovid/2010/08/what-to-know-before-debating-type-systems.html)
* [JavaScript's typs system](http://2ality.com/2013/09/types.html)
* [You Don't Know JS: Types & Grammarcjdjfj](https://github.com/getify/You-Dont-Know-JS/blob/master/types%20%26%20grammar/ch4.md)

## Follow

* JavaScript to Elm
  * Twitter: [@jstoelm](https://twitter.com/jstoelm)
  * Email: [hello@jstoelm.com](mailto:hello@jstoelm.com)
* Jesse Tomchak
  * Twitter: [@jtomchak](https://twitter.com/jtomchak)

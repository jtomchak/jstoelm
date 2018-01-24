---
layout: post
title: '22: Project Make Something'
audioURL: e022-make-a-project
categories: episodes
excerpt_separator: <!--more-->
---

Taking a break from the compiler project, but only for now. I feel the need to excerise a bit more of the of the productive side. I've had this idea, for a long, long time. And have basicly been building it in my head for the last year.

<!--more-->

<!-- TOC -->

* [Project: Just do it already](#project-just-do-it-already)
* [Where it all when wrong the midterm](#where-it-all-when-wrong-the-midterm)
  * [Realign Expectations, Rethinking learning this stuff](#realign-expectations-rethinking-learning-this-stuff)
  * [Rebooting ?](#rebooting-)
* [Picks](#picks)
* [Resources](#resources)
* [Follow](#follow)

<!-- /TOC -->

## Project: Just do it already

* Run code in MirrorCode and transpile JS code to AST and compare to answer stored at AST.
* But the first part is to incorporate the editor, CodeMirrior, and capture the input. That would be the definition of success.

1. Init app, get it running
2. Split page into 50% using CSS Grid, bc fancy
3. Put CodeMirror onto page with Elm

* The Problem. I need to apply the instance of CodeMirror to the div with id "CodeEditor"
* After Importing CodeMirror, Embedding the Elm app on the root id tag
* my "CodeEditor" element is nowhere to be found.

* Ports
* Ellie as a template

4. Capture coding input and output
5. Evaluate that JS, safely?

## Where it all when wrong the midterm

* Passed or Failed
* Totally failed at this one.
* Apply the instance of CodeMirror to the element ID after Elm creates the content
* Request Animation Frame?? Nope, no idea?
* The rabbit hole, Elm and Ports
* Me, Elm, and Compile failures
*

### Realign Expectations, Rethinking learning this stuff

* Ok, so it's a larger project
* I don't have a good grasp on Elm
* Core Mission of this Podcast
* LOL, 1 point for attendance
* Pipe Operator, ??
* A bit disheartened with my progress
* A little concerned effort v progress
* Remember learning React and Redux? That was a beast
  * but it was in JS, which was still C style object programming
  * now it's functional, is it the paridigm that i'm struggling with ?

### Rebooting ?

* Elm multi-files ? This was a bit of a struggle
* Braking down the problem into small enough chunks ?
*

## Picks

* [Functional to wasm](https://github.com/appcypher/astro)

  * Astro is a
    * statically-typed language that
    * compiles to native code and WebAssembly,
    * has no GC,
    * has a syntax similar to Python,
    * provides full type inference, and
    * has first-class support for data-race-free concurrency.

* [Teach yourself CS](https://teachyourselfcs.com/)

  * If you’re a self-taught engineer or bootcamp grad, you owe it to yourself to learn computer science. Thankfully, you can give yourself a world-class CS education without investing years and a small fortune in a degree program 💸.

* [Welcome to Engineering's CS1 - SELF PACED!](https://lagunita.stanford.edu/login?next=%2Fdashboard)
  * Welcome to a public, self-paced version of Stanford's undergraduate course on Compilers. All course content is now available.

## Resources

* [Yep, more Elm Town!](https://elmtown.github.io/2016/11/07/js-in-elm-town-episode-4.html)
* [An implementation using requestAnimationFrame()](https://stackoverflow.com/questions/38952724/how-to-coordinate-rendering-with-port-interactions-elm-0-17)
* [Life of a File](https://www.youtube.com/watch?v=XpDsk374LDE)

## Follow

* JavaScript to Elm
  * Twitter: [@jstoelm](https://twitter.com/jstoelm)
  * Email: [hello@jstoelm.com](mailto:hello@jstoelm.com)
* Jesse Tomchak
  * Twitter: [@jtomchak](https://twitter.com/jtomchak)

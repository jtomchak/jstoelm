---
layout: post
title: '14: Webassembly'
audioURL: e014-webassembly
categories: episodes
excerpt_separator: <!--more-->
---

Taking a look at webassembly. A new compilation that brings more than just
JavaScript to the web,allowing memory managed apps like, C/C++ and Rust to be
compiled down to assembly and run in the browser environment. This along side
your current JavaScript code.

<!--more-->

<!-- TOC -->

* [Webassembly Overview](#webassembly-overview)
  * [What is webassembly?](#what-is-webassembly)
  * [Inter opt with JavaScript](#inter-opt-with-javascript)
  * [Linear Memory](#linear-memory)
  * [Getting some wasm in the browser](#getting-some-wasm-in-the-browser)
  * [Gotcha's](#gotchas)
* [Picks](#picks)
* [Resources](#resources)
* [Follow](#follow)

<!-- /TOC -->

## Webassembly Overview

* Disclaimer: webassembly does not currently support 'Garbage Collected'(GC)
  compilations. This means it's not yet viable for Elm. It will be, however,
  important to web development ecosystem as a whole, and thus very much worth
  our time and energy understanding it, and being ready to leverage it as soon
  as possible.

### What is webassembly?

* wasm is a new portable, size- and load-time-efficient format suitable for
  compilation to the web.
* Efficient and fast
* Open and debuggable (pretty print)
* Part of the open web platform
* webassembly must currently be loaded and compiled by JavaScript.
* General Purpose virtual architecture
* Webassembly is **NOT** always faster than JavaScript
* Pace...

### Inter opt with JavaScript

* For basic loading, there are

  * [three steps](http://webassembly.org/getting-started/js-api/):

  1. Get the .wasm bytes into a typed array or ArrayBuffer
  2. Compile the bytes into a WebAssembly.Module
  3. Instantiate the WebAssembly.Module with imports to get the callable exports

### Linear Memory

* rather than js objects that will be GC (garbage collected later on)
* used to represent the entire heap of a compiled C/C++ application.
* can be considered to be an untyped array of bytes
* it's sandboxed
* execution engine’s internal data structures, the execution stack, local
  variables, or other process memory.
* In the MVP, linear memory cannot be shared between threads of execution. The
  addition of threads :unicorn: will allow this.
* Memories can be created from JavaScript by supplying their initial size and,
  optionally, their maximum size: `var memory = new
  WebAssembly.Memory({initial:10, maximum:100});`
* Memory imports work just like function imports, only Memory objects are passed
  as values instead of JS functions. Memory imports are useful for two reasons:
  1. They allow JavaScript to fetch and create the initial contents of memory
     before or concurrent with module compilation.
  2. They allow a single Memory object to be imported by multiple instances,
     which is a critical building block for implementing **dynamic linking** in
     WebAssembly.

### Getting some wasm in the browser

* [Following Get Started with Rust, WebAssembly, and Webpack](https://github.com/jtomchak/fsociety)
* Installing Node, Rust, updating rustup

```
cd ~
 wget https://s3.amazonaws.com/mozilla-games/emscripten/releases/emsdk-portable.tar.gz
 tar -xvf emsdk-portable.tar.gz
 cd emsdk-portable
 ./emsdk update
 ./emsdk install sdk-incoming-64bit
```

```
cargo new fsociety --bin --vcs none
cd fsociety
npm init -y
```

* Yep, it took a while.
  <a href="https://imgur.com/6xIEzpz"><img src="https://i.imgur.com/6xIEzpz.png" title="source: imgur.com" /></a>

* Just a bit more....
  <a href="https://imgur.com/3jYwZ34"><img src="https://i.imgur.com/3jYwZ34.png" title="source: imgur.com" /></a>

### Gotcha's

* WebAssembly supports integers and floats, coming in 32- and 64-bit varieties.
* translate JavaScript objects to/from their C/C++ equivalents will need a far
  bit of logic
  * think distinct modules
* access to the WASM instance memory via JS ArrayBuffer. access from both sides
  of the fence
* you don't get access to system allocation commands like 'malloc' and 'free,'
* wasm is not always faster than js. there is no silver bullet

## Picks

* [A lang that compiles to wasm](https://github.com/forest-lang/core)
* [Figmas](https://blog.figma.com/webassembly-cut-figmas-load-time-by-3x-76f3f2395164)

## Resources

* [Elm w/ Webassemly](https://github.com/elm-lang/projects/blob/master/README.md#explore-webassembly)
* [Lin Clark](https://www.youtube.com/watch?v=HktWin_LPf4)
* [React, Elm, Webassemly](https://x-team.com/blog/x-periment-a-react-elm-and-webassembly-story/)
* [Preethi Kasireddy on Elm](https://medium.com/elmlightments/why-elm-is-a-future-of-frontend-interview-with-preethi-kasireddy-92d6bc6a5018)
* [Jan-Erik Rediger: WebAssembly for the rest of us](https://www.youtube.com/watch?v=SGkZbxIGDNE)
* [webpack with webassembly](https://github.com/ianjsikes/rust-wasm-loader/blob/master/index.js)
* [Get Started with Rust, WebAssembly, and Webpack](https://medium.com/@ianjsikes/get-started-with-rust-webassembly-and-webpack-58d28e219635)
* [webassembly overview](https://dzone.com/articles/webassembly-overview-so-fast-so-fun-sorta-difficul)
* [the rust post](https://users.rust-lang.org/t/compiling-to-the-web-with-rust-and-emscripten/7627)

## Follow

* JavaScript to Elm
  * Twitter: [@jstoelm](https://twitter.com/jstoelm)
  * Email: [hello@jstoelm.com](mailto:hello@jstoelm.com)
* Jesse Tomchak
  * Twitter: [@jtomchak](https://twitter.com/jtomchak)

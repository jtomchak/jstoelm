---
layout: post
title: '1: Hello World'
date:   2017-08-14
categories: episodes 
---
<!-- TOC -->

- [Why this show now?](#why-this-show-now)
- [So what is the podcast about?](#so-what-is-the-podcast-about)
- [What is ELM](#what-is-elm)

<!-- /TOC -->
## Why this show now?
* I have gotten a taste of functional programming, and really like it, but Haskell is rough. Map, reduce, filter, slice. 
* I Need that extra little push to keep at it, so by producing this show, I've added a little bit of outside pressure to keep me on track.
* [The New Rustacean](http://www.newrustacean.com/) inspiration
* Webassembly is coming
* [FrontEnd Masters](https://frontendmasters.com/courses/)
* [Lin Clark](https://hacks.mozilla.org/2017/02/a-cartoon-intro-to-webassembly/)
* [webpack mozilla](https://medium.com/webpack/webpack-awarded-125-000-from-moss-program-f63eeaaf4e15)


## So what is the podcast about?
* Learning ELM as I learn ELM, each episode will focus on a particular part or topic of the language. We'll start at the beginning together and slowly work up to more advanced topics as we go. 
* Show notes and exercises  
* Possible community interviews and resources
* I like ELM Town, and would really like more podcast about ELM, rust, web assembly, and other cutting edge shows. If you know of any please drop me a message. 

## What is ELM
* Elm compiles to JavaScript, so trying out Elm is easy.
* Current version is 0.18.0
* Quick History:
	* created by Evan Czaplicki as his 2012 Thesis. 
	* [ELM Town podcast](https://elmtown.github.io/2016/12/01/The-Founding-Story-Ep-6.html)
* Unlike hand-written JavaScript, Elm code does not produce runtime exceptions in practice. Instead, Elm uses type inference to detect problems during compilation and give friendly hints. 
* Enforced Semantic Versioning. No more surprises in PATCH releases!
	* SemVer x.y.z
		* x stands for major version, breaking changes expected
		* y stands for minor version, **NO** breaking changes
		* z stands for patch, tiny update
* Top Level Features
	* Immutability
	* Static types
	* Module System
	* Interoperability with HTML, CSS, and JS
	* Limits: does not have higher-kinder types, and thus cannot provide generic abstractions for many common operations, like map, apply, and fold. They are modules List.map, Dict.map
* Installing Elm
	* elm-repl — play with Elm expressions
	* elm-reactor — get a project going quickly
	* elm-make — compile Elm code directly
	* elm-package — download packages




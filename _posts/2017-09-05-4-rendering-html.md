---
layout: post
title: '4: Rendering HTML'
date:   2017-09-04
audioURL: 'e004-Rendering-HTML'
categories: episodes
excerpt_separator: <!--more-->
---
We will take a look at rendering our Elm to HTML using several libraries. The basic structure of getting that compiles JS from our Elm code into a div element. We will also go over a lot of the tooling used in getting all of this accomplished.  
<!--more-->
<!-- TOC -->

- [News and updates](#news-and-updates)
- [Rendering HTML](#rendering-html)
- [Picks](#picks)
- [Follow](#follow)

<!-- /TOC -->


## News and updates
* Attended a workshop by Micheal Jackson of React Training, creator of react-router v4
* Keep learning and doing

## Rendering HTML
* HTML elements that we are used to like div, img, h1 take exactly 2 arguments
  * the first is a list of attributes
  * the second is list of child nodes
  * if there is no attributes or child nodes we provide an empty list []
```js
 div [ class "content" ]
      [ h1 [] [ text "Photo Groove" ]
      , div [ id "thumbnails" ]
          [ img [ src "http://elm-in-action.com/1.jpeg" ] []
          , img [ src "http://elm-in-action.com/2.jpeg" ] []
          , img [ src "http://elm-in-action.com/3.jpeg" ] []
          
          ]
      ]
```
* Import, it's kinda like JS
  * We use the html library, may be surprised it's not part of the core library. If you look at things in our JS ecosystem, react & angular. They had moved towards a lean core lib, and extend that will specific libs. Like pulling out propTypes or when angular pulled out the router, bc everyone used ui-router. 
  * Like JS import { Component }, rather than deconstructing the import we use the key work 'exposing' (x, y, z)
  * Or to import all of them we use (..) to sort of spread over all of them
  * refered to as qualified and exposing everything is unqualified. 
  * When two use one or the other ? unqualified imports will often lead to ambiguous code. Is that map on List or Dict ? Who knows. 
* Export, still like JS
  * instead of export or export default we use module *filename* exposing (..) 
  * module is at the top of the file, not at the bottom, where I always forget to add it!
  * can expose all the functions in our module, or we could specify just a few that we want to publicly expose
  * nice that it's simple in and out, without all the possible configurations from js
* Package Manager, more similarities
  * install & publist packages. Sweet.
  * it does ask me if "Some new packages are needed. Here is the upgrade plan." That continues with the Elm ethos from the compiler that I've gotten so far. 
```sh
elm-package COMMAND
 Available commands:
  install                  Install packages to use locally
  publish                  Publish your package to the central catalog
  bump                     Bump version numbers based on API changes
  diff                     Get differences between two APIs 
```
* Built Step elm-make *filename* --output elm.js
  * this will compile our Elm into JS
  * comes with the Elm Runtime to handle the following
    * Event Listeners
    * When to update the DOM
    * app needs a main, one and only one, like in standard C programs
    * that module must be exposed, so we can call Elm.*filename*.embed
    * If you come from React, Angular, this is pretty familiar stuff, right?
  * now inject that js into the DOM using 'getElementById()'
  * at this point we can check out the index.html file and it should be rendering our images


```html
<div id="elm-area"></div>
  <script src="elm.js"></script>
  <script>
    Elm.PhotoGroove.embed(document.getElementById("elm-area"));
  </script>
```


* elm-reactor
  * Builds out our app, has a nice home directory showing used packages
  * First thing I did, was update some text and save, live reloading?
  * That's where elm-live comes in, remember JS has some very nice tooling
  * also found this [elm webpack starter](https://github.com/elm-community/elm-webpack-starter)

* the original title of this episode was Elm Architecture, but there's a lot to cover before we get to use


```js
main =
    Html.beginnerProgram
        { model = init ""
        , view = view
        , update = update
        }
```




## Picks
* [Ellie](https://ellie-app.com)
* [Elm in Action](https://www.manning.com/books/elm-in-action)
* [PhotoGrove](https://ellie-app.com/4f8cy8LhWvTa1/1)

## Follow
* JavaScript to Elm
  * Twitter: [@jstoelm](https://twitter.com/jstoelm)
  * Email: [hello@jstoelm.com](mailto:hello@jstoelm.com)
* Jesse Tomchak
  * Twitter: [@jtomchak](https://twitter.com/jtomchak)




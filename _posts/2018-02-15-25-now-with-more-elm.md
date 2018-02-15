---
layout: post
title: '25: Now With More Elm'
audioURL: e025-now-with-more-elm
categories: episodes
excerpt_separator: <!--more-->
---

Now we have Elm working inside of our react app, its time to pick a spot, feature, or pain point and get to refactoring with Elm. There are several ways to tackle this, we'll cover a few of the different ones, and what ultimately worked for us in meow notes.

<!--more-->

## Conferences

* Elm Europe is closed for CFPs
  * [elm Europe](https://2018.elmeurope.org/)
    * Elm Europe will be a two-day conference dedicated to Elm, taking place at the EFREI Engineering School in Villejuif (near Paris, France) on July, 5-6th 2018.
  * [React Rally](http://www.reactrally.com/)
    * React Rally is a two day single track conference for developers of all backgrounds using Facebook's React.js, React Native, and related tools. Speakers will cover topics such as React Native, Flux, ES6, isomorphic universal JavaScript, and so much more
    * CFP
      * The core theme for talks at React Rally is "things that are interesting to React developers." We want stories about how you built products or experiences with React, stories about overcoming challenges with (or caused by) React, and ideas for solving problems that exist in React today.
      * Sample of good proposals

## Local ServiceWorkers, because you know....SSL!

* After searching the inter webs for several possible solutions...
  1. Local signed cert
  2. Launch Chrome with flags `/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --user-data-dir=/tmp/foo --ignore-certificate-errors --unsafely-treat-insecure-origin-as-secure=http://localhost:3000`
  3. And plenty others
* "If you need to test your offline-first service worker locally, build the application (using npm run build) and run a simple http server from your build directory. After running the build script, create-react-app will give instructions for one way to test your production build locally and the deployment instructions have instructions for using other methods. Be sure to always use an incognito window to avoid complications with your browser cache."[Offline First](https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/template/README.md#offline-first-considerations)
* Or, after reading a bit of the docs from Create React App, [CRA service worker included by default](https://github.com/facebook/create-react-app/issues/2398) the answer was, it is not enabled by default for development. D'OH!
* [Making a progressive web app](https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/template/README.md#making-a-progressive-web-app)
* Run time caching: If you would like to use a runtime caching strategy for those requests, you can eject and then configure the runtimeCaching option in the SWPrecacheWebpackPlugin section of webpack.config.prod.js.

## Adding More Elm

* So after watching Life of a file, it dawned on me, that as soon as I see file of 200 lines or so, I **FREAK** out. And it was really nice to have Evan explain the sort of core reasoning for that.
  1. "As LOC increases, the probability of _sneaky mutation_ approaches one." Therefore: **PREFER SHORTER FILES**
  2. "Refactoring is _very_ risky. A full rewrite can be cheaper." Therefore: **GET ARCHITECTURE RIGHT FROM THE START**
* Richard's 2016 talk

  * React in 2013 -> Lots of React
  * Elm in React -> slowly grew piece by piece
  * Start with something small and get it to production!

* Start with the boiler plate Create Elm App. And the idea, is that, there isn't anything in the Home component that I couldn't do in Elm. With the exception of the api call, bc awsSigV4Client that is signing all the requests from our API. So that users can temporarily upload to our s3 bucket by verification of the identity of the requester.

```Elm
  renderElm() {
    return <Elm src={ElmHome} />;
  }
```

* Start with modeling your data.
* OK
* I've got an article that has content, createAt, noteId.
* And model will be a list of type Note. So we make an type alias to refer to our note object that we get back from the API

```
type alias Note =
    { content : String
    , createdAt : Date
    , noteId : Int
    }


type alias Model =
    List Note


init : ( Model, Cmd Msg )
init =
    ( [], Cmd.none )
```

* Calling update on init
  * wanting to make a call for the list of notes when elm app is started
  * Commands!!!!

```
  //init setup for ports
  setupPorts(ports) {
    ports.fetchNotes.subscribe(() => {
      invokeApig({ path: "/notes", queryParams: { limit: 5 } })
        .then(results => ports.notesLoaded.send(results))
        .catch(e => console.log(e));
    });
  }

  renderElm() {
    return <Elm src={ElmHome} ports={this.setupPorts} />;
  }
```

## Picks

* [Elm and the outer world](http://codeloveandboards.com/blog/2017/05/15/elm-and-the-outer-world/)
* [Kent C. Dodds New Context API](https://medium.com/dailyjs/reacts-%EF%B8%8F-new-context-api-70c9fe01596b)

## Resources

* [ReactiveConf 2016 - Richard Feldman: Elm and React in production](https://www.youtube.com/watch?v=3FNKaGm3gk0)
* [Life as a file](https://www.youtube.com/watch?v=XpDsk374LDE&list=PL-cYi7I913S8cGyZWdN6YVZ028iS9BfpM&index=1)
* [State of Elm](http://www.brianthicks.com/post/2018/02/01/state-of-elm-2018/)
* [Elm Wrapper](https://blog.boon.gl/2017/11/28/react-elm-wrapper.html)
* [Node Elm Compiler](https://github.com/rtfeldman/node-elm-compiler)
* [Service Worker](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API/Using_Service_Workers)
* [Elm Infinite List View](http://package.elm-lang.org/packages/FabienHenon/elm-infinite-list-view/latest)

## Follow

* JavaScript to Elm
  * Twitter: [@jstoelm](https://twitter.com/jstoelm)
  * Email: [hello@jstoelm.com](mailto:hello@jstoelm.com)
* Jesse Tomchak
  * Twitter: [@jtomchak](https://twitter.com/jtomchak)

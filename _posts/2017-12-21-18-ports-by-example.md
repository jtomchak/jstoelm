---
layout: post
title: '18: Ports by example'
audioURL: e018-ports-by-example
categories: episodes
excerpt_separator: <!--more-->
---

It's time to dive right in with several uses of Ports in Elm, what better way than by example! Ports are Elms way of interacting with the outside world, currently with JavaScript, but the sky is the limit.

<!--more-->

<!-- TOC -->

* [More Ports](#more-ports)
  * [Ports, the Actor Model.](#ports-the-actor-model)
  * [Ports, the example](#ports-the-example)
* [Picks](#picks)
* [Resources](#resources)
* [Follow](#follow)

<!-- /TOC -->

## More Ports

### Ports, the Actor Model.

* Ports is not server/http, but rather the Actor Model
* Talking with messages. Messages In, Messages Out.
* Erlang/Elixir, webworkers, Scala
* Let's just have 1 port. Singular. Let's **NOT** wrap the JS API.
* Murphy's "Outside Info" of a single pair of ports
* The Actor Model
  * The actor model is a conceptual model to deal with concurrent computation.
  * The actor is just a _thing_ that receives a message and then does something based on that message.
  * The actor can have private state, that cannot be changed directly by another actor.
  * Actors work in a system of actors. If you only have a single actor, then there's no one to send messages to or worse, no one to get messages to. In our case, Elm is an actor, and JS is an actor, sending messages back and forth to each other.
  * Messages sent to an actor or processed sequentially.
  * Needs 3 things of computation:
    1. getting something done
    2. store things
    3. be able to communicate
  * Actors can only do one of the following:
    1. Create more actors;
    2. Send messages to other actors; (Factorial, many messages at the same time, relates to concurrency)
    3. Designates what to do with the next message, to itself. (This relates to the state of the actor)
  * Mailboxes, concurrency, and queues
  * EO Wilson, "One ant, is no ant"
  * Actors will need an address, in order send messages to.
  * "the actor has to agree to chop off it's own head. "

### Ports, the example

* Before Diving into the implementation of the Ports Example, I wanted describe what it was like to get stuff from Elm and be able to simply `console.log` it out into my familiar dev tools. There was a real, oh shit moment, where it started working.
* Incoming Cmd hand to the runtime in Elm.
* Outgoing Subscription, message tagger.
* Change the module declaration to `port module`
* We've got `port check : String -> Cmd msg`
  * function that takes a string and returns a Cmd msg. This is used by our update function,
  * so, with the onClick we take the string in the current model word, which has been captured with the onChange, and we and in the update function we call `check` and the model.word creating a Cmd for the Elm runtime.
  * as a port it will handle making that available to JS from `app.ports.check.subscribe` which takes a callback to invoke whenever Elm passes a message. This is the sort of gritty part of the actor model setup.
  * So we've wired up the outgoing message from Elm,
* Now we've got `port suggestions : (List String -> msg) -> Sub msg`
  * This is going to be our List of Strings from JS, or is JS speak, Array
  * so you can convert that list of strings to your Msg type immediately.
  * This makes it easy to deal with in your update function, but it is just for convenience.

The JS Side

```js
var app = Main.fullscreen();
/*
Methods we delcared as 'port' in Elm will be available on app.ports that
will get invoked/called when we send a cmd message out via Elm.
*/
app.ports.check.subscribe(function(word) {
  var suggestions = spellCheck(word); //--> invoke JS function, return array of strings
  app.ports.suggestions.send(suggestions); //--> sending to the Elm sub
});

function spellCheck(word) {
  console.log(word); // Words from Elm!!!!!
  return [];
}
```

The Elm Side

```Elm
port check : String -> Cmd msg


---- Subscription ---
-- port for listening for suggestions from JavaScript


port suggestions : (List String -> msg) -> Sub msg


subscriptions : Model -> Sub Msg
subscriptions model =
    suggestions Suggest

...

type Msg
    = Change String
    | Check
    | Suggest (List String)

...

Suggest newSuggestion ->
            ( Model model.word newSuggestion, Cmd.none )
```

## Picks

* [State of Elm](https://discourse.elm-lang.org/t/state-of-elm-2018-questions-draft-1/161/11)

## Resources

* [Elm Docs Docs](https://guide.elm-lang.org/interop/javascript.html)
* [Murphy Randle — The Importance of Ports](https://www.youtube.com/watch?v=P3pL85n9_5s)
* [Actor Model logic programming](https://en.wikipedia.org/wiki/Actor_model#Relationship_to_logic_programming)
* [The Actor Model](http://www.brianstorti.com/the-actor-model/)
* [Actors from the guy who invented them, Hewitt, Meijer and Szyperski](https://www.youtube.com/watch?time_continue=11&v=7erJ1DV_Tlo)
* [Elm Port Example ](https://github.com/jtomchak/elm-port-example)

## Follow

* JavaScript to Elm
  * Twitter: [@jstoelm](https://twitter.com/jstoelm)
  * Email: [hello@jstoelm.com](mailto:hello@jstoelm.com)
* Jesse Tomchak
  * Twitter: [@jtomchak](https://twitter.com/jtomchak)

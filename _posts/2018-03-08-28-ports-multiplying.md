---
layout: post
title: '28: Ports Multiplying'
audioURL: 'e028-ports-a-multiplying'
categories: episodes
excerpt_separator: <!--more-->
---

We are back to meow notes, adding our onClick event from Elm back to React to route either to a new note, or an existing note by note.id. This is going to require us to poke another hole in our ports, but remember Murphy's warning, not to treat this like http methods, so lets keep that in mind as we move forward.

<!--more-->

## Extra Type Alias

* I had made a `type alias Notes = List Note`
* Mostly because the compiler was complaining at one point, and I wasn't able to see to distill from it that all I needed was some parentheses around `List Note` to disambiguate it.

## Tackling the onClick event

`List.map (\n -> Listgroup.li [ onClick (routeTo "/notes/" ++ n.noteId) ] [ text n.content ]) notes`

* that was my first thought, but..

```
The 1st argument to function `li` is causing a mismatch. - Function `li` is expecting the 1st argument to be:

    List (Listgroup.ItemOption msg)

But it is:

    List (Html.Attribute a)
```

grrrrrr

```
List (Html.Attribute msg)

But the right side is:

    Html.Attribute Msg
```

* What I finally got

```
 Listgroup.button
    [ Listgroup.attrs <| [ onClick (SetRoute ("/notes/" ++ n.noteId)) ]
```

* Ok got that sorted, sending an Html msg, and in the update function calling the ports function routeTo with the built string.
* What's the title look like? Used to be..

```
header={note.content.trim().split("\n")[0]}
```

* Now it looks like

```
--good
Maybe.withDefault "Note Title" (List.head (String.lines content))

--better
Maybe.withDefault "Note Title" (n.content <| String.lines <| List.head) --backwords

--best
Maybe.withDefault "Note Title" (n.content |> String.lines |> List.head)
```

* saw the nested, and remembered that's why the Pizza Operator, er, Pipe Operator
* I also did it backwards the first time. lol

## Too Many Ports, our ship is sinking

* too many ports sink ships, but what I want is working code first, I'm not trying to refactor this in my head, **NO WAY**

```
//init setup for ports
  setupPorts = ports => {
    ports.fetchNotes.subscribe(path => {
      invokeApig({ path: path, queryParams: { limit: 5 } })
        .then(results => ports.notesLoaded.send(results))
        .catch(e => console.log(e));
    });
    ports.routeTo.subscribe(url => {
      this.props.history.push(url);
    });
  };
```

* So let's try to consolidate some stuff. We don't need two elm files rendering for the Home component, let's pass the isAuthenticated prop into Elm and have that do it for us
  * So how do we do multiple subscriptions?
  * Batch of course!
  * So we send in the props value,
  * and this works, `ports.isAuthenticated.send(this.props.isAuthenticated);`
  * but I'm not super happy with it....
  * React lifecycle methods to the rescue,
    * instead of calling isAuthenticated.send we assign it to updateAuth and now we can call it on mount and when component received new props, **NOT** just when we instantiate our Elm Home Component.
    * Must better.

## Picks

* [On Yeah Atom with X-ray!](https://github.com/atom/xray)
* [Too many coding tools put up big barriers to your creativity by requiring tons of setup, having lots of confusing and complicated features, or by letting jerks run rampant in the community. With Glitch, we're rolling out the red carpet to welcome creators just like you.](https://glitch.com/about/)

## Resources

* [Murphy's The Importance of Ports](https://www.youtube.com/watch?v=P3pL85n9_5s)
* [Using Elm in React](https://codeburst.io/using-elm-in-react-from-the-ground-up-e3866bb0369d)
* [Elm Functions – Syntax, Piping and Currying](https://dennisreimann.de/articles/elm-functions.html)
* [From React To Elm](http://sebastianporto.com/blog/posts/2017/from-react-to-elm/)
* [Interacting with the DOM Element using Elm](https://vincent.jousse.org/en/tech/interacting-with-dom-element-using-elm-audio-video/)
* [Elm Elixir-Phoenix Functional Full Stack](https://teamgaslight.com/blog/elm-elixir-and-phoenix-reflecting-on-a-functional-full-stack-project)

## Follow

* JavaScript to Elm
  * Twitter: [@jstoelm](https://twitter.com/jstoelm)
  * Email: [hello@jstoelm.com](mailto:hello@jstoelm.com)
* Jesse Tomchak
  * Twitter: [@jtomchak](https://twitter.com/jtomchak)

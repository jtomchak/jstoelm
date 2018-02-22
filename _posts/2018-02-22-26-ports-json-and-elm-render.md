---
layout: post
title: '26: Ports, JSON, and Elm render'
audioURL: 'e026-ports-json-elm-render'
categories: episodes
excerpt_separator: <!--more-->
---

26: Ports JSON And Elm render

The last 10%. We left off our app with being able to pass the return JSON from our fetch promise to get a list of notes through ports to Elm, and debug logging that out. At this point I thought, "success!". You might even recall, I glossed over rendering it to a list, totally spaced the click event needed to make the list actually do something. So today we take the work of getting the data to work, to the work needed to get it back to working functionality using Elm.

<!--more-->

## Data from Ports

* After being about to do a debug log in the update function that was just a dump of the results from the port function
  `port notesLoaded : (Value -> msg) -> Sub msg`
  This was cause for celebration.
* Now getting that JSON data into a list.
* Ok, what is the return payload in ?? Little messed up looking at most examples, bc they were dealing with maybe JSON
* Result type signature

```
type Result error value
    = Ok value
    | Err error
A Result is either Ok meaning the computation succeeded, or it is an Err meaning that there was some failure.
```

```
type Msg
    = NotesLoaded (Result String Notes)

[...]
port notesLoaded : (Value -> msg) -> Sub msg  
```

![inline](https://i.imgur.com/YpLOhT9.png)

## Decoding List of Objects.

* Everyone's favorite. This is the part I enjoy in programing the sort of gritty, data transformation.
* incoming JSON is run through the noteListDecoder, which runs decode on a list of Notes. Using map3 we Try three decoders and then combine the result.
* `>>` In other words, (<<) takes 2 functions of types b -> c and a -> b respectively, and returns a function of type a -> c. It composes 2 functions into one.

```
subscriptions : Model -> Sub Msg
subscriptions _ =
    notesLoaded ((decodeValue noteListDecoder >> NotesLoaded))


noteDecoder : Decoder Note
noteDecoder =
    map3 Note
        (field "content" string)
        (field "createdAt" int)
        (field "noteId" string)


noteListDecoder : Decoder (List Note)
noteListDecoder =
    list noteDecoder
```

* Once we've got our JSON in, decoded, and called update function `NotesLoaded` we're all set right? **GOTTA STOP SAYING THAT**
* `NotesLoaded` takes a JSON decoded which we're passing (Result String Notes)
* Then we just have to deal with the Ok or Err from the Result. If it's ok we can set the nicely decoded result to our model notes, otherwise, we aren't doing anything in our Err, but will populate the error String into a model error string and conditionally render the DOM. We'll get there.

```
        NotesLoaded (Ok notes) ->
            ( { model | notes = notes }, Cmd.none )

        NotesLoaded (Err fail) ->
            ( model, Cmd.none )
```

## Render List

* now the update function is good to go.
* One of the nice parts of this project is I don't have to mentally think about layout, style, or functionality, the removes a nice level of decision making and let's me just focus on the code. And that's rad!
* add bootstrap-elm for Listgroup ul and li.
* call `renderNotes model.notes` in the view function
* `renderNotes` map's over each record in the list, transforms it into Html Msg that Listgroup.ul will take.

```
renderNotes : Notes -> Html Msg
renderNotes notes =
    let
        noteItems =
            List.map (\n -> Listgroup.li [] [ text n.content ]) notes
    in
        Listgroup.ul noteItems
```

## Todo's

* onClick
* trim note to first line trim
* show created date, hopefully we'll have some nice Elm Date method to do it for us.... I hope.
* port to handle the onClick, because it's a router push to `/notes/${note.noteId}` so we'll figure that out too. Weeeeeeeee!!!!
  ## Picks
* [Elm Survey](http://www.brianthicks.com/post/2018/02/01/state-of-elm-2018/)
* [Gatsby Static site generator](https://www.gatsbyjs.org/)
* [jamstack \’jam-stak’\ ](https://jamstack.org/examples/)
* [Using Elm to Prototype and Build Web Applications – David Calavera](https://www.youtube.com/watch?v=Lmg9v2U6-y4)

## Resources

* [Fira Code](https://github.com/tonsky/FiraCode)
* [Building Web Apps with Elm | Elm Tutorial by The Pragmatic Studio](https://pragmaticstudio.com/elm)
* [Elm changed my mind about unpopular languages – Real Kinetic Blog](https://blog.realkinetic.com/elm-changed-my-mind-about-unpopular-languages-190a23f4a834)
* [Lambda Cat](http://www.lambdacat.com/road-to-elm-let-and-in/)

## Follow

* JavaScript to Elm
  * Twitter: [@jstoelm](https://twitter.com/jstoelm)
  * Email: [hello@jstoelm.com](mailto:hello@jstoelm.com)
* Jesse Tomchak
  * Twitter: [@jtomchak](https://twitter.com/jtomchak)

---
layout: post
title: '11: Fetch & Decoding JSON Part-1'
date:   2017-11-01
audioURL:e011-fetch-decode-part-1
categories: episodes
excerpt_separator: <!--more-->
---
One of the fundemental tasks of any web app, is to get, display, capture, save, manipulate, or otherwise man handle data from an http request. We are gonna dive into what that means for our model, our update function, and our sanity. 
<!--more-->
<!-- TOC -->

- [Fetching and Decoding JSON](#fetching-and-decoding-json)
  - [So with that let's talk about why it's more effort than that? (Evan's post)](#so-with-that-lets-talk-about-why-its-more-effort-than-that-evans-post)
  - [Model Change considerations...](#model-change-considerations)
  - [No Side Effects](#no-side-effects)
  - [The actual thing, http.send](#the-actual-thing-httpsend)
- [Picks](#picks)
- [Resources](#resources)
- [Follow](#follow)

<!-- /TOC -->
## Fetching and Decoding JSON
* More that just fetch and use!
```js
fetch('dataURI')
.then(res => res.json())
.then(payload => {
  alreadyJSObject(payload.coolstuff);
})
.catch(err => neverFails(err))
```

### So with that let's talk about why it's more effort than that? (Evan's post)
  * > If I change a type, I want the compiler to complain
  * I can pretty much agree with that statement. From someone who had to check ```if(obj == (NSString *)[NSNull null] || obj.length==0)``` 
  in objc a grip ton on incoming JSON data, I can appricate the compilers help on this one. 
  * I also had to deal with SOAP endpoints without the cover of .NET to help me, so I don't feel that JSON is bad, it's better than what we had. But that doesn't me it's good, just that it's better than what we had before. So we're less worse off??
  * I would like some sort of contract between clients and servers. If that's in a .format type file, great! If there's something else, I'm willing to try it. 
  * I can't think of a good reason a language _should_ inclue in the stlib a parse solution for a particular format. That seems short sighted to me. These formats come and go with every cycle. 
* Commands in Elm
  * Addition of commands do not change the structure of our appliction, as cmd are feed back to our update function to handle. 
  
### Model Change considerations...  
  * Yeah, didn't really think that's where'd you start, but it makes sense. This is a again really data model, type driven development. You've got to stop and consider what these actions do, like fetching data, to your data model. Feels a little bit like creating a data migration when working with a SQL ORM? Where in order to use a new table or column, you've got to create it first, run the migration, and then it's totally fine. Sorta maybe the same feeling? or process might be a better word.
  * Our initial value when fetching data is gonna be zilch. **Maybe** to the rescue. Changing our type alias for Model to have a sprinkle of Maybe's let us set those values to equal to Nothing. That's Nothing with a capital 'N'

So Angry When You Change the Model!!
![alt text](https://i.imgur.com/v8B2fxn.png "So Anger")
That's better
![alt text](https://i.imgur.com/MeBEqz1.png "So much better")

  * Propagate the maybe. Sort of remember this from Swift. Rather than unwrapping it, or handling the maybe and pulling out the Just or Nothing, we can pass it along, and have it 'handled' down the line. 
  * Once we've handled our type mismatches, and the compiler (usually i'd say complaining, but in this case it definitely helping) is satisfied. We can turn our attention to the business logic.

### No Side Effects
  * http, even a GET request, is by definition a side effect. As it can not be guaranteed to return the same result by calling the request again. Not to metional all the effects it can have on the other state. That list goes on and on. 
  * So what' a developer to do? most applications revolve around the concept of getting and sending data? Or more simply, creating side effects. And that we leave up to the Elm runtime. We simply describe what we want, using cmd's, and through the update function, we pass them into the runtime and let that handle it. 
  * In the case of http requests, we are going to create a cmd using http.send, which when called, will return us the cmd needed to pass to the Elm runtime, at which point IT will do make the actual http request using the data in the cmd that we send it. sweet, right?

### The actual thing, http.send
  * So when call http.send. Unlike JS, that doesn't make the http request. Nope. It's a cmd, that the Elm run time will do for use. Meaning we need to handle the return results in our update function. The return is a Result, which is displayed below. Showing either error or ok. 

```js
type Result errValue okValue
    = Err errValue
    | Ok okValue”
```
 * Expected this part to be longer..... but we've sorta handled everything. By the time that data comes back. We've already build all the possible results **AND** their respective paths. If we have data, it needs to be this type, put it here, otherwise handle this error. 
 * I guess there is no step 3.
 * Handling the Errors with a view or error function. Not sure how I feel about that. I mean, I guess it failed,right? 
 * I also saw this little tid bit. ```import Task exposing (Task, andThen)``` so now I need to do a little research on what Task is. As I saw it twice today alone!

<iframe src="https://ellie-app.com/embed/fRJh3Wh5Qa1/0" style="width:100%; height:400px; border:0; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

*


## Picks
* [Manton](https://manton.org/)
* [Micro Blog](https://micro.blog)
* [Due task management]()
* [Teaching Haskell, a new hope](http://argumatronic.com/posts/2017-10-28-a-new-hope.html)

## Resources
* [Elm in Action](https://www.manning.com/books/elm-in-action)
* [Murphy Fun Hipster stuff](https://egghead.io/lessons/elm-make-an-http-request-in-elm)
* [Why do I have to write JSON decoders in Elm? A vision for data interchange in Elm](https://gist.github.com/evancz/1c5f2cf34939336ecb79b97bb89d9da6)
* [Serde is a framework for serializing and deserializing Rust data structures efficiently and generically.](https://docs.serde.rs/serde/)

## Follow
* JavaScript to Elm
  * Twitter: [@jstoelm](https://twitter.com/jstoelm)
  * Email: [hello@jstoelm.com](mailto:hello@jstoelm.com)
* Jesse Tomchak
  * Twitter: [@jtomchak](https://twitter.com/jtomchak)



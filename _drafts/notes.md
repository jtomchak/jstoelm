Got behind on podcasts and am late on this, but you probably already have an explanation. However, I'll toss this out.

When you hear the term 'morphism' in the realm of programming, think 'function'. Functions are the word we usually use when we talk about morphisms.

A polymorphism is a function which works on many types. Note that a union type is just one type which can combine values of other types.

Parametric polymorphism is like `List a`. We can form a list of any type we want, but `List Bool` is not the same type as `List Int`. We can make morphisms (functions) which can come from any List to some value (e.g. length).

Ad-hoc polymorphism says that there is a function defined somewhere which allows us to do a thing. This is what typeclasses are doing. To make a type a member of a typeclass, you have to define a set of functions. To be `Foldable`, you have to have the functions `foldMap` and `foldr` (and can define others for performance if you would like). If you declare that a type variable must have `Foldable` defined, then you can use those functions on it and Haskell will figure out which one to call when required.

---
layout: post
title: A Practical Introduction to Functional Programming - Now with Swift!
date: 2015-08-10
categories:
- blog
tags:
- tech
- ios
- swift
status: publish
type: post
published: true
---

# Introduction

Swift introduces a new paradigm to the world of iOS programming: the functional paradigm. Many of us iOS developers have become so used to Objective-C - and perhaps other object-oriented languages before - that writing and thinking functionally feels a bit brain-addling. 

Where to begin? Myself, I find examples the easiest to digest - and  I thankfully needn't have looked farther than this wonderful post by [Mary Rose Cook](http://maryrosecook.com/) to find some good ones: [
A practical introduction to functional programming](http://maryrosecook.com/blog/post/a-practical-introduction-to-functional-programming). Not only that, but she includes examples of code that you and I might write _plus_ the functional complement.

What my post does is revisit Cook's examples, except in Swift. So before you make your way through this, do read her post - not only did it originate these examples, but it has very clear explanations of functional programming concepts for beginners that I won't be reiterating in totality.

<blockquote>When people talk about functional programming, they mention a dizzying number of “functional” characteristics...Ignore all that. Functional code is characterised by one thing: the absence of side effects. It doesn’t rely on data outside the current function, and it doesn’t change data that exists outside the current function. Every other “functional” thing can be derived from this property. Use it as a guide rope as you learn.</blockquote> -- *Mary Rose Cook* on learning about functional programming

<br />

## Example #1 - Increment

<script src="https://gist.github.com/hkellaway/303af36465e98d002f9e.js"></script>

Notice the difference between these two functions written to increment variable *a* - while *incrementUnfunctional* modifies a global value, *incrementFunctional* is a general use function that reliably takes in a number and returns what its value would be when incremented. This is the "abscence of side effects" Cook mentions: *incrementFunctional* does not affect state outside of itself.

# Cook's Lesson #1: Don't Iterate over lists. Use map and reduce.

Any dive into functional programming will quickly be met with mention of *map*, *reduce*, and *filter*. These are popular among the powerful functions used to work with collections. We're going to take a look at *map* and *reduce*.

## Example #2 - Map 1

<blockquote>Map takes a function and a collection of items. It makes a new, empty collection, runs the function on each item in the original collection and inserts each return value into the new collection. It returns the new collection.</blockquote>

<script src="https://gist.github.com/hkellaway/a240853a870a743e9c76.js"></script>

As this example illustrates, *map* simply returns a new collection - in this case an *array* - with the result of applying an anonymous function to each element of the original collection. The original collection remains unmodified.

## Example #3 - Map 2

<script src="https://gist.github.com/hkellaway/432a64be4ed2a932930a.js"></script>

Here we see how we might acheive getting an array of random programming languages in a way that's probably familiar - as well as the functional complement.

## Example #4 - Reduce 1

<blockquote>Reduce takes a function and a collection of items. It returns a value that is created by combining the items.</blockquote>

<script src="https://gist.github.com/hkellaway/69e4f87f8c703d45311f.js"></script>

*Reduce* is a bit harder to grasp than *map*. It starts accumulating a value starting with *initial* - *0* in our example - and returns the result of calling *combine* on each member of the collection and the running combination.

The above example uses shorthand argument names - *$0* and *$1* - which some find confusing. Here's another way to express the same:

<script src="https://gist.github.com/hkellaway/afea64a148f7aa8cf7fd.js"></script>

We start out with *0*, then combine the *runningSum* with the *currentValue* in our collection of *numbers* using addition - to eventually arrive at *sum*.

## Example #5 - Reduce 2

*Reduce* does not only have to be used on collections of numbers - let's look at an example with a collection of strings. This is a function that tells us how many phrases include the word "hello":

<script src="https://gist.github.com/hkellaway/56f700898bc5891fdb4b.js"></script>


### A Swift Note About Map, Reduce & Friends

For Swift 1.2, functions like *map* and *reduce* were global functions in Swift's library  - so you'd use syntax as such: *map([0, 1, 2, 3, 4], { x in x * x })*. Swift 2 provides us with the more intuitive syntax that you see in these examples, of calling *map* directly on a collection. The same concepts apply to each!


# Cook's Lesson #2 - Write declaratively, not imperatively.

<blockquote>A functional version [of imperative code] would be declarative. It would describe what to do, rather than how to do it...A program can be made more declarative by bundling pieces of the code into functions.</blockquote>

Objective-C programmers are used to writing imperatively - this is a programming paradigm where sequences of statements are used to modify state. Functional programming is a form of declarative programming - which is characterized by using functions to describe what to do.

## Example #6 - Imperative 1

Let's look at Cook's example of a small program that will simulate a race between three cars:

<script src="https://gist.github.com/hkellaway/66b33e33e0d97ca8fe4c.js"></script>

## Example #7 - Imperative 2

A practiced Objective-C programmer might look at this and realize it'd be better expressed by breaking it into smaller pieces:

<script src="https://gist.github.com/hkellaway/8f080902ef988c51078c.js"></script>

This is cleaner code, but it is still not functional - each function does not do what Cook teaches us to expect with a functional impelemtnation: "[functions don't] rely on data outside the current function, and [don't] change data that exists outside the current function".

## Example #8 - Declarative

Here's the functional version:

<script src="https://gist.github.com/hkellaway/4d343c0d6a5bec217139.js"></script>

Whoa, that's a lot. I encourage you to think carefully about each function you see in this example and recognize that it does just what we want: it doesn't rely on or modify data outside of itself.

Another neat thing about this example is that using custom types - via the *typealias* keyword - just came naturally when implementing it. One aspect of functional programming that I personally love is that it forces us to think carefully about the types that we use in our program and how to manipulate them with functions.


# Cook's Lesson #3 - Use pipelines.

<blockquote>In the previous section, some imperative loops were rewritten as recursions that called out to auxiliary functions. In this section, a different type of imperative loop will be rewritten using a technique called a pipeline.</blockquote>

## Example #9 - Not using pipelines

Let's start by looking at a typical example of applying transformations to a set of data. Here, we bave an array of *bands* who each have a *name* and *country*. We want to apply 2 transformations to the collection of bands: 1. Set the country to Canada 2. Capitalize the band name. Here's how we might take a first go at this:

<script src="https://gist.github.com/hkellaway/894b7f1883b27939ada3.js"></script>

Use of the *inout* keyword is already a clue that we're not getting functional. 

Where we want to go with this is a having a much more expressive and flexible way of representing the transforms we want, without baking it into our *formatBands* function:

*print(formattedBands(bands, [setCanadaAsCountry, capitalizeName]))*

How do we get there?

## Example #10 - Functional pipelines

<script src="https://gist.github.com/hkellaway/71530223d3e462730996.js"></script>

Take a careful look at the *canada* and *capitalize* functions; these simply take in a *BandProperty* (string) and return a *BandProperty* (string). 

Take a look at *setCountryAsCanada*, and *capitalizeName* functions; these simply *call* a *BandPropertyTransform* function (such as *canada* or *capitalize*) on a property of a *Band* (dictionary) denoted by a key (*"country"* and *"name"* respectively)).

All of these functions make sense independently of how we use them. Our *formattedBands* function ends up simply calling an array of *BandTransform* functions on the *bands* passed in. We could write any number of transforms and pass them to *formattedBands* without having to modify it - that's powerful stuff!


## Extra credit - Function Composition

If you've stuck with me so far - let's take a look at another way to combine the transforms that was not in Cook's original post. 

This implementation is inspired by one of my favorite books on Swift: [Functional Programming in Swift](http://www.objc.io/books/fpinswift/) by Chris Eidhof, Florian Kugler, and Wouter Swierstra of [objc.io](http://www.objc.io/). There's a section in this book that talks about composing functions - we can apply this concept to the task at hand:

### Example #11 - Function composition

<script src="https://gist.github.com/hkellaway/b219270c2841a8e9babc.js"></script>

This is ultimately very similar - but uses the concept of function composition to apply our transforms instead of the *map* and *reduce* calls used in Cook's solution.


# Conclusion

These lessons are again best summed up by Cook:

<blockquote>Functional code co-exists very well with code written in other styles...Turn iterations of lists into maps and reduces. Think of the race. Break code into functions. Make those functions functional. Turn a loop that repeats a process into a recursion. Think of the bands. Turn a sequence of operations into a pipeline.</blockquote>

Swift is not a purely functional language - your functional code can co-exist very well with code written in non-functional style. Challenge yourself using the lessons here to translate some of your code to a functional style and evaluate whether it's beneficial.

All of the code in these examples are available as Gists as well as on Github: [https://github.com/hkellaway/swift-functional-intro](https://github.com/hkellaway/swift-functional-intro)

Happy programming!


---
layout: post
title: Introducing Gloss - A Shiny, New JSON Parsing Library in Swift
date: 2015-08-16
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

# Introducing Gloss

![Gloss](http://hkellaway.github.io/Gloss/images/gloss_logo_tagline.png)

<br />

[Gloss](https://github.com/hkellaway/Gloss) is a shiny, new JSON parsing library written in Swift!

Gloss enables simple transformation from JSON to objects - and from objects back to JSON. It supports nested models with no extra work, as well as custom transformations. 

Let's take a quick look using the following JSON representing a Github repository.

Repo JSON:

<script src="https://gist.github.com/gloss-swift/bd555a41eba0208c8529.js"></script>

<br />

Repo Model:

<script src="https://gist.github.com/gloss-swift/7d2eee0c1f91e1a74a45.js"></script>

<br />

Creating a Repo object:

<script src="https://gist.github.com/gloss-swift/502c84e16e7a089391c4.js"></script>

<br />

Translating a Repo object back to JSON:

<script src="https://gist.github.com/gloss-swift/e0ee7a1e9d7b16bc8e2c.js"></script>

Nice!

There's a whole lot more info in the [Gloss docs](https://github.com/hkellaway/Gloss/blob/master/README.md) - including a closer look at these models, how to create custom transformations, and more.


# Why Though?

Gloss joins several Swift JSON parsing libraries - why create a new one?

After [reviewing](/blog/2015/07/05/swift-json-parsing-by-example/) several other libraries, there were aspects of each that I liked and those I did not. I tried to address the following concerns with Gloss:

* **Immutable models** - I don't want to require each property to be a _var_

* **Serialization** - I want a library that offers not just translation _from_ JSON, but _back to_ JSON

* **Ease of model creation** - I want my models to be fairly compact, with a roughly 1-line-to-property ratio for deserialization and serialization respectively

* **Ease of comprehension** - I want a library that's not too difficult to understand if I need to dive into the source code

Additionally, I'd say there's not a clear call on which JSON library is the go-to - so there's still room to introduce new takes on the issue at hand. 

I also just love the act of contributing to collective knowledge and utility by open sourcing libraries like this, especially one with such potential for impact.

# Try It!

Gloss is available via Cocoapods - just add the following to your Podfile:

<script src="https://gist.github.com/gloss-swift/432d9c3581661dc04fd6.js"></script>

As you're vetting libraries to use for JSON parsing in your next Swift project or if you're looking to switch libraries - give [Gloss](https://github.com/hkellaway/Gloss) a try! 

If you have concerns or improvements, I encourage you to contribute to the project - the quickest way being submitting an [Issue](https://github.com/hkellaway/Gloss/issues/new) or a [Pull Request](https://github.com/hkellaway/Gloss/pulls).

Happy coding!

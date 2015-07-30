---
layout: post
title: Swift JSON Parsing by Example - ft. Argo, JSONJoy, ObjectMapper, and SwiftyJSON
date: 2015-07-05 
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

Since Swift landed on the scene roughly a year ago, a number of libraries have cropped up that help us developers with a central task: parsing JSON into application models. In this post, I'm going to explore how a few of the frontrunners are actually used. 

This post is meant to be singly practical and will not delve into opinion or theory as to why one library would be used instead of another. For another practical look at JSON parsers plus some valuable musings, I highly recommend reading [Swift JSON Shoot-Out](http://blog.scottlogic.com/2015/03/09/json-in-swift.html) by [Sam Davies](https://twitter.com/iwantmyrealname).

## Libraries

The libraries I'll be exploring are:

* [Argo](#argo)
* [JSONJoy](#jsonjoy)
* [ObjectMapper](#objectmapper)
* [SwiftyJSON](#swiftyjson)

Examples will demonstrate how each library handles: simple model creation, JSON to model translation, transforming values during translation, and translating nested models. These examples are not exhaustive of what each library is capable of.

## JSON

JSON will be retrieved from the Github API using [Alamofire](https://github.com/Alamofire/Alamofire) for networking. The JSON retrieved is the representation of the repo for this demo: [https://api.github.com/repos/hkellaway/swift-json-comparison](https://api.github.com/repos/hkellaway/swift-json-comparison)

The models present in the demo JSON are *Repo* and *RepoOwner*. Despite having many more attributes in the actual JSON, our *Repo* model will simply have have an *id*, *name*, *description*, *url*, and *Owner*. A *RepoOwner* will have an *id* and a *username*. 

A simplified version of the JSON we're using would look as such:

<script src="https://gist.github.com/hkellaway/a4d5304709f319ac4e93.js"></script>

## Code

You can explore the code in this post yourself by heading over to: [https://github.com/hkellaway/swift-json-comparison](https://github.com/hkellaway/swift-json-comparison)

Code for this project was written with Swift 1.2.

This project uses Cocoapods as a dependency manager with the following pods and versions:

* pod 'Alamofire', '1.2.3'
* pod 'Argo', '1.0.3'
* pod 'JSONJoy-Swift', '0.9.2'
* pod 'ObjectMapper', '0.12'
* pod 'SwiftyJSON', '2.2.0'

<a id="argo">

# Let's Explore

## [Argo](https://github.com/thoughtbot/Argo)

### A simple model

The *RepoOwner* model:

<script src="https://gist.github.com/hkellaway/ac2def3b984ff9acebd5.js"></script>

Models are characterized by:

* Importing *Argo* and its helper library *Runes*
* Representing the model as a *struct* with constants
* Creating an *extension* that conforms to the *Decodable* protocol
* Including a *create(_:)* function responsible for object creation
* Including a *decode(_:)* function that represents the translation between JSON properties and *RepoOwner* properties

### A more complex model

The *Repo* model:

<script src="https://gist.github.com/hkellaway/9b238a874e69eda19f4e.js"></script>

#### Property transformers

To translate the *url* property to an *NSURL*, we use a transformer function we wrote ourselves, *urlFromString(_:)*, in the *create(_:)* function.

#### Nested objects

*Repo* has a nested object - *owner*, which is a *RepoOwner* object. Given *RepoOwner* is also an Argo model, using it as a property incurs no additional work.

### Translation from JSON

Making a network call and translating the resulting *NSData* into our desired *Repo* model takes the following form:

<script src="https://gist.github.com/hkellaway/bd8f853e4eca1bb132fa.js"></script>

Result:

*repoId: 38541958*<br />
*name: swift-json-comparison*<br />
*description: Optional("Comparison of Swift JSON libraries")*<br />
*URL: https://github.com/hkellaway/swift-json-comparison*<br />
*owner: ownerId: 5456481; username: hkellaway*<br />

Translation is characterized by:

* Application code using *NSJSONSerialization* to deserialize the fetched data
* Use of the *decode* function to auto-magically handle translation

<a id="jsonjoy">

<br />

## [JSONJoy](https://github.com/daltoniam/JSONJoy-Swift)

### A simple model

The *RepoOwner* model: 

<script src="https://gist.github.com/hkellaway/83e289df8e3e5bc06d85.js"></script>

Models are characterized by:

* Importing *JSONJoy*
* Representing the model as a *struct* with constants
* Having the struct conform to the *JSONJoy* protocol
* Including an initializer *init(_:)* that takes in a *JSONDecoder* object and is responsible for the translation between JSON properties and *RepoOwner* properties

### A more complex model

The *Repo* model:

<script src="https://gist.github.com/hkellaway/0d7ec249c3a5189a54b4.js"></script>

#### Property transformers

To translate the *url* property to an *NSURL*, we create an extension on *JSONDecoder* and define the transformer function *urlFromString(_:)*; this function is used inside *init(_:)* to transform the desired value.

#### Nested objects

*Repo* has a nested object - *owner*, which is a *RepoOwner*. This model is translated in the *init* function by initializing a *RepoOwner* object with the corresponding decoder: *owner =  RepoOwnerJSONJoy(decoder["owner"])*. *RepoOwner* must also be a JSONJoy model.

### Translation from JSON

Making a network call and translating the resulting *NSData* into our desired *Repo* model takes the following form:

<script src="https://gist.github.com/hkellaway/65c93f3bd70f06393397.js"></script>

Result:

*repoId: 38541958*<br />
*name: swift-json-comparison*<br />
*description: Optional("Comparison of Swift JSON libraries")*<br />
*URL: https://github.com/hkellaway/swift-json-comparison*<br />
*owner: ownerId: 5456481; username: hkellaway*<br />

Translation is characterized by:

* Application code **not** having to use *NSJSONSerialization*
* Use of the *init(_:)* function to auto-magically handle translation

<a id="objectmapper">

<br />

## [ObjectMapper](https://github.com/Hearst-DD/ObjectMapper)

### A simple model

The *RepoOwner* model: 

<script src="https://gist.github.com/hkellaway/75a4575e9ebf02108c8d.js"></script>

Models are characterized by:

* Importing *ObjectMapper*
* Representing the model as a *class* with variable - i.e. non-constant - properties which must also be Optionals
* Having the class conform to the *Mappable* protocol
* Including a *required* failable initializer *init(_:)*, that takes in a *Map* object and calls the *mapping(_:)* function
* Including a *mapping(_:)* function that represents the translation between JSON properties and *RepoOwner* properties

### A more complex model

The *Repo* model:

<script src="https://gist.github.com/hkellaway/9cf59fcdddfab5255d3a.js"></script>

#### Property transformers

To translate the *url* property to an *NSURL*, we define that mapping with a tuple that takes in a *TransformType* class as its second argument: *url <- (map["html_url"], URLTransform())*. The *URLTransform()* class is included with ObjectMapper - other custom transformers can be made by creating classes that conform to the *TransformType* protocol.

#### Nested objects

*Repo* has a nested object - *owner*, which is a *RepoOwner*. Given *RepoOwner* is also an ObjectMapper model, using it as a property incurs no additional work.

### Translation from JSON

Making a network call and translating the resulting *NSData* into our desired *Repo* model takes the following form:

<script src="https://gist.github.com/hkellaway/b5bdddb8f65e2340bfd1.js"></script>

Result:

*repoId: Optional(38541958)*<br />
*name: Optional("swift-json-comparison")*<br />
*description: Optional("Comparison of Swift JSON libraries"))*<br />
*URL: Optional(https://github.com/hkellaway/swift-json-comparison)*<br />
*owner: Optional(ownerId: Optional(5456481); username: Optional("hkellaway"))*<br />

Translation is characterized by:

* Application code using *NSJSONSerialization* to deserialize the resulting data
* Use of the *map(_:)* to auto-magically handle translation

<a id="swiftyjson">

<br />

## [SwiftyJSON](https://github.com/SwiftyJSON/SwiftyJSON)

### A simple model

The *RepoOwner* model: 

<script src="https://gist.github.com/hkellaway/c645720260bf4bf08c9f.js"></script>

Models are characterized by:

* **Not** importing SwiftyJSON
* Representing the model as a *struct* with constants

### A more complex model

The *Repo* model:

<script src="https://gist.github.com/hkellaway/3e989146245711871a99.js"></script>

#### Property transformers

Property transformation is not handled in the model.

#### Nested objects

Nested objects are not handled in the model.

### Translation from JSON

Making a network call and translating the resulting *NSData* into our desired *Repo* model takes the following form:

<script src="https://gist.github.com/hkellaway/6f89ad98e4eff5aed849.js"></script>

Result:

*repoId: 38541958*<br />
*name: swift-json-comparison*<br />
*description: Optional("Comparison of Swift JSON libraries")*<br />
*URL: https://github.com/hkellaway/swift-json-comparison*<br />
*owner: ownerId: 5456481; name: hkellaway*<br />

Translation is characterized by:

* Application code **not** using *NSJSONSerialization*, rather creating a *JSON* object with the *init(data:options:error:)* initializer, to deserialize the resulting data
* Application code handling translation between JSON properties and model properties

# Conclusion

Each of the libraries presented here takes a different approach to how models should be set up and how JSON can be translated into those model objects. 

While this post didn't delve into theorization on which might be better than the other, I certainly hope it helps when it comes time to evaluate such libraries for your next project. Again, you can check out the code seen in this post in action here: [https://github.com/hkellaway/swift-json-comparison](https://github.com/hkellaway/swift-json-comparison)

Happy coding!

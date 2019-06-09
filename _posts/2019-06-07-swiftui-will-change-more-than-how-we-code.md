---
layout: post
title: SwiftUI Will Change More Than How We Code
date: 2019-06-07
categories:
- blog
tags:
- tech
- emerging tech
- ios
- swiftui
status: publish
type: post
published: true
---

Cross-posted from the [Prolific Interactive Blog](https://www.prolificinteractive.com/2019/06/07/swiftui-will-change-more-than-how-we-code/)

My career as an iOS engineer started in earnest in 2015. It’s only been 4 years, but I’ve already seen the rise and recession of major technologies and paradigms. Such is the life of one devoted to iOS; it can be equal parts destabilizing and exciting. I found the wobbles coming back this past Monday, when Apple [announced at WWDC](https://www.apple.com/apple-events/june-2019/) the release of a declarative UI framework. [SwiftUI](https://developer.apple.com/xcode/swiftui/) is a big deal. Obviously, it has implications for our UI code – but the more I dig into it, the more I understand how much farther it could reach.

When I mention witnessing major technologies rise and recede, it’s been most stark with Swift and Objective-C. In my work, Objective-C is alternately relegated to the status of a [neat specialization](https://www.quora.com/What-can-Objective-C-do-that-Swift-cant), or a respectable relic, or (quite often) a ball-and-chain. That last one has manifested at Prolific in struggle with maintenance and debugging for teams that are less and less familiar with Objective-C. It’s [not that Objective-C has completely gone away](https://blog.andrewmadsen.com/post/182862756395/how-many-apps-use-swift-in-2019) – but there is an undeniable shift towards Swift.

My career has changed over the past 4 years too. Where I was an iOS Engineer, now I’m an Engineering Manager – so my focus is less on developing code and more on developing engineers (who then develop code). And that has really changed my lens on announcements like this. I’m lucky and happy that at Prolific, being a Manager doesn’t mean giving up being an Engineer. Just last week, I gave a talk to our engineers on understanding React and Redux for iOS; I joked about how unlikely it was for Apple to reveal something like React at WWDC. I was so wrong! When SwiftUI dropped, I rolled up my sleeves too and dug into the [SwiftUI Tutorials](https://developer.apple.com/tutorials/swiftui). What I found myself struck by more than the ramifications for code were the potentialities around things like hiring and education, keeping a team of busy engineers up-to-date, reforming strategy and process – the things the manager side of my brain is as fascinated with as code.

After living the experience of how Swift changed iOS development and how our engineering team changed around Swift, I find myself anticipating some of the effects SwiftUI may have. Of course, introducing a new major UI framework isn’t as seismic as introducing a whole new programming language – but I believe it has a lot of similar potential to change iOS development.

# Prepare for iOS Education to Change

Education for software engineers has evolved a lot over the past few years. Most notably, there’s been a huge swell of bootcamp programs and engineers receiving their education in bootcamps. I’ve seen this effect profoundly in my hiring work. Over time, a large portion of our applicants have shifted to coming from bootcamp programs – and many of our candidates primarily only knew Swift. These two things do go hand in hand. With such a large amount of education happening in bootcamps and online and them eventually teaching only Swift, it was only a matter of time for our candidate pool to reflect the shift.

Why do bootcamps teach Swift? My thought is it’s due in part to Swift being relatively “easy” – to teach, program, and create apps that are more manageable to maintain. We’re seeing some of that same [messaging about ease](https://developer.apple.com/xcode/swiftui/) with SwiftUI: it’s “an innovative, exceptionally **simple** way to build user interfaces… With a declarative Swift syntax that’s **easy** to read and **natural** to write…” (emphasis mine).

But SwiftUI is not going to be the primary driver here. Bootcamps will gravitate toward the dominant technology that Apple promotes. Their bottom line depends on giving developers skills relevant enough to place them in jobs. So, if Apple successfully pushes adoption of SwiftUI, then bootcamps will base their education on it. That’s what happened with Swift. And, then we’ll be one step closer to a world where many iOS developers *only know SwiftUI*.

Is this scary? Hard to say. What we have found with the engineers exiting brief bootcamps is they’re more akin to Swift Engineers than the Software Engineers you might expect from formal education – and no slight meant there having hired many amazing bootcamp grads. But how then do we understand competency? Is an iOS Engineer competent if they don’t know Objective-C? Arguably. How about UIKit?

# Form a Strategy for Achieving Competency Across the Team

Reflecting on Prolific’s ability  to train a team of Objective-C engineers to work in Swift  – amidst project deadlines – fills me with pride and gives some insight into how we could get there with SwiftUI. When our team decided to shift to Swift, we involved all of our iOS Engineers and encouraged them to get their hands dirty with Swift at app scope. We didn’t throw everyone in the deep end of production with zero exposure. And, we’ll be considering what a similar roll-out plan would look like for SwiftUI, undoubtedly referring to [how we pulled it off before](https://www.prolificinteractive.com/2016/05/25/objective-c-u-l8r-a-swift-transition-2/).

Truth be told, despite enforcing exposure to Swift in small projects and presentations, it didn’t really sink in until our engineers had to use it on a production app daily. As easy and simple as SwiftUI is marketed, becoming competent with SwiftUI across a team will require great effort. This is due in part, as mentioned, to the patterns and paradigms it encourages which aren’t evenly mastered across a team. It’s also a change in workflow: developing effectively with SwiftUI involves mastering Previews (i.e. live reload). That’s not a complaint; I cannot wait until Previews are a natural part of my workflow. But, it will take time to ingrain, especially if we’re switching between UIKit and SwiftUI views.

Our high-level approach to a transition to SwiftUI would likely be similar to that of Objective-C to Swift. We’ll make a call when to adopt and have a strategy for getting the whole team up to speed before a real road test is initiated. Along the way we’ll be realistic that there will be road bumps and learnings as the team gains expertise.

# Be Cautious About Changing Too Quickly

Prolific was a somewhat early adopter of Swift. We jumped into Swift about 6 months after version 1 was released and put a hard stop on doing Objective-C apps in 2016 as soon as our collective competency was fair. Being a product agency, engineering has to suit a wide range of criteria – from being responsible and future-defensive in the codebases we deliver to attracting and retaining talented engineers. I do think embracing Swift was the right call for those aspects among others, but I think we rushed in quicker than was strictly necessary and without diligently weighing [why some were sticking with Objective-C](https://www.hackingwithswift.com/articles/27/why-many-developers-still-prefer-objective-c-to-swift). So, in the excitement over SwiftUI and reactive paradigms, I’ll be urging us not to be hasty – to throw aside our invested knowledge – without due diligence.

In hindsight, something I would have been a lot more cautious about was introducing Swift into an existing and well-functioning Objective-C codebase. Along with the introduction of headaches from interop came the more profound difficulty of compromising the consistency of the codebase when mashing in what was hip in the Swift community. And hear this: even though it has “UI” in the name, *the consistency that mixed SwiftUI apps threaten isn’t just in the UI layer*. Much like with Swift, we’re going to see certain patterns and paradigms really captivate the community (e.g. reactive via the new [Combine](https://developer.apple.com/documentation/combine) [framework](https://developer.apple.com/videos/play/wwdc2019/722)).

This isn’t to say you shouldn’t have mixed codebases – but rather to be thoughtful and strategic about introducing SwiftUI to existing projects. Keep it isolated, have a plan for migrating older UI or clear reasoning when not to migrate. Articulate what patterns and paradigms the app will use where, have a plan for upgrading older features to eventually achieve consistency. The key part being, have a plan.

Lastly, yes, the tutorials for SwiftUI are beautiful – but they are still just toys. Time will tell where this framework goes sideways at scale. We didn’t quite anticipate, for example, the impact of the breaking changes for each Swift release and how unstable it was when we started to transition. With SwitUI, there’s already one major barrier for Prolific in that it’s for iOS 13+ only. Given we support at least one major version back, that’s a clear indicator we need not rush in.

# Realize the Intersections with Cross-Platform

The move to encouraging declarative UI and reactive programming isn’t all that revelatory if you’ve been following cross-platform for a bit. Or the [independent](https://componentkit.org/) [Swift/iOS](https://github.com/ReactiveX/RxSwift) [projects](https://github.com/ReSwift/ReSwift) that have explored them. Or Google’s announcement of [Jetpack Compose](https://developer.android.com/jetpack/compose) for Android a month back.

To focus on cross-platform though: both [React Native](https://facebook.github.io/react-native/) and [Flutter](https://flutter.dev/) leverage the same declarative and reactive concepts SwiftUI brings us. Both are also tied in different ways to web programming where, likewise, [these](https://reactjs.org/) [concepts](https://github.com/ReactiveX/rxjs) would be at home. The breadth and depth of what it means that Apple is promoting them too, I’m not sure – it points to interesting things like what it means to stay competitive as a Big Five,  the centering of web paradigms, the centering of cross-platform paradigms, etc. Regardless, we should consider what implications it has in the context of our work. Being a mobile agency that has and will explore cross-platform solutions, it’s important just to recognize that concepts are similar across approaches. At the very least, it has implications for cross-discipline training.

#And More

What snapped all of this into focus for me was reading through [tutorial](https://developer.apple.com/tutorials/swiftui/creating-and-combining-views) [after](https://developer.apple.com/tutorials/swiftui/building-lists-and-navigation) [tutorial](https://developer.apple.com/tutorials/swiftui/handling-user-input) and eventually realizing that there wasn’t a mention of Storyboards. No Storyboards! Moreover, [all](https://developer.apple.com/documentation/swiftui/views_and_controls) [of](https://developer.apple.com/documentation/swiftui/view_layout_and_presentation) [the](https://developer.apple.com/documentation/swiftui/drawing_and_animation) [domain](https://developer.apple.com/documentation/swiftui/state_and_data_flow) [concepts](https://developer.apple.com/documentation/swiftui/previews) and terms are brand new. We have `Binding`, and `State`, and `Environment`, and `Publisher` and…. We also have the more recognizable `View` and `Text` and `Button` (much Swift-ier naming though, right?).

We’re glimpsing a world where `viewDidLoad` and `UIButton` don’t exist. In fact, the [lesson on UIKit interoperability](https://developer.apple.com/tutorials/swiftui/interfacing-with-uikit) is saved for the end after many other “essential” tutorials including one named “Composing Complex Interfaces”. Readers could almost interpret this to mean: “integrating with UIKit is not *essential* if you’re doing SwiftUI right and, moreover, it’s a *complex* topic. So avoid UIKit if you can!”.

This is astounding for someone whose development world has revolved around UIKit for years. It may seem unfathomable, but the parallel of SwiftUI/UIKit to Swift/Objective-C calls us to imagine: a world where UIKit is something we interop with only when we absolutely need to, where we consider UIKit legacy, where entire apps are re-written so they won’t be “UIKit apps”, where new iOS developers know only vaguely about something called UIKit. Admittedly, it is really hard for me to think this could be in just a short handful of years. But isn’t this how hardcore Objective-C developers must have felt in the gold rush to Swift?

There are many more lessons here, with at least one that is really present for me. For those of us who have spent our iOS development careers tied to UIKit and have moved on to roles that involve less coding: if we want to stay sharp with iOS, we’re going to have to dig back in. We’re facing new paradigms, new syntax, new developer flows and tools. Knowing these well is not a question of *if* – but of when and how.

---
layout: post
title: Writing Imperfect Code
date: 2017-09-06
categories:
- blog
tags:
- tech
- clean code
status: publish
type: post
published: true
---

Cross-posted from the [Prolific Interactive Blog](https://www.prolificinteractive.com/2017/09/06/writing-imperfect-code/)

Young in our development* careers, we’re often told that code should be [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself). That we *absolutely must remove duplication. It feels dire sometimes: if duplication in a codebase exists, that code ought be burned at the stake. Maybe us along with it? It can feel like a parent saying “do as I say, not as I do,” or “you’ll understand one day.”

It is actually great advice. It comes from any tome on good programming practice by the masters in our field: [Clean Code](https://www.goodreads.com/book/show/3735293-clean-code) by Robert Martin, [The Pragmatic Programmer](https://www.goodreads.com/book/show/4099.The_Pragmatic_Programmer) by Hunt & Thomas, [Implementation Patterns](https://www.goodreads.com/book/show/781559.Implementation_Patterns) by Kent Beck, etc. Developers like Martin and Beck have been in the game for decades, and these books are attempts to crystallize their immeasurable knowledge in a way that is accessible– for the new developer all the way through the next generation of master.

But experienced developers know something: code cannot always be DRY. Indeed, if you read a post like [The Wrong Abstraction](https://www.sandimetz.com/blog/2016/1/20/the-wrong-abstraction) by Sandi Metz, you learn that there is a time and place when code *shouldn’t* be DRY. What gives?

Developers like Metz, I wager, have studied the masters and applied their techniques over and over – on real world applications, and recently. The advice they dispense comes from experiencing and witnessing principles put into practice and recognizing patterns. They’re here to give us the liberating reminder that code cannot be perfect.

I’m quite guilty, as a lot of us are, of perfectionism when it comes to code. The origin story for this post starts with me at the threshold of leading development on another application, recognizing that my perfectionism had slowed us down in the past. I knew that being *dogmatic* about DRY or about [protocol-oriented programming](https://developer.apple.com/videos/play/wwdc2015/408/) or whatever it was I deemed best practice was at odds with my deadlines. In searching for how other developers balance principle and practice, I found a slew of posts like Metz’s – knowledge as decentralized as a textbook is centralized, as context-specific as a textbook is general.

The experimental lens I’m taking to exploring these posts is to pick out advice that – in a soundbite – is about directly opposite the advice we’ve been given by the greats.

So here’s my advice for you, perfectionistic programmer:

* Do Repeat Yourself
* Use MVC
* Create Inflexible Interfaces
* Do Not Refactor
* Don’t Cherish Good Code
* Cherish Legacy Code


# How to Write Imperfect Code

## Do Repeat Yourself

“…duplication is far cheaper than the wrong abstraction” – [The Wrong Abstraction](https://www.sandimetz.com/blog/2016/1/20/the-wrong-abstraction), Sandi Metz

If all you’ve ever conceived of “duplication” as is shorthand for “bad,” it’s almost astounding to read that there are times when duplication is acceptable – even preferred. What Metz describes is a very common scenario: a developer has written a beautiful abstraction – another developer comes later with a new use-case which the abstraction almost suits so they add a parameter and some conditional logic; rinse and repeat until all traces of beauty are gone. Metz says, stop there and back out – *better to duplicate* the logic at every call-site, and then refactor to a new abstraction that actually makes sense.

This example is very context-dependent and it’s clear why that duplication is preferable. But a general takeaway is the simple fact that duplication *can* exist in a codebase, and can even be better than an alternative – as long as it’s an educated move – and likely one that is temporary on the path to better code. The extended version of the lesson we’re trying to teach junior developers when we bark about DRY is that the practice of drying out code often reveals better abstractions.

However, I would contend that *unnecessary* duplication is inevitable in a codebase of good size written at great speed. Indeed, if we look back to even the masters, the prioritized list of [Beck’s Design Rules](https://martinfowler.com/bliki/BeckDesignRules.html) has DRY in third place or four! The skill to learn as a lead developer is to be just as calculated as Metz in where and how duplication happens, if and when to remove it.

## Use MVC

There’s a corollary here regarding architecture. It’s been a trend over the last few years in the iOS community to condemn MVC and prop up [other architectures](https://www.prolificinteractive.com/2016/06/10/themes-in-modern-ios-architectures/). I’ve witnessed a similar insistence toward junior developers to just plain not use MVC – with that same parental tone of keeping DRY at all costs. I aim to have us recognize that there are few, if any, examples of programming strategies and architectures that are categorically bad or categorically essential. MVC can be a totally decent choice depending on context, timeline, prioritization, etc.

To take a slight detour here as an architectural enthusiast– in my experience, it’s often maintenance where architectural patterns go off-track. Maintenance cannot be enacted if there isn’t a clear idea in the first place. So, as a lead developer turned Software Architect, it’s your job to have a clear vision for how your architecture plays out. Moreover, you have to enforce it– at a pull request level scale, even– until the team can fly with it solo.

## Create Inflexible Interfaces

“Building a pleasant to use API and building an extensible API are often at odds with each other” – [Write code that is easy to delete not to extend](http://programmingisterrible.com/post/139222674273/write-code-that-is-easy-to-delete-not-easy-to), Thomas Figg of *Programming is Terrible*

As application developers, one of the skills we practice day in and out is interface design. Every object you create has its own interface, whether you’re deliberate about that or not. If taken to the nth degree though, the sentiment that well-designed interfaces are important can lead to spending far too much time designing gorgeous, flexible, extensible interfaces that are unnecessary in practice. Often times, what’s more warranted is a simple, uncomfortably application-specific interface that is easy for the next developer to understand and use.

Try this: start with the super-simple, reasonable, working interface and merge that. Even better, with tests. Then refactor to that generic, flexible one. Or, maybe don’t refactor.

Do Not Refactor

“Code that is written once doesn’t need to be beautiful and elegant. It has to be correct. It has to be understandable…This is code that never needs to be polished. This is code that doesn’t need to be refactored (until and unless you need to change it), even if other code around it is changing” – [Don’t Waste Time Writing Perfect Code](https://dzone.com/articles/dont-waste-time-writing), Jim Bird for *DevOps Zone*

This particular piece allowed me to diagnose a recurring condition I have: refactoritis. That is, refactoring too much. That is, thinking if I just get this class or component right it’ll pay off dividends in the long run. That latter thought might be right for the mission-critical components of your application, but logic dictates this cannot hold true for all components of your application. Refactoritis is recognizing that, but not being able to stop.

The attributes to better strive for, as pointed out in this quote, are *correctness* and *understandability*, and there’s often a point when our code has achieved that long before we’ve sunk hours polishing it to high shine.

This quote particularly calls out code that is “written once.” That’s a lot of code in our applications– this is code that doesn’t need to be picked apart with a fine-toothed comb, given that it works and is intelligible. On the other hand, the code that *is* written more than once, such as critical business logic or maybe the class you annoyingly have to add a `switch` case to every single pull request, should be the code you’re polishing.

## Don’t Cherish Good Code

“Good code isn’t about getting it right the first time. Good code is just legacy code that doesn’t get in the way. Good code is easy to delete” – [Write code that is easy to delete not to extend](http://programmingisterrible.com/post/139222674273/write-code-that-is-easy-to-delete-not-easy-to), Thomas Figg of *Programming is Terrible*

We should get by now that there’s no such thing as writing perfect code. But what about just good code? We might feel our DRY, [SOLID](https://www.youtube.com/watch?v=gkxmeWvGEpU), loosely coupled, [VIPER](https://www.prolificinteractive.com/2016/07/01/building-a-reusable-e-commerce-framework-using-viper/)-ized code is good stuff when we submit that pull request– and we may very well be right. But code is at the mercy of time: all code becomes dreaded Legacy Code. Perhaps truly good code is legacy code we work with for a couple days and don’t want to just blow up.

Or, maybe good code is legacy code that is already easy to blow up! What a perspective shift to think we’re not to write code that’s *so good it can last forever*, but write code that’s *so good it can be disposed of*. It’s a fact that the developers working on the project in the future – who may even be us – are going to modify our beautiful code. We should write in such a way that that’s not painful and bug-prone.

Another takeaway here is not to cherish your own code or even code written by those you admire; all code might need to be refactored or removed. I like Metz’s phrasing of this sentiment: “Existing code exerts a powerful influence. Its very presence argues that it is both correct and necessary…Don’t get trapped by the sunk cost fallacy.”

Just because code has been around for a long time or written by someone prestigious doesn’t mean it should stay by virtue. And, when you find that code that is no longer suitable, what will make it *good* in that context *is* that it’s easy to extricate.

## Cherish Legacy Code

“It’s important to remember that when you start from scratch there is absolutely no reason to believe that you are going to do a better job than you did the first time” – [Things You Should Never Do, Pt. 1](https://www.joelonsoftware.com/2000/04/06/things-you-should-never-do-part-i/), Joel Spolsky of Joel On Software & [The Joel Test](https://www.joelonsoftware.com/2000/08/09/the-joel-test-12-steps-to-better-code/)

Speaking about blowing up code though – don’t be too trigger-happy. At first glance, most legacy applications seem terrible. The strong temptation is to obliterate them and start anew. Some of this can be ego (“I can write better code than this!”); a lot of it is that we’re much more practiced in writing code than reading it.

“Things You Should *Never* Do” (emphasis mine) contends that it’s foolhardy to throw out a legacy codebase that represents so much accumulated knowledge on how to solve a problem and how to avoid bugs in the system. Not only that, but there’s no reason to think that you will actually do it better! So if you are feeling that urge to detonate, reflect on all that you’re getting rid of. Try this: stick with that codebase for a few days before writing it off.

Though, saying you should *Never* Do something is rarely true. A response was written to “Things You Should Never Do” by another author I admire, Jeff Atwood of Coding Horror. In [When Understanding Means Rewriting](https://blog.codinghorror.com/when-understanding-means-rewriting/), Atwood points out that rewriting code is a tool for understanding that code– which I couldn’t agree with more. (Pro Tip: One of the ways I’ve personally gotten better at object and library design is by picking a simple [pod](https://cocoapods.org/) and refactoring/rewriting it for readability).

Especially as a lead developer, it’s your responsibility to understand how the business-critical portions of your project work. Make a thoughtful decision on whether blowing up the existing legacy application is necessary to achieve this. If what you’re really seeking is understanding, rewriting part of an application is perhaps all you really need.


# Perfect the Imperfect

“No one in the brief history of computing has ever written a piece of perfect software. It’s unlikely that you’ll be the first. And unless you accept this as a fact, you’ll end up wasting time and energy chasing an impossible dream” – *The Pragmatic Programmer: From Journeyman to Master* by Andrew Hunt and Dave Thomas

One of the quintessential texts I mentioned earlier is *The Pragmatic Programmer*. The subtitle of that book is *From Journeyman to Master*. The various authors mentioned in this post, including its own, are the Journeypeople described there. That’s likely you, too. Journeypeople have perspective and context which complicates the teachings of the masters. They can and should use their real-world experiences to inform less didactic approach.

Let’s review some insights from the “advice” I gave that would make a perfectionist cringe:

* Codebases will exhibit duplication
* Using MVC isn’t bad
* Not every object needs an infinitely eloquent interface
* Not every object is worthy of refactoring
* Don’t meticulously write code as if it’s going to live forever
* Don’t impulsively throw away code that’s been around forever

And more action-oriented:

* Make an educated decision when to employ duplication or leave duplication intact
* When employing an architectural pattern, make a point to clearly define and carefully maintain it
* When designing interfaces, make something *simple* – then go from there
* When implementing logic, make something that *works* – then go from there
* Write your own code and review others’ with the mindset that it can and should be extricated when it doesn’t suit current needs
* Make an effort to understand a legacy codebase and the impact of starting over

We are all at a different place in our journey of learning application development. And, honestly, a less-experienced version of me couldn’t have deeply understood these points– that took time and experience living the exact scenarios these Journeypeople are talking about. I have dogmatically applied DRY, I’ve unthinkingly eschewed MVC, I’ve obsessively refactored, I’ve unwittingly tossed entire legacy applications. And so has just about every admirable developer you know.

Young in our development careers, it *is* vital to work through the concrete mechanics of applying principles like DRY. For lead developers, however, there’s a task at-hand that isn’t immediate in the texts we point to: developing perspective on the principles.

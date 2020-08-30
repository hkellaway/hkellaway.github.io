---
layout: post
title: A Tale of Third-Parties or How to Stop Using My Code
date: 2020-08-30
categories:
- blog
tags:
- tech
- ios
status: publish
type: post
published: true
---

This is the tale of [Gloss](https://github.com/hkellaway/Gloss), my first major contribution to the open source iOS world. It is Yet-Another-JSON-parsing-library that I released in 2015.

 Let me take you back there. 2015 was a time when the Swift language was young and intrepid Swift developers didn't have a first-class option for JSON parsing. This caused [many](https://github.com/SwiftyJSON/SwiftyJSON) [third](https://github.com/thoughtbot/Argo)-[party](https://github.com/tristanhimmelman/ObjectMapper) [JSON](https://github.com/Anviking/Decodable) [parsing](https://github.com/delba/JASON) [frameworks](https://github.com/matteocrippa/awesome-swift#json) to pop up. It became an in-joke in the community, *What's the JSON parsing flavor of the week?* Each library saw some amount of success, each with its own [tradeoffs](/blog/2015/08/16/introducing-gloss-json-parsing-swift#why-though), and none categorically better than the rest.

Gloss itself wasn't even a standout on the JSON parsing playing field. I'm convinced it survives to this day only because a Ray Wenderlich tutorial once used it (fun fact!) which caused it to be adopted by apps and SDKs that otherwise wouldn't. Just out of the blue one day, I saw my GitHub stars rising astronomically (for me) - and that's when things changed. 

 Once its adoption reached a critical mass, it was no longer responsible to consider it a toy project I could toss aside. For the first year or so, I didn't even want to toss it aside - I was having a blast! For a developer young in my career, it was validating and illuminating to maintain open-source software that other people relied on. I learned a ton about writing usable libraries and about communicating with other developers in the open. But...it got old once I wanted to use my coding energy elsewhere. Yet, I've been maintaining Gloss for 5 years.

Times have changed for Swift developers. There is now an excellent first-class option for JSON parsing in Swift, and it should absolutely be your first choice. Of course, I'm referring to [Codable](https://developer.apple.com/documentation/foundation/archives_and_serialization/encoding_and_decoding_custom_types). So this weekend, I finally made a big move to help people **stop using my code** and start using something better.

The audience for this post is two-fold. First, it's for anyone using Gloss today to get a more colorful backstory to the [Migration Guide](https://github.com/hkellaway/Gloss/blob/production/GLOSS_CODABLE_MIGRATION_GUIDE.md). Second, it's for the developers who nod their heads knowingly when I describe maintaining such a library: the developers who maintain their own libraries with superior successors. Probably some Swift developers who maintain JSON parsing libraries. For you, I'll share some tactical things I did to still feel accountable to the developers that rely on my code.

## Where Do We Begin?

I've been thinking about doing this for quite a while. I've started many branches only to have abandoned them. What brought me to getting serious about it was what brings a lot of humans to change: pain. 

It wasn't the pain of maintaining `Gloss`. After years of `Codable` floating around, I now rarely get GitHub Issues or Pull Requests. No, it was the pain of using a (different[)](https://github.com/SwiftyJSON/SwiftyJSON) third-party JSON parsing framework at my workplace and wanting so much to use `Codable`, having to create my own workarounds for doing so, and thinking what a relief it would have been if that library could help me out. It was realizing that I'm potentially putting users of my library through the same pain. 

So, instead of my stagnation giving others another reason to stagnate - I'm going to offer a boost in the right direction.

### The Code

Once I set my sights on doing this, I realized that I didn't know how to "do" it. There isn't a guide (that I know of) of how to gracefully help users of your library get over the hump to another. Is it purely a code solution? A single document? Do I make breaking changes? Do I simply archive the repo without a word?

I very often fiddle in code when the outline of a solution is there but the details are still primordial goop. And, this case was no different. I asked myself: *if I was a user of Gloss trying to move to `Codable` piecemeal, what splint might I write in between the two?* With some fiddling later, a path forward was lit.

I made the decision to release a backwards-compatible version of the library that included helper methods safe to place in current implementations that would aid the migrator in uncovering where their `Codable` definitions would go awry. Indeed, that's exactly what I've done in my own workplace code while migrating to `Codable`. Given its a tactic I've proved out on real-world applications at scale, it's something I feel good suggesting to others.

What helped immensely with this process is that I had a [Demo project](https://github.com/hkellaway/Gloss/tree/production/GlossExample) waiting that uses Gloss as well as a [suite of tests](https://github.com/hkellaway/Gloss/tree/production/Sources/GlossTests) verifying its functionality. I was able to work out many kinks in my splint by migrating my Demo project and I feel much more confident my work is backwards-compatible with my tests all green. 

One of the many lessons Gloss taught me, is the elements that should be included in a professional open source library. That topic alone is enough for another post - but, to say the least, a good Demo project and test suite are it.

### The Migration Guide

Once the implementation approach was figured out, writing a [Migration Guide](https://github.com/hkellaway/Gloss/blob/production/GLOSS_CODABLE_MIGRATION_GUIDE.md) became much simpler. The point of it is to illustrate just enough to help the dedicated migrator get busy. 

What I came to realize is that the Migration Guide cannot cover every scenario out there. It is those invested in migrating and in understanding how Codable expresses itself (which is a boon to any iOS developer!) that will lean heavily on this document. I did extra diligence to make starting on migration as copy-pastable as possible. With this document in hand, I'll no longer entertain feature requests or troubleshooting for folks not on the migration path.

### The Rollout

With Code and Guide ready, the last piece was to figure out how to get it all out to the world. Of course publishing said Code and Guide are part of the rollout - but what else? 

Early on I determined that part of the point was to keep new developers from picking up `Gloss` instead of `Codable`. So, the first place to deter them is the `README`. I'll be honest, it was hard to take down a README that I worked on for over 5 years, but it's the right thing to do. I kept a [backup of the former README](https://github.com/hkellaway/Gloss/blob/production/README_ARCHIVE.md) for reference, but the new README serves one purpose: a stop sign with only directions on how to start migrating.

A couple other good leverage points to stop folks from picking up Gloss or attempting feature development are at Issues and Pull Reuqests. So a new [Issue Template](https://github.com/hkellaway/Gloss/blob/production/ISSUE_TEMPLATE.md) and [Pull Request Template](https://github.com/hkellaway/Gloss/blob/production/PULL_REQUEST_TEMPLATE.md) were in order.

Lastly, I'm a big fan of writing down those things that exist [between](/blog/2017/09/06/writing-imperfect-code) the [technical](/blog/2016/06/10/themes-in-modern-ios-architectures) and [non-technical](/blog/2019/06/07/swiftui-will-change-more-than-how-we-code) - at the least as a reference for myself, with hope it'll be helpful for others. And, that's why I also chose to write a blog post as part of the rollout.

### Then What?

In working through my own solution, it became apparent that *breaking changes* would likely both help ease migration and enable Gloss to be more opinionated in the direction of Codable. The jury is still out on whether I'll pursue those breaking changes, or leave things as they are and await any feedback as folks (hopefully) work their way through migrating. I'll be waiting expectantly to see if I get any new Issues post-release.

 Then, once enough time has passed, I'll finally hit the button that marks a repo as `read-only` and close the chapter of my life that included Gloss.

## Steps to Enable Other Developers to Stop Using Your Code Too

What follows is a little reference of just the steps I took toward getting Gloss migration ready:

* If you have a release in progress, finish up that release and ship it: that'll be your last release on anything that doesn't involve migration (example: [Gloss 3.1.1](https://github.com/hkellaway/Gloss/releases/tag/3.1.1))
* Write a backwards-compatible splint that helps migrators try out the new framework without harming their current integration
* Test your splint with realistic usage! Hopefully you have tests (and a Demo project) for your library and can confirm the splint doesn't affect expected behavior or make for a nightmareish integration
* Prepare a [Migration Guide](https://github.com/hkellaway/Gloss/blob/production/GLOSS_CODABLE_MIGRATION_GUIDE.md) once the shape of the splint is solidified
* Release a specific version of the library only containing that splint. You can now think of your library as before-migration and after-migration. New changes are made only to support migration; only changes compatible with that version are accepted; users on lower versions with version-specific fixes must be gently turned down and urged to upgrade (example: [Gloss 3.2.0](https://github.com/hkellaway/Gloss/releases/tag/3.2.0))
* Move your current README to an archive of that README (example: [Gloss/README_ARCHIVE.md](https://github.com/hkellaway/Gloss/blob/production/README_ARCHIVE.md))
* Create a new README specifying that the succeeding library should be used in place of yours - and thank everyone whose used and contributed your library to date! Make note that the library is now *Deprecated* and updates will only be made to help with migration (example: [Gloss/README.md](https://github.com/hkellaway/Gloss/blob/production/README.md))
* Update your [Issue Template](https://github.com/hkellaway/Gloss/blob/production/ISSUE_TEMPLATE.md) and [Pull Request Template](https://github.com/hkellaway/Gloss/blob/production/PULL_REQUEST_TEMPLATE.md) to push people towards migrating
* Write a blog post :)

After an amount of time has passed addressing migration issues, it's time to officially deprecate. At that point you can:
* Move to only having a singular branch on your repo (no more *develop* branch)
* If on GitHub, use the Archive feature to make the repo read-only
* Change the name and/or description of the repo to clearly indicate it's *Deprecated*
* Hands off keyboard

You may not follow every single step, some of the steps might not work at all for your library, you may add a step of your own. Regardless, my hope is it's helpful to see how one maintainer puzzled their way through this process while still feeling accountable.


## The End

Amidst preparing this piece, I stumbled upon the remains of a JSON parsing library written by an iOS developer whose code and communication I admire ([JohnSundell/Unbox](https://github.com/JohnSundell/Unbox/blob/master/CodableMigrationGuide.md)). I came to find that John too made the call to push developers towards Codable with a Migration Guide to ease the journey. I took it as a sign I'm making the right move. While he & I released our libraries at nearly the same time, one of us deprecated a whole year ago and one of us is writig this now. Another lesson learned courtesy of Gloss!

That [Ray Wenderlich tutorial](https://www.raywenderlich.com/3418439-encoding-and-decoding-in-swift) that ushered Gloss here, you ask? Well, it's been updated to a Codable tutorial.

At the time of writing, Gloss has 1659 stars, 28 contributors, 36 releases...and 666 commits. Hm. I'll miss you too, Gloss - thanks for 5 years.


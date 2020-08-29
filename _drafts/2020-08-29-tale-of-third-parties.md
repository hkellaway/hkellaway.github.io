---
layout: post
title: A Tale of Third-Parties or How to Stop Using My Code
date: 2019-06-07
categories:
- blog
tags:
- tech
- ios
status: publish
type: post
published: true
---

This is the tale of [Gloss], my first major contribution to the open source iOS world. It's a JSON parsing library I unleashed in 2015. Yes, I know.

 Let me take you back to 2015. This was a time when the Swift language was young and intrepid Swift developers didn't have a first-class option for JSON parsing. This caused [many] [third]-[party] [JSON] [parsing] [frameworks] to pop up. It became an in-joke in the community, *What's the JSON parsing flavor of the week?* Each library saw some amount of success. I would contend that none were categorically better than the rest.

Gloss itself wasn't even a standout on the JSON parsing playing field. I'm convinced it survives to this day only because a Ray Wenderlich tutorial once used it (fun fact!) which caused it to be adopted by applications and libraries that otherwise wouldn't. Just out of the blue one day, I saw my GitHub starts rising astronomically - and that's when things changed. 

 Once its adoption reached a critical mass (thanks to Ray), it was no longer responsible to consider it a toy project I could toss aside. For the first year or so, I didn't even want to toss it aside - I was having a blast! For a developer young in my career, it was validating and illuminating to maintain open-source software that other people relied on. I learned a ton about writing usable libraries and about communicating with other developers in the open. But...it got old once I wanted to use my coding energy elsewhere. Yet, I've been maintaining Gloss for 5 years.

Times have changed for Swift developers. There is now an excellent first class option for JSON parsing in Swift, and it should absolutely be your first choice. Of course, I'm referring to [Codable]. That [Ray Wenderlich tutorial]() has changed too. It's been updated to a tutorial on how to use `Codable` - as it should. 

The audience for this post is two-fold. First, it's for anyone using Gloss today to get a more colorful take on the [Migration Guide]. Second, it's for the developers who nod their heads knowingly when I describe maintaining such a library; the developers who maintain their own libraries with superior successors. For those developers, I'll share some tactical things I did to still feel accountable to the developers that rely on my software. There may be a third audience too: the bright-eyed young developers who want to make the next best JSON parsing framework out there. To them, it's a cautionary tale.

## Where to Begin

I've been thinking about doing this for quite a while. I've started many branches only to have abandoned them. What brought me to getting serious about it was what brings a lot of humans to chainge: it was pain. It wasn't the pain of maintaining `Gloss`; finally, after years of `Codable` floating around, I rarely get GitHub Issues or Pull Requests. No, it was the pain of using a (different) third-party JSON parsing framework at my workplace and wanting so much to use `Codable`, having to create my own workarounds for doing so, and thinking how relieving it would have been if that library could help me out. It was realizing that I'm potentially putting the users of my library through the same pain. Now instead of my stagnation giving you a reason to stagnate alongside `Gloss`, I'm going to give you an out.

## What This Isn't

This isn't meant to say that every application calls for migrating `Gloss ` to `Codable`. There are always tradeoffs when making structural changes to an application.

What it is, though, is a boost in the direction of `Codable` for those already considering it, a stake in the ground against new users adopting `Gloss` over `Codable`, and a suggestion to think about what those tradeoffs would be if you're not yet on the `Codable` train.

## Steps to Enable Other Developers to Stop Using Your Code Too

* Write the splint
* Test your splint on realistic usage! + you should already have tests for your open source lib
* Relase a specific version of the library only containing that split. You can now think of your library as before-migration and after-migration. New changes are made only to support migration. This version should be backwards compatible - it'll allow folks to explore the migration without committing to any breaking changes
* You may then release a version that has breaking changes tha tsupport the migration (example `Decoder` > `GlossDecoder`)
* Move your current README to an archive of that README (example: README_ARCHIVE.md)
* Update your README to only read that the new framework should be used - and thank everyone whose used your library to date; note that it is deprecated and updates will only be made to help with migration
* Move to only having a singular branch on your repo - no more `develop`. Eventually, you can use GitHub's Archive feature when the migration has been out for a while with no Issues

## The End

If you use the Migration Guide to work on your own `Gloss` to `Codable` - please help improve the docs! 

At the time of writing, Gloss has 1659 stars, 28 contributors, 36 releases, and 666 commits. That last figure I'll take as an omen. The time has come for Gloss to pass.

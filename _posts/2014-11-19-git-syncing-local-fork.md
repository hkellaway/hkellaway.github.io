---
layout: post
title: Quick Tip - Syncing Your Local Git Fork
published: true
---

Having just wrestled for too long with how to sync my local branch - I thought I'd write a quick post on how I got it down.

Setup: I forked a project two days ago and have since been working on my fork locally. In the meanwhile, the original repository I forked had changes made. Before I continued with development, I wanted to make sure that my local branch and the original repository were in sync.

I thought this might be as simple as a *git fetch upstream* (https://help.github.com/articles/syncing-a-fork/) - but it turns out I did not have my *upstream* set. Upon doing a *git upstream*, I received the frustrating message:

*fatal: 'upstream' does not appear to be a git repository*

Indeed, doing a `git remote -v` confirmed this:

*origin https://github.com/my-project/repo-name.git (fetch)
origin  https://github.com/my-project/repo-name.git (push)*

After reading a bit, I attempted a *git remote set-url upstream https://github.com/original-project/repo-name.git*

This, however resulted in *fatal: No such remote 'upstream'*

More reading revealed the answer: I needed to *add* the upstream repository before *fetch*ing from it:

*git remote add upstream https://github.com/original-project/repo-name.git*

Doing a *git remote -v* confirmed I had it set correctly this time:

*origin	https://github.com/my-project/repo-name.git (fetch)
origin	https://github.com/my-project/repo-name.git (push)
upstream	https://github.com/original-project/repo-name.git (fetch)
upstream	https://github.com/original-project/repo-name.git (push)*

Happy coding!

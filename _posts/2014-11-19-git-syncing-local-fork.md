---
layout: post
title: Quick Tip - Syncing Your Local Git Fork
published: true
---

<p>Having just wrestled for too long with how to sync my local branch - I thought I'd write a quick post on how I got it down.</p>

<p>Setup: I forked a project two days ago and have since been working on my fork locally. In the meanwhile, the original repository I forked had changes made. Before I continued with development, I wanted to make sure that my local branch and the original repository were in sync.</p>

<p>I thought this might be as simple as a *git fetch upstream* (https://help.github.com/articles/syncing-a-fork/) - but it turns out I did not have my *upstream* set. Upon doing a *git upstream*, I received the frustrating message:</p>

<blockquote>fatal: 'upstream' does not appear to be a git repository</blockquote>

<p>Indeed, doing a `git remote -v` confirmed this:</p>

<blockquote>origin https://github.com/my-project/repo-name.git (fetch)<br />
origin  https://github.com/my-project/repo-name.git (push)</blockquote>

<p>After reading a bit, I attempted a *git remote set-url upstream https://github.com/original-project/repo-name.git*</p>

This, however resulted in *fatal: No such remote 'upstream'*

<p>More reading revealed the answer: I needed to *add* the upstream repository before *fetch*ing from it:</p>

<blockquote>git remote add upstream https://github.com/original-project/repo-name.git</blockquote>

<p>Doing a *git remote -v* confirmed I had it set correctly this time:</p>

<blockquote>origin	https://github.com/my-project/repo-name.git (fetch)<br />
origin	https://github.com/my-project/repo-name.git (push)<br />
upstream	https://github.com/original-project/repo-name.git (fetch)<br />
upstream	https://github.com/original-project/repo-name.git (push)</blockquote><br />

Happy coding!

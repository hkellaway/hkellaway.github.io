---
layout: post
title: Using Github for Lightweight Software Project Management
date: 2015-04-02
categories:
- blog
tags:
- tech
- project management
- product management
- github
status: publish
type: post
---

I've recently been playing around with using Github's Issues feature to facilitate some typical software project management techniques. Despite not being designed specifically for project management, Github Issues can be used as a lightweight substitute for [more](http://www.pivotaltracker.com/) [targeted](https://basecamp.com/?source=37signals+home) [software](https://www.atlassian.com/software/jira/) with just a bit of creativity and coaxing. This post will informally discuss my current process and any future insights I have while refining it.

Note: This post assumes you have a minimal basis in project management terminology or are willing to look things up. I'll be abbreviating *Github Issues* as *GI* here for readability.

# Before Coding

## Create the Backlog and the Icebox

At the inception of my project, I make two important GI [Milestones](https://help.github.com/articles/creating-and-editing-milestones-for-issues-and-pull-requests/): *Backlog* and *Icebox*. Generally speaking, the *Backlog* and *Icebox* are where stories, chores, or bugs you're not actively  working on are placed to be addressed later. These Milestones should not have a specific due date.

![Github Issues Milestones](/img/blog/github-pm-milestones.png)

If you've never heard such terminology, I recommend reading this handy piece: [http://www.sproutstech.com/blog/backlog-vs-icebox/](http://www.sproutstech.com/blog/backlog-vs-icebox/)

## Create Labels

[Labels](https://help.github.com/articles/creating-and-editing-labels-for-issues-and-pull-requests/) are used as descriptors for Issues. GI comes with a number of default Labels that are more oriented towards bug reporting and communication with open source contributors - *enhancement*, *help wanted*, *question*, etc. I prefer not to get rid of these or change their colors as they are a convention that may make open source collaboration on your project easier down the line.

I do, however, add a few project management specific Labels: 

### Blocked

This Label is for stories that cannot move foward unless another story is completed.

### Feature

This Label is for stories that introduce a new feature.

### 1 Priority, 2 Priority, 3 Priority

These Labels are for prioritizing stories that are in the *Backlog*.

### Other

I also tend to add a few other non-PM Labels that I personally find helpful: *core*, *design*, *feature*, *testing*

My starting list of Labels might look something like this:

![Github Issues Labels list](/img/blog/github-pm-labels.png)

You can utilize any color scheme for your labels - I would just recommend retaining the colors of the default labels.


## Brainstorm Stories

Before you even begin coding, brainstorm some stories. These can be anything - create xcode project, setup continuous integration, wireframe landing page. Anything. Create an Issue for each and assign its Milestone  as either *Backlog* (for stories that will definitely be done) or *Icebox* (for stories that are nice-to-haves or potential ideas, but are not clearly on the path to be executed).

# Sprints

Finally it's (almost) time to get started coding! At this point, I create a new Milestone named *Sprint 0* - and this time I give it a due date. This is where Sprinting begins:

![Github Issues Srint 0](/img/blog/github-pm-sprint-0.png)

## Pick Stories From the Backlog for the Upcoming Sprint

For stories that should be done next and can be done by the due date on your Sprint, change their Milestone from *Backlog* to the current Sprint. In this example, that'd be *Sprint 0*.

## Prioritize Your Stories

If the stories you've selected for your Sprint have no priority, use your *1 Priority*, *2 Priority*, and *3 Priority* labels to indicate how urgent each story is within your Sprint. I tend to label stories that need to get done before others in the sprint as *1 priority*.

## Label Your Stories

Add any other additional labels that describe your story - *bug*, *feature*, etc.

## Assign Your Stories

If they haven't already been given an owner, do so.

![Github Issues Backlog](/img/blog/github-pm-backlog.png)

## Work!

Now its time to start coding or designing or what-have-you. As you work, make notes on your stories, document subtasks in the comments by [creating checkboxes](https://github.com/blog/1375%0A-task-lists-in-gfm-issues-pulls-comments), @ mention others if you have questions, etc. Keeping all of this information in the story allows you to look back at it later.

Once you're done with the story, make sure to close the Issue. If it's a coding task that has an associated Pull Request, I also like to link to that Pull Request for later reference.

## Close the Sprint

When the due date for the current Sprint is reached, reevaluate all open stories - update their Milestone and Labels, comment as to why they weren't finished, re-assign them if needed, etc.

Afterwards, close that Sprint's Milestone.

![Github Issues Sprint Close](/img/blog/github-pm-sprint-close.png)

## Create the next Sprint

Rinse and repeat. Make a new Milestone called *Sprint 1*, assign it a due date, and keep chugging along.

# How does this work day-to-day?

Given this, how does each participant know what to work on on a given day?

The way I might orient myself is to first check my Notifications. Then, I head to the Milestones on GI, click on the current Sprint (at any given time, there should only be *Backlog*, *Icebox*, and the current *Sprint* in your Milestones), and filter by either what tasks are assigned to me or what is high priority. Then, I get get to work.

From a project manager standpoint, I'd take a look at the current Sprint, make sure priorites and Labels are right, that the number of stories open vs closed for that Sprint seems reasonable, whether I need to or can add more stories to that Sprint, etc. I may also take a look at the *Backlog* and prioritize what I can. Additionally, I might look at the *Icebox* and see if anything there could be realistically brought into the *Backlog*.

# Nice Features

There are some nice features built into GI that help this process out. 

First, it allows you to assign each story to an individual. This will provide them with a Github notification and an email, depending on their settings.

Second, collaborators can be tagged in comments on a story with the *@* symbol prepended to their username -- i.e. *@hkellaway*. This also notifies them and allows for conversation about stories to stay in one place.

Third, a search bar and filtering make it simpler to find information among your stories.

Fourth, a timeline of what's happened on a story is automatically generated. Each time you change a Label or a milestone or an assignee or link to a story, that action will be added to that story. This gives a simple look at how a story is progressing.

![Github Issue History](/img/blog/github-pm-issue-history.png)

# Not Nice Features

As I've mentioned, GI wasn't created for project management. It lacks features more robust tools have - customizable dashboards, statistics related to overall project progression, etc.

Another interesting side-effect is that, if you're working on an open source project, your project management process will be globally searchable on Github and your project will appear to have a ton of outstanding Issues - which some may interpret at-a-glance as you having a crazy buggy project.

# Some Project Management Is Better Than None

In my opinion, doing something to track what tasks you've done and have yet to do is better than not. Github Issues was an easy move as I've used it before for documenting bugs and random tasks. I also enjoy that it keeps all my work in one place.

All this being said, I am no professional project manager - this all comes from experience as a developer on teams with both effective and ineffective project management. Any ideas on how to improve this process? Leave them below!

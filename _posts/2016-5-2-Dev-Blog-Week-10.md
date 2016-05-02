---
layout: post
title: Dev Blog - How to build a holodeck, week ten
category: DevBlog
tags: DevBlog, weekly
keywords: 
---

This week has been a slow one. Apologies for the late post!

## Whatcha been doing?

I've spent about half the week refactoring my existing prototype code
such that I can have more than one prototype easily share some of the
core code I've written over the last few weeks. There's still a load
more effort here if I want to reuse the UI (gaze tracking, head gestures, etc)
without bringing over a copy of all the existing menus, and there's a lot
of work to be done with general flow control in the app (startup ordering,
which systems should be active, that sort of thing).

Creating prototypes from scratch is awesome fun - there's no legacy
codebase there to deal with, there's no restrictions in place - whatever
you need, you just write it, steal it or copy it.

Once you've got a codebase that's working, the temptation is to keep
adding to it. I've seen this happen in commercial settings where the end
result is the conclusion of many people actively jamming new code into
an ever more messy codebase, and in my previous roles actively avoiding
this (and architecting ways to mitigate the issues) was a key part of my
role.

It's been really liberating to spend a couple of months just avoiding even
thinking about this, but the time has come to start splitting up the
existing mess I've got in my environment scanning prototype and pull out
some of the useful code into separate parts. I can't avoid it any more -
I have to spent time thinking and planning around this. 

### COLLADA exporter

One of the easy parts to pull out is my COLLADA exporter code - that's now
up as a public repo on Bitbucket here:

[https://bitbucket.org/Evryway/evryway-colladaexporter](https://bitbucket.org/Evryway/evryway-colladaexporter)

If you think you might find it useful, clone it and use it. This is my
first bit of shared code in recent memory, so feedback is always welcome,
even if it's negative.

## What else?

I was intending to make a start on networking - but instead of that,
I've been messing around with the Vive in Unity. What a wonderful bit of
hardware. I've made a bit of progress reading button states and tracking
the controller pose - I've yet to bring this into the main codebase,
but there's still a lot of learning to happen before I attempt that.

It's also spurred me into thinking about a variety of side projects and games
I'd like to look at. I think I may spend a little time in the next few
weeks trying out some controller-related concepts, while I get the
core networking up and running in prototype 2.


## Next week ...

Oh, I really don't know this time. Let's play it by ear and see what
comes up!








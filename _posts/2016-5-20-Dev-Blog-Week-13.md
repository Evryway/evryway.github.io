---
layout: post
title: Dev Blog - How to build a holodeck, week 13
category: DevBlog
tags: DevBlog, weekly
keywords: 
---

I've always wanted to play God, and I'm a huge fan of god games.
One prototype I've had on my list to make for a while is some form
of solar system formation simulator. I've taken a very early stab
at it this week, with some lessons learned.

## TL;DR

[Week 13 - orbital simulation](https://youtu.be/aF7UsDtiqOg)
{% include youtubep.html id="aF7UsDtiqOg" %}

## But first, a quick catchup ...

Very early in the week, I managed to get voice comms working in
the portals prototype. That's awesome, and it means I can move on to
testing multiple people interacting (somehow) in the same space (somewhere).

The initial networking tests last week used a smiley face sphere,
and having that kinda-looking at you and talking at the same time "works"
(for some value of works) but it's not particularly compelling - it's better
than a telephone call, but it's not crazy immersive "I felt like I was there".

When I've managed a very rough first pass of something, I often hit a bit
of a mental block as to how to refine it. Rather than going for the next obvious
piece of the puzzle (avatars, for more realistic human presence) I thought
I'd take a bit more time to investigate controllers, and also think more about
what kind of information I'm going to send over the network.

## Networking, determinism and latency

I've written a few networked games in my time, both realtime and turn based.
Multiplayer realtime networking is another one of those challenging areas that
it's pretty darned hard to get right, but it's also an area where the
architecture of the solution you pick will mould and inform the rest of the
codebase. Dropping in Photon and copying their demo examples has gotten me
up and running, but I need to think properly about my strategy for passing
information between participants.

Determinism is pretty important in multiplayer games - you want all clients
to respond in the same fashion to the same inputs, regardless of who they are
coming from. Having a server arbitrate is the normal way to do this, but you
can do this on one of the clients if the load isn't too high. You need to ensure
that everyone performs the same actions at the same point in time, and any
randomness is the same on each client when the action is performed. It's possible
Photon has good tools to help this, so that's next up on the research list. If not,
I'll probably be writing some form of command stream over the network, as
synchronising all the state I want to chuck around will get pretty expensive pretty
fast; I'm looking at 30-40 transform nodes per person for their skeleton, plus
controller transforms and an array of input feeds.

Latency is also going to be a big player in the holodeck - I'm looking at more than
200ms right now with local tests, and we've all experienced the kind of delays
you get on a transatlantic phone call or watched a live news broadcast where the
delay can top a second or more. This is impossible to mitigate below the base level,
but I need to ensure that all local actions are immediate, but appear synchronised
to all the other clients, so I'll need to put some serious thought into structuring
the data transfer around this.

## Physical simulations

As soon as you start putting moving objects into the environment, you have to
start figuring out how to synchronise those over the network, so that seemed
like a great test for the week. I've also put in some basic Vive wand controller
wrappers so I can easily get the wand states. Hopefully I've written this in a nice
enough way that putting in Leap Motion as a controller will also work - that
will let me move over to Tango as a test environment for interactions. I'm currently
limited in the number of folks who both possess a Vive and are close enough to
physically meet! Hopefully that'll change over the course of this year.

I've been messing around with a couple of cool game ideas which incorporate physics,
but I've always wanted to make a solar system, and I've never really played with
physics in 3D before, so I've built a very simple gravity simulation. Check
out the video above, and if you'd like to try it on the Vive, drop me a mail and
I'll send a link to the exe.

[Week 13 - orbital simulation](https://youtu.be/ktdfx7UmpUM)
{% include youtubep.html id="ktdfx7UmpUM" %}

There's something quite magical about putting a thing in orbit around another thing.
I guess this is the kind of fun you can have up in the space station, but it's certainly
a first for me to be able to do this. It's a viceral realisation of something
that's always been a mathematical notion. 2D games (or 3D games on a 2D screen) can
obviously portray gravity and physics, but stepping inside it is really something
different.

Having this work across the network will be a challenge, but I'm a fan of
challenges, and hopefully it'll teach me all the stuff I need to know to get
the avatars synching properly.

## Next week ...

Next week is "taking stock" week. I've been on a three month trial with myself,
finding out if I can survive and be productive outside the structure of an
established studio. It's been a real journey so far, and it's time to decide
what the plan is for the remainder of the year.

I'll be looking at reaching out to interested folks to participate (local testers
initially) - If you're up for getting involved, drop me a mail!







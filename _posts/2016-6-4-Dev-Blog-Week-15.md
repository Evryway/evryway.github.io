---
layout: post
title: How to build a holodeck, week 15
category: DevBlog
tags: DevBlog, weekly
keywords: 
---

A holodeck ain't much fun if it's just you. Or rather, it's loads
of fun - but it's more fun with friends! This week I've been looking
at how to chuck stuff around the network, starting with a simple
painting prototype. 

## TL;DR

[Week 15 - multidraw](https://youtu.be/KyRjIHv4piM)
{% include youtubep.html id="KyRjIHv4piM" %}

## Networking and friends

A few weeks back I got very basic networking going - voice comms
and a floaty head being sent over the network. This gives you the
very basics of interactions with someone else, but the real goal is
to be looking at a full body avatar, and (potentially more importantly)
their interactions with the world.

As they interact with the world, they'll create and change things - in
this paint prototype, they're creating paint streaks in the world. This
raises a set of questions like, what do I send from player to player? Do
I send the whole drawing, or just changes to the drawing? Do I send a list
of inputs from the controller and re-create those on the other side?

There's a *fantastic* set of write-ups of how games do networking by
Glenn Fiedler, [which you can dive into here](http://gafferongames.com/networking-for-game-programmers/).
For a full physics simulation (such as the orbitals prototype, or any
of the real interaction mechanisms I'd like to have in the holodeck) we'll
need to use both state synchronisation and command streams, as well as
ensuring a local simulation. Command streams should be enough to create/delete/modify
objects, and state synchronisation will let us correct any non-determinism
by delegating authority over one or more objects to a single participant in the scene.

I've got a LOT of work to do to make a fully robust simulation work, but
the initial command stream tests are working quite nicely for painting. I basically
send out a set of commands every time a local player interacts (paint start, paint at,
paint stop) and then replay those on all the remote players.

Fixing up network errors / dropouts / people joining mid-session - those
are all complex issues but there's solutions to all of them. Making a fully
robust simulation that gracefully handles players coming and going, as well
as orbital mechanics or other dynamic modes - that's going to be a challenge ;)

### Multiplayer painting

The painting prototype is limited to the Vive for being able to draw, but I've
added support for the Rift and Tango as viewers, so you can be a floaty head
in the same room and what what the drawers are creating. Voice comms works on
all clients, so I think this is officially my first interactive state holodeck
prototype (portals has chat and heads, but that's no better than a phone call
until we've got proper avatars and motion going on).

## Interactions on Vive and mobile devices

The Vive wands are great, but I'd really like to see some fingers! I spent a bit
of time getting Leap Motion working on Vive, and if there's any interest I might
get the painting prototype working with finger inputs, I think that could be pretty
cool. Hand input on Tango doesn't appear to be properly viable at the minute
for a variety of reasons, which means I'll have to come back to it at a later point.

I should be able to use a selection of input mechanisms (hands, wands, oculus touch
when I get the hardware, etc) which is going to be truly educational to see. I only
hope that there's a mechanism that works on mobile in the very near future.

I will likely capture vids of the hands working once I've got something useful happening
with them - everyone has likely seen the Leap Motion Orion demos now, and I've not
got anything cooler than that working, yet.





## Help!

This time, I really do need help - I need alpha testers with Vive or Tango! drop me a
mail if you'd like to try it out. 

## Next week ...

I'm really not sure what's on the cards for next week, yet. I've been hoping to get
around to skeleton capture for a while, so that might be the thing ...





---
layout: post
title: Dev Blog - How to build a holodeck, week 14
category: DevBlog
tags: DevBlog, weekly
keywords: 
---
Very quick one this week, as I've got very little work done!

## Taking stock

I spent a chunk of time talking about the future with my better half, deciding
if it's worth continuing down this road, or whether I should be doing
something more constructive with my time. I'm lucky to have her support on this,
otherwise it would really be a fool's errand. The conclusion is: stick with it
for the summer, and re-evaluate then. Yay!

## Chickenpox and visitors

My youngest son came down with Chicken pox over the weekend, which
means we're in lack-of-sleep territory again. That's thrown out all our
plans, and taken up a big chunk of the week, but he's pulling through. I think
he got quite a light dose in the end, compared to his brother.

I also spent a leisurely afternoon showing Jason (my Boss Alien partner)
some of my work and my favourite VR experiences. It's always great to show
this stuff to people and watch how they react. I think the Lab and Orbitals
were the favourites, and Portals seems to work pretty nicely.

## Hand gesture tracking on mobile

I spent a couple of days looking at hand gesture tracking on the Tango tablet,
which I can now add to the list of "soon but not yet" technology. Beta terms
mean I can't discuss specifics, but the Tango tablet doesn't appear to provide
enough power at the USB port to reliably power the tracking device I was testing,
and when it does work it's proving somewhat unreliable. I've got a module ready
to drop in place when I decide to resurrect it, but I'm pretty disappointed that
I couldn't get this one to work right now.

Heading down that route made me realise how annoying my Android build pipeline can
be, as I need to plug in the USB cable, do a build, wait for it to deploy, unplug
the USB cable, plug in the gesture tracking device, slot the tablet back into the
Durovis Dive, tap on the screen, click through permissions, place on head.

## Android ADB tools in Unity

I'm sure someone will have done this already, but since I've created a logging window,
I thought it would be useful to add device management in there, and add TCP
support, which (in theory) lets me work without a cable.

After a couple of days wrangling, I can now pick from a historic list of attached
devices, connect (if it's TCP, otherwise you still need to plug in the USB lead)
and select a device (so you see logs, and make it a build deploy target).

This is wonderful for logging, but less so for builds and deploys, because
ADB over TCP is sloooow. So slow it's actually faster to do the cable dance above
than it is to just deploy the build over wi-fi. This is horribly sad. (and by slow,
I'm talking about 300KB/s transfers instead of 5-6MB/s transfers). This means
my Portals prototype build, which is about a 55MB APK, takes around 3 minutes to
deploy. This puts it firmly in the "get a coffee" time window, instead of the
sub 10 second window I prefer. Ho hum.


## Next week ...

* Networking in orbitals. 

* Hand gesture tracking on Vive (if I can find a mount or a big chunk of blu tak) and
Kinect integration into Portals.





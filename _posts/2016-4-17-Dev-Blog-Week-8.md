---
layout: post
title: Dev Blog - How to build a holodeck, week eight
category: DevBlog
tags: DevBlog, weekly
keywords: portals, vive, tango, holodeck, realtime
---

Portals, Vive, multiplatform - what an exciting week!

## TL;DR

You may have already seen this if you've read the post from
earlier this week. If not, enjoy!

[Week eight portals](https://youtu.be/EWsPTGHgrgg)
{% include youtubep.html id="EWsPTGHgrgg" %}

## Portals

After spending three weeks working on the environment capture process, I thought
it was high time for a change. There's loads of chunks of tech I need to get working,
and teleporting / portals is one of them.

I spent the first three days this week getting basic portals working on Tango,
as you can see from the video above. It's not super-pretty, but it's functional.

One of the main issues with the way I'm doing it [(see previous post!)](http://www.evryway.com/Portals)
is the cost of the rendertexture pass, as well as the quality issues with walking really close
to the portal.

Various folks have suggested using Stencils in the shaders instead, such that I simply
draw the garage and the living room, and the second thing to get drawn is clipped to just
the view through the portal. Technically, it should work (and be pretty simple!) but once
I started down that road, I've come across a host of issues. The way Unity handles cameras
on the Rift is very clever but precludes me easily setting rendertextures - it's fixable I think
but it'll take a bit of rework. And stencil rendering just seems broken right now on Rift,
so I might spend a bit more time next week getting that working.

## Vive

The vive arrived at the start of the week, and it's awesome. Lots of downsides compared to the Rift,
but lots of upsides too - it feels very Valve (which is a good thing!). Steam integration is excellent.
There's *loads* of content out already, many things for free, and there's enough to give anyone
a taste of room-scale VR.
[Job simulator](http://store.steampowered.com/app/448280/) is wonderful,
[Tiltbrush](http://store.steampowered.com/app/327140/) is wonderful,
[The Lab](http://store.steampowered.com/app/450390/) shows off some great concepts.

People all over t'internet are doing "compare and contrast" reviews with the Vive and the Rift,
and they are well worth viewing. The obvious differences are the controllers (Vive wins), the cable
length (Vive wins), comfort (Rift wins), visual quality (Rift wins), content (right now, Rift can
work with both stores, but many room-scale experiences only work in the Vive, so I'm tempted to
say Vive).

One thing that's really key, and I'm not seeing much in the reviews, is that they are BOTH absolutely
fantastic bits of kit. It's like arguing over whether or not you're going to buy the Ferrari or the
Lambo - if you can afford it right now, why not get both? If you have to pick one, either is great
(although you should try them before you buy them).

## Room scale

I did a few tests last week with the Rift, and the room-scale tracking is pretty damn good. You
are limited by the cable length, obviously, but the stability and precision of tracking is great.

It's NOT as good as the Vive, though. When the Vive works (99% of the time) it's rock-solid, and
you can happily move around in your room scale area. I've got the vast majority of the garage tracked,
enough to get a warning about having the lighthouses too far apart (about 6 meters diagonally apart?)

Room scale content really is VR, for me. I love the Rift, but the experiences so far are all a bit
throwback, as soon as you compare them to something like
[Fantastic Contraption](http://store.steampowered.com/app/386690/).

I tells ya what, though - cables SUCK. I mean really suck. I've seen a load of folks say that they
simply don't notice the cable, but I do. All the time. Whether this is because I've spent the last
couple of months doing untethered room-scale, of whether other people will find this too, I don't know.
I still find myself having to unwind in the world so I don't get wrapped up like some form of techno
squid is going to eat me.

## Both headsets at once

I've got the Vive and the Rift both plugged in (after buying a load more USB3.0 ports for my aging
machine) and "it works" - but only in the barest sense. I keep having to unplug on or the other to
get the system to gracefully switch, and as I'm doing my unity dev with the Tango and the Rift,
and doing most of my show-off demos to friends with the Vive this week, that has meant a load of
switching cables around. And both cables get tangled up in each other unless you very carefully
manage where the headsets live. I've now got them happily arranged on wall hooks, so grabbing
the Rift + remote, or Vive + wands, is pretty painless, but the first couple of days were really
nasty for getting wires tangled up.

I've heard rumours that they can both run at the same time on the same machine, but I'm not desparate
to go there, yet. One annoying thing is being unable to switch between the Vive and the Rift in 
Steam VR - if anyone knows of a way to do this without unplugging the relevant headset, please
let me know!

## So, Vive or Rift?

After a day, I was convinced the Rift was much better, apart from the room-scale and the controllers.
Now I'm not so sure. The Rift's comfort and ease of fitting and audio and thin cable and visual
quality are all wonderful. When Touch comes out and the Rift has decent controllers, I think it
may be the better package all round - but room-scale really is where VR is better than anything
you've ever done before, and right now no-one in their right mind would say Rift does room-scale
better than the Vive. I think if you don't have access to a Vive, you're missing out on the most
compelling content right now.

## What did you do with the rest of the week?

As soon as I got portals working, I wanted to see what it looked like in the Rift. Which meant
getting the Rift working in my main project (rather than a side testbed project I used for
previously looking at models).

Of course, this lead me down about ten new rabbit holes, each more wonderful than the last.
To date, I've re-written:

* All of my pose tracking code (which was due a rewrite any way) so that I have the concepts of head,
camera feed, hands, and any other arbitrary items I want to position as inputs to the system

* How I handle environments, now that I've got more than one of them

* the whole portal rendering process to use stencils (still WIP)

* Frames of reference (in general, and environment/portal origins in particular)

plus I'll likely have to do a big chunk of work at some point soon to get the Vive working,
ideally with controller inputs.

I'm almost back up and running again on both Tango and Rift in the single project, so that's good.
Lots of work ahead next week though! I'm going to try getting stencils working on Tango,
and then RT and stencils working on Rift, then back to environment capture improvements - having
a week of not working on it has helped me work through some of the issues in my head, so I feel
a lot fresher about it.

## Help!

Loads of issues this week - Unity cameras - how do I get two of them back again with the Rift? Do stencils work in VR
in Unity? How do I get up and running on Vive in Unity? Oh FSM, so many issues and problems.

Still, there's always ...

## Next week ...

More portals, more environment capture, more platforms, more videos.

And maybe some Kinect skeleton capture ;)







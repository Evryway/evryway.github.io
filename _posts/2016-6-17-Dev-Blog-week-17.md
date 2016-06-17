---
layout: post
title: How to build a holodeck, week 17 - More Avatars
category: DevBlog
tags: DevBlog, weekly
keywords: Avatars, Kinect, Unity
---

This week I've continued exploring Avatars, getting a rigged / skinned mesh up and running
in Unity, driven by the Kinect2. I've also been looking further into RGB-D sensors and
scanning software for facial and body capture.

## More shader effects for fire dancing

One thing that should be obvious to folks watching my various youtube videos is that they
all look pretty awful. Last week's dancing skeleton particle effects took about 15 minutes
to cook up, and it shows.

This [recent video](http://player.vimeo.com/video/169599296) by
[Method Studios](http://www.methodstudios.com/) wowed me last week, and
made me go off on a bit of tangent, thinking about how cool it would be to do some fancy
dancing shaders, which would be a massive diversion in and of itself. I've done a little
shader work before on games and tools, but it's been a while since I tried to do anything
artistic, so Monday and Tuesday were taken up with experiments with noise shaders, trying
to get something a bit more fire-like.

Monday was mostly fiddling with fire as a 2D particle in 3D space. I've looked at loads of
asset store fires, and there's a few beautiful examples, but I thought I could improve on most
of the free ones. 


Here's the latest iteration:

[Week 17 - fire dancer](https://youtu.be/quc61D3dnyQ)
{% include youtubep.html id="quc61D3dnyQ" %}

I'm using baked 2D noise as a source, with a colour gradient, an alpha wipe over time to make the flame
rise, and some math to silhouette the shape of the flame.

The 2D noise used in the shader caused me all sorts of grief, because I wanted the flames
to look like they were locked to the world space. Rotating the particle system breaks
the shader, as does observing from the side instead of the front. A wild rabbit hole appears!
So, I then spent the next two days looking into procedural noise, with 2D and 3D simplex
and perlin noise.

There's a great free asset on the Asset store for
[creating 3D noise shaders](https://www.assetstore.unity3d.com/en/#!/content/3957) which has, in the
source, links to a load of excellent info on 3D and 4D noise. I managed to create a few nice
3D noise shaders to remake my star - I was using a lovely asset from the asset store, but it was
giving me shader errors on Android, so recreating that became the next goal.

[Week 17 - sun](https://youtu.be/wO3ugEFkn-M)
{% include youtubep.html id="wO3ugEFkn-M" %}

3D noise should be great for a 2D effect (like the fire quads) but to make it move, I resorted
to translating (spinning, moving and scaling) the 3D spaces used for the noise - what I really
want is 4D noise. That's probably going to take a few days research and coding to create the
relevant shaders, and as this was a distraction from actually getting kinect working with Unity
avatars, I'm going to park it for a while, but it's been fun getting it working!

There's loads of great art being created with noise functions, like
[this](https://www.reddit.com/r/proceduralgeneration/comments/2rves3/fun_with_4d_noise/)
and I could probably spend a good few weeks messing around with this stuff, but I'm not going to,
because I want to get avatars working, gosh dagnabbit.

## Avatars part two

Just about every link I've seen discussing Kinect and Unity recommends the
[Kinect V2 Examples with MSSDK](https://www.assetstore.unity3d.com/en/#!/content/18708) package,
and I grabbed it early Wednesday morning. It's awesome, and huge, and supports Kinect 1, 2 and
(as far as I can tell) OpenNI drivers. I've barely scratched the surface yet, as I was intending
to use it as a springboard to create my own stuff but it's so fully featured I'm seriously considering
just using it directly - at the very least, it's given me an idea of the amount of effort I'll
need to put into writing this stuff properly myself.

One piece of wierdness that crops up with the Avatar driving is strange motion occurring on
hands and feet. It's probable that I've simply not got the correct settings set up on the tracking,
but the thumb-hand rotation doesn't appear to be working correctly (the cube-man shows the
thumb orientation, the unity avatar doesn't appear to reflect this at all). The knee-heel joint
also does very strange things - again, the cube man accurately reflects leg bends when you do things
like squats, but the unity avatar sticks the legs out to one side.

I have a feeling a lot of people are using this package as the base of their kinect tracking, as I've 
seen this behaviour all over the place, now I've been looking. You can see examples of both
these issues on this [Avateering example from Vitruvius](https://www.youtube.com/watch?v=_UMDyHIYPLE)
which I'm hoping is just some funky math in the package code, rather than a core problem with
tracking using the Kinect. I started to get stuck into the rotation math used to create the rig
node rotations and offsets, but didn't make much progress yet.

Hopefully next week I'll have some example videos to show off.

## Scanning and capture, again

Today, my [RealSense SR300](http://click.intel.com/intelrrealsensetm-developer-kit-featuring-sr300.html) arrived.
I nearly purchased a Structure sensor earlier in the week, but thought 400 bucks (plus shipping and
taxes and the like to the UK) was a wee bit steep. Turns out, when I was comparing sensor framerate
and resolution and the like, I missed the bit in the spec sheet where it says "range - 1.2m". Which means
it's not going to be much use at all for full body scanning. It's possible I'll be able to get some
use out of it for object scanning.

I'm going to look at turntables to make scanning "things" (objects and people, primarily) a more controlled
process. I've got a nice big lazy susan bearing on order, and I might be doing some woodwork next
week to build a platform for scanning things on. The reason for buying the bearing, rather than a turntable,
is that ultimately I'll be wanting to be able to scan people to a decent quality, which means a motorised
turntable that can take a load of 100+ Kg. I quite fancy doing a bit of work in the real world - all my
VR experiments are leaving me a bit disconnected from physical reality!

I've spent a little more time looking at capture software, including the 3D Scan and 3D Builder software
on the Microsoft store. They seem to work "ok", but still not good enough to just grab things out of the
box with no effort. If I want good results, I'm going to have to get set up for it, which means making
a little more space in the garage and probably a new desk.

## Next week

Probably more avatar work, next week. There's a lot to cover.





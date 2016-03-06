---
layout: post
title: Dev Blog - How to build a holodeck, week two
category: DevBlog
tags: DevBlog, weekly
keywords: dev blog, how to build a holodeck
---

I'm wearing a VR headset. I can see stuff in the world. Where am I?

This is a pretty complex question, when you start digging into it. Most of the details I'll discuss will be relevant for all the headsets out there on the market, but I'll be mostly focusing on the Tango as that's what I've been working with this week.

## TL;DR

[Week two - the globe, in the holodeck](https://youtu.be/Jo5ajCooYwA)
{% include youtubep.html id="Jo5ajCooYwA" %}

## Where am I in the virtual world?

First of all, you need some kind of position and orientation in your virtual space. Think of this as your starting point if you will. If you're a gamer, think of this as your spawning point.

![Minecraft Bed](http://img15.deviantart.net/3e35/i/2011/268/4/f/bunk_bed_by_kevster14-d4av727.png '(Image via DeviantArt)')


Most games will pop you into the world at a pre-defined point, and many let you specify a point that you'll arrive at or respawn at if you die. There's often a real-world metaphor that translates into selecting and anchoring your start position in the virtual world, for example sleeping in a bed in Minecraft or Terraria.

For my virtual world, I'll be starting with the Unity scene origin as my world origin - the point in space that maps to (0,0,0). This means the point in the world at 0 metres down each of the X,Y and Z axes. I'll also be starting with the assumption that I should be pointing "forward" in the scene. This means pointing down the Z axis in the Unity scene.

In the future, we'll look at arrival points, transit between these points and more - but that's a long way off yet.

#### Coordinate Systems

There's a whole host of assumptions baked into the descriptions above that complicate things. First off, which way is up?
which way is forward? which way is left and right? The way that people normally capture these is by describing a
[coordinate system](https://en.wikipedia.org/wiki/Coordinate_system).
Fortunately, we'll be doing all of our modelling in a [Euclidian space](https://en.wikipedia.org/wiki/Euclidean_space) for now.
Unfortunately, the specifics of "the coordinate system" cause all kinds of problems - and that's mainly because there's not just one coordinate system; there's many.

![LHS vs RHS](https://upload.wikimedia.org/wikipedia/commons/b/b2/3D_Cartesian_Coodinate_Handedness.jpg '(Image via Wikipedia)')

Unity uses what's called a Left-handed coordinate system, with the positive X axis aligned to "right", positive Y axis aligned to "up", and positive Z axis aligned to "forward". All very sensible if you ask me. If we just stay in that space, then it's pretty clear that the position (2,5,10) means somewhere that's 2 metres to the right, 5 metres up and 10 metres forward from the scene origin.

Of course, the Tango device (and all android devices in general) use different systems to describe a selection of coordinate spaces, and the [Tango has a LOT of coordinate systems](https://developers.google.com/project-tango/overview/coordinate-systems). There's the Device space (positions and rotations relative to the device). There's the Area_Description space. There's the Start_of_Service space. There's the [IMU](https://en.wikipedia.org/wiki/Inertial_measurement_unit) space (where the motion sensors "live"). Most of these spaces do *not* share the same coordinate system. Most of these are right-handed, but they nearly all disagree on which direction "up" is.

![Tango Frames](https://developers.google.com/project-tango/images/overview/coordinate-systems/tango-frames.png)

This isn't a problem specific to working with Project Tango, by the way. Moving between rendering engines invariably means moving into a new coordinate system, often with the handedness switched. Transporting assets between authoring packages like 3DS Max, Blender or Maya brings the same issues. In typical human fashion, if there's more than one way to do it, you can guarantee that someone has done it that way and believes it's the best way.

For the code I'm writing now, I'm going to have to deal with the conversions between the various spaces, but my mental model needs to be consistent, otherwise - well, you end up going crazy and your math breaks. So whenever I discuss positions and rotations, you can assume from this point onwards we're talking about them in the Unity-World coordinate system.

Before I stop talking about coordinate systems, though, it's worth pointing out that I've spent three days this week simply trying to understand (and in a few places, modify) the math that drives the Project Tango Unity examples. It's complicated to me (and I guess it needs to be!) If there's one thing that's true, it's that humans are not, by and large, built to mentally model three-dimensional translations between coordinate systems. If you've ever stood in a room twisting your fingers around imaginary objects while pointing at the sky with your thumb, then welcome to my world!

#### Frames of reference

Once we've agreed on (or transformed between) the various coordinate systems, we need to specify frames of reference. For example, I could say "I'm two metres away in the X axis" - but two metres away from what, exactly? The simplest frame of reference is the Unity Scene (occasionally I'll call this the Unity World). this means the (0,0,0) point is the origin of the scene or world space. If I choose the tango device itself as a frame of reference, then 0,0,0 means a point slightly inside the plastic shell of the tablet. If the back of my tablet is pointing along the X axis in world space, then a point "forward" from my tablet is actually "right" in the world space.

Moving between these various frames of reference is another transformation of the numbers. Fortunately for me, I can do most of this work in the unity world space coordinate system, so it's slightly brain-melting but not totally incomprehensible.

The Tango SDK provides a set of [frame of reference pairs](https://developers.google.com/project-tango/overview/frames-of-reference) which allow you to understand where something is relative to. The target frame is where something *is* and the base frame is where something is *relative to*.

## That's great! so, where am I in the real world?

As I move and rotate my device around in the real world, the information for position and rotation come back to me as a [Tango Pose](https://developers.google.com/project-tango/overview/poses). There's two primary base frames that matter - the "Start of Service" frame and the "Area Description" frame.

By default, the Tango device will begin with an origin in world space of where the app initially starts. If I start the app standing in the doorway to my garage - that's 0,0,0. If I close it, walk over to the middle of my garage and start it up again - that's now 0,0,0. There's no relationship between these two real-world spaces as far as the Tango device is concerned. This means that my Virtual world will re-centre itself each and every time I restart the device.

#### Drifting

Without having a constant frame of reference, the Tango device also suffers from a serious problem - drift. This means that if the device loses tracking for a while, you can suddenly find yourself moving in the virtual world when you're stationary in the real world - this is annoying for apps that use the device as a tablet, but much more severe (potentially nausea-inducing) for the holodeck. Worse than this, the device itself drifts slightly in position and rotation over time - which means as you walk around, if you return back to the place you started, you're normally not quite in the same place in the real world (and often not pointing in quite the same direction).


![Drift correction](https://developers.google.com/project-tango/images/overview/Drift_Correction.png)

#### Area Descriptions

the Tango SDK provides the ability to capture an area by using Area Description Files, and [Area Learning](https://developers.google.com/project-tango/overview/area-learning). Instead of providing a pose relative to the Start-of-Service origin, you have the ability to create an Area Description file, tell the Tango service to use that, and you get back a pose relative to the Area Description origin, as well as the Start-of-Service origin.

This gives us two primary benefits - firstly, there's very little drift. From the numbers I've been looking at in my debug tools, the position and orientation drift is on the order of millimetres when the device is localised to an area. That's pretty darned awesome in terms of tracking accuracy - probably not quite as good as the Vive, but certainly good enough to walk around looking at, under or over things in the virtual scene.

Secondly, I can specify a real-world origin space, and lock this to a virtual-world origin space. Every time I start the app, I'm looking in the same direction from the same point in space, both in the real world and the virtual world. bonus!

It can take a little while for the Tango to lock in to the area description localisation - you can see this happen in this week's video at around 23 seconds - the Area Description Lock icon goes from red to green, and the world jumps a few feet to the left. Prior to this, the app was using Start_of_Service localised data. After this, it uses Area Description localised data.

![Banana for scale]({{ site.url }}/assets/banana_grid.jpg)

Here you can see (with a *very* small banana for scale - probably the world's worst scale banana) the garage-space grid at ground level.
I've been using a very scientific method to define the origin of my world - I have put some gaffer tape on the floor with masking tape at one-metre markers.
When I create my Area Description, I simply plant my heel at the garage origin, place the tango device on top of my knee, ensure my leg is vertical, and begin recording the area.
My floor-to-kneetop distance is approximately 0.65m.
I'm not 100% certain where the exact centre of the device is, but I'm guessing it's between 20 and 50 millimetres below the top edge, so I can confidently say the ADF origin is at  somewhere around (0.0, 0.70, 0.0) in garage-space - give or take a few centimetres in all three axes.

I'm currently using the [Project Tango Explorer app](https://play.google.com/store/apps/details?id=com.projecttango.tangoexplorer) to create the area descriptions - I'll be adding this to the holodeck viewer app at some point, as this will become pretty important to do in-app on-device in the next phase of the project.

## Progress so far (20160304)

Since last week, I've added the following things:

 - Debug menu showing arbitrary text in VR space (currently showing lots of vectors)
 - Debug menu showing Tango status icons (connection to service, ADF localisation, SOS localisation)
 - Debug objects showing AD, SOS and AD_to_SOS nodes
 - ADF loading menu and correct offset between Garage ADF origin and Garage real-world origin
 - slightly less artistically challenged content
 - rewrote "all the things" to fix startup timing issues and tango device permission flow

I've had a bit of a stomach bug this week which hasn't helped progress, but it has made me back off working silly hours, which is a definite good thing. Slow and steady, folks - slow and steady.

I grabbed some assets from the Unity Asset store last week (a lovely table and chair and a fridge) and this week I've grabbed [Planet Earth](https://www.assetstore.unity3d.com/en/#!/content/23399) to drop in my environment.

## Reference links

[Unity Matrix programming examples](http://catlikecoding.com/unity/tutorials/rendering/part-1/)

[Android sensors overview](http://developer.android.com/guide/topics/sensors/sensors_overview.html)

## Help!

I've got a plan of attack which roughly maps out what I'm hoping to achieve next. There's a lot on there - prettier content, capture of real world environments into the holo space, speech and gesture recognition, networking, avatars. If you have feedback (or advice!) on any of these areas, drop me a mail, I'd love to know what people think they'd like to see next.

## Next week ...

We'll take a look at cameras, and start exploring environment capture.





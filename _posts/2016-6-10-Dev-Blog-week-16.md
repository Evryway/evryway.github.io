---
layout: post
title: How to build a holodeck, week 16 - Avatars
category: DevBlog
tags: DevBlog, weekly
keywords: avatars
---

How does one represent themselves to the world? A tricky question, both
physically and metaphorically. The apparel oft proclaims the man, according
to the Bard. This week, I've started to explore Avatars.

## TL;DR

[Week 16 - skeleton tracking](https://youtu.be/2xDDRWNtkro)
{% include youtubep.html id="2xDDRWNtkro" %}

[Week 16 - networked skeletons](https://youtu.be/mJ6GvdxakgE)
{% include youtubep.html id="mJ6GvdxakgE" %}

## Avatars - where to begin?

"Avatar" is typically used to describe either a deity in manifest form, or a representation of somebody
(or something, or some idea), often in a computer game. "Your" avatar can be your representation of
"you", as well as a channel for interactions both ways (from you to the world, from the world to you).

You can have no avatar at all (This is actually pretty uncommon, but it does work). You can have
an avatar that's visible to others only (typical in first person games) or one that's visible
to yourself as well (pretty necessary for third person games).

We're all quite used to the idea of playing a "character" in a computer game, be that Mario or Lara Croft,
and it's no surprise that the representation of that character gives you lots of information about
the environment in which the character participates, as well as the capabilities of the character
themselves. When you play street fighter, you can identify your opponents capabilities just by
looking at that character on the screen. If all the fighters had the same visual representation,
you'd have a much harder time figuring out what moves or powers you were up against.

So it's pretty clear that an avatar really matters, both to how you see yourself, and how others
percieve you when they interact.

## Representing an avatar in the holodeck

There's a few key things I'd like to learn as I move towards holodeck version 1.0. Some of them
are about self-identity, and a lot of that comes from the form and motion of your avatar in the
world space. Some of them are about communication - just how much is communication improved
when you have some form of realistic body to provide gestural queues? The last chunk of key
information is the specifics of how to actually capture/create a realistic avatar with the time
and budget constraints I'm under - this is another "How close can I get?" chunk of work.

### Rigging and skinning

The typical way that games (and current social experiences such as AltSpaceVR) represent you is to have
a [rigged and skinned](https://en.wikipedia.org/wiki/Skeletal_animation)
 human (or humanoid) mesh. [Here's an example](https://vimeo.com/30073532) of how a mesh
can be rigged (attached to a skeleton) and skinned (blend weights assigned)
so that it can move and deform like a human.

### Texturing

Once you've got a mesh that's rigged and skinned, you need to ensure you've got a nice
quality textured mesh to go with the model. The texture can be scanned, or it can be created
in a paint program.

### Animation

Once you've got a skinned, textured mesh, you then need to make it move. There's a variety
of techniques here, including direct animation playback (moving the skeleton rig around
to move the arms and legs) and [Inverse Kinematics](https://en.wikipedia.org/wiki/Inverse_kinematics)
or IK, which lets a controller move an end node (i.e. the hand) and the IK solver works out
where the rest of the body should be based on constraints (your arm can only twist this far,
your bones are this long, so your back needs to bend like *this* to allow your hand to be there).
The best games and movies will use combinations of both captured animation
([motion capture](https://en.wikipedia.org/wiki/Motion_capture)), hand crafted animation, IK
and other procedural tools to drive the model. My previous company had some fantastic tools
like [Morpheme](http://www.naturalmotion.com/middleware/morpheme/) which show how complex
all of this can get.

Of course, a human isn't the only way to represent an avatar - you can use robots, flames,
or a floaty yellow ball - they all serve the same purpose, but they all have a different
impact on how the player, and viewers, percieve your character.

## Making a realistic human model is hard

Getting a good looking human model is hard, and the closer it comes to photo-realistic, the harder it
becomes. Without getting stuck in conversations around the uncanny valley, I think we can probably agree
that the characters in ["The last of us"](https://www.youtube.com/watch?v=OQWD5W3fpPM) look pretty darned human, and 
the human-like characters in Altspace are not quite up to that level of fidelity.

The last of us:

![TLOU](http://static1.gamespot.com/uploads/scale_super/mig/0/7/1/0/1990710-652686_20120814_003.jpg)

Altspace:

![altspace](http://altvr.wpengine.netdna-cdn.com/wp-content/uploads/2015/12/ruben.gif)

and here's a *wonderful* TLOU cosplay image by
[Jordan Farbridge](http://jordanfarbridge.com/reigan-chan/product/the-last-of-us-bundle/).

![TLOU cosplay](http://jordanfarbridge.com/reigan-chan/wp-content/uploads/2015/06/DSC08386.jpg)

The Last Of Us is close to the pinnacle of quality when it comes to human models in games. There's a few
movies (such as Avatar, natch) that have really pushed the boundaries of what's capable, but even now
you can often tell straight away that the image is computer generated. The amount of effort (and budget)
that goes into creating these characters is enormous. Constructing and rigging the models, applying
textures, animating the model (and the face, and the mouth and eyes, and the hands) all take a big team
of expert artists months or years.

[There's a great video here](https://www.youtube.com/watch?v=CmrXK4fNOEo)
showing the development process of a single character, Senua, in the upcoming game Hellblade. You
can see the amount of effort that's gone into creating her, and the results are nothing short of
astounding.

## Doing this realtime with no budget

Here's lil' old me, trying to bring something to the party, and I've got a very constrained budget
(both time and money) so I'd like to create human meshes and drive them with realistic animation,
all in realtime. What's the solution?

Well, this week I've totally skipped the "human mesh" part of the avatar story, and gone directly
for a more abstract representation of a human. I'm using the
[Microsoft Kinect V2 sensor](https://developer.microsoft.com/en-us/windows/kinect/develop) 
to track the position of a human in the holodeck space, and I'm then taking the joint positions
and turning them into little particle generator points.

In the first video, I'm projecting the skeleton a few metres in front of myself in virtual space so
that I can see myself moving around. This feels pretty darned cool in VR, and I'd love to try this
out with someone else with the same setup (Kinect and Vive) - get in touch if you'd like to try it.

In the second video, I'm sending the skeleton node positions over the network, and reconstructing
the fire avatar on the Tango (which can also move around the scene using Tango tracking).

I'm not (yet) using that skeleton data to drive a meshed avatar, but that's the next obvious part
of the puzzle. I also need to look at driving the resulting mesh using just IK and animations, instead
of using the Kinect feed for two reasons. 1, most people don't own a kinect - and 2, the results
coming out of the Kinect are ropey as all hell. 


### Scanning tools and options

There's a few apps and tools out there that use my current pool of
[RGB-D](https://en.wikipedia.org/wiki/Range_imaging) sensors (Tango and Kinect)
to scan heads and bodies, but after trying out a selection of them (KinectFusion as an example)
they're all pretty ropey. I was hoping to use [ReconstructMe](http://reconstructme.net/) but that
doesn't appear to support Kinect V2.

Some of the best consumer-level results I've seen are from the [Structure sensor](http://structure.io/)
and the Itseez3D app, which can produce fantastic results for head and body scans. Here's an example
on Sketchfab from a few days ago by Roboindus:

<iframe width="640" height="480" src="https://sketchfab.com/models/2706a706a9d64678a7b817d1a59e9e62/embed" frameborder="0" allowfullscreen mozallowfullscreen="true" webkitallowfullscreen="true" onmousewheel=""></iframe><p style="font-size: 13px; font-weight: normal; margin: 5px; color: #4A4A4A;">
    <a href="https://sketchfab.com/models/2706a706a9d64678a7b817d1a59e9e62?utm_medium=embed&utm_source=website&utm_campain=share-popup" target="_blank" style="font-weight: bold; color: #1CAAD9;">RI011160605001</a>
    by <a href="https://sketchfab.com/roboindus?utm_medium=embed&utm_source=website&utm_campain=share-popup" target="_blank" style="font-weight: bold; color: #1CAAD9;">roboindus</a>
    on <a href="https://sketchfab.com?utm_medium=embed&utm_source=website&utm_campain=share-popup" target="_blank" style="font-weight: bold; color: #1CAAD9;">Sketchfab</a>
</p>

The Tango, in theory, is capable of performing this kind of scanning, but in practice the
quality and accuracy of the data produced mean the results are not anywhere near as good as the
example above, and I'm not (yet!) intending to spend months or years creating tools to compete
with Itseez - so it looks like I'll be getting myself an iPad Air and a structure sensor in the near
future to try and get some quality scans done.

Another option is the [Intel Realsense](http://click.intel.com/intelrrealsensetm-developer-kit-featuring-sr300.html)
developer kit, and as they are a lot cheaper I've got one on pre-order. Hopefully Itseez will support this hardware,
if not I'll be grabbing a structure sensor in the next month or two.

### Turning a scanned mesh into a rigged mesh

I'm not an animator, so I need some simple tools to rig and skin the resulting mesh. Here's an example
showing Sketchfab's Alban dancing, using a mesh created in Itseez and the Mixamo animation tools.


<iframe width="640" height="480" src="https://sketchfab.com/models/26d5265ae74f46b7926e3ce78393ab6c/embed" frameborder="0" allowfullscreen mozallowfullscreen="true" webkitallowfullscreen="true" onmousewheel=""></iframe><p style="font-size: 13px; font-weight: normal; margin: 5px; color: #4A4A4A;">
    <a href="https://sketchfab.com/models/26d5265ae74f46b7926e3ce78393ab6c?utm_medium=embed&utm_source=website&utm_campain=share-popup" target="_blank" style="font-weight: bold; color: #1CAAD9;">Gangnam Style</a>
    by <a href="https://sketchfab.com/alban?utm_medium=embed&utm_source=website&utm_campain=share-popup" target="_blank" style="font-weight: bold; color: #1CAAD9;">alban</a>
    on <a href="https://sketchfab.com?utm_medium=embed&utm_source=website&utm_campain=share-popup" target="_blank" style="font-weight: bold; color: #1CAAD9;">Sketchfab</a>
</p>

We're still in the uncanny valley here (especially with the foot movements and some of the arm constraints)
but these results are close to what I want to use, so I guess I'll be going down that route in the near future.


## Next week ...

Next week I'll probably look at getting the Kinect data to drive a Unity avatar, and get that synced over
the network. [Getting started on something along these lines](http://thesai.org/Downloads/Volume6No12/Paper_40-Real_Time_Talking_Avatar_on_the_Internet.pdf).

Or, I might take one more punt at fixing up some of the known issues with my scanner, and get the skeleton
tracking working in the Portals prototype.





---
layout: post
title: Dev Blog - How to build a holodeck, week nine
category: DevBlog
tags: DevBlog, weekly
keywords: mesh welding, looking forward
---

Week 9 - two months in (and a few days!) It's as good a time as any to look at
goals (short and long term) and figure out what to do next.

## TL;DR

[Week nine - tango drift](https://youtu.be/5RlYHLT_aHE)
{% include youtubep.html id="5RlYHLT_aHE" %}

[Week nine - garage in the rift](https://youtu.be/WJz0D7b4UxY)
{% include youtubep.html id="WJz0D7b4UxY" %}

## Environment capture improvements

I'm really starting to see my velocity drop on visual improvements to the
environment capture, mostly because I don't understand what I'm doing, and
partly because it's no longer blatantly obvious what the causes of the issues are.

I've spent a few days this week making the welds along the join between adjacent
grid cubes "work". I'm using a pretty simple approach - identify the grid face,
identify the normal axis, then try and weld across the other two axes. Chisel
produces very regular spacing (in my case, 4mm) along the "major" axis, so I identify
whether there's reasonable motion in the other axis and then move adjacent verts
to an average position along that axis. This breaks if the join isn't axis aligned,
or goes from horizontal to vertical, and it also has a threshold in place which works
for small gaps, but not huge jumps.

The first video above shows you a feed from the Tango while stationary, and the amount
of drift is much larger than my original tests. I'm not sure if I need to recalibrate,
but I've been working under the assumption that I'm getting 10-20mm out of "real" as a positional
delta, and it's closer to 200 mm in "normal" conditions, and that causes a lot of the texture
offsetting that's happening - not all of it, but enough to be basically unfixable.

#### Texturing

Projecting the texture directly was always a bit of a pipe dream, but as I close in on
getting it to work, the obvious remaining flaws are all going to be fairly tricky to solve.
Firstly, the mesh isn't perfect (by a long shot) so I'm often projecting an image onto
a mesh that doesn't actually exist, or projecting a gap onto a solid surface that shouldn't
be there.

I'm also projecting past the first set of polygons I hit, so for example the orange chair gets spread
all over the floor behind it until I go do a texture sweep of that area. This is happening
all over the place, and I'll need to put in some masking on the atlas blit, which is another
fairly big chunk of work.

I need to only do texture projection if the device is relatively stable, and that should only
take a day or two to get working - but I still haven't solved the projection not mapping
as expected (and I've re-written the math 5 times now). Given the drift, the bad projection,
and the lighting/exposure problems, making proper progress on this is also on the order of
weeks rather than days.

Due to the way I'm constructing my atlases (each atlas is N pairs of triangles arranged
as a square, and each triangle maps to a unique mesh triangle) the size of the atlas texture
dictates how big the resulting mesh object will be. I'm using one material with one atlas
texture for each mesh chunk. I need to ensure that these are kept under 65K vertices, otherwise
Unity automatically splits the mesh up, and for some unknown reason when this happens I get
really spurious mesh results (spikes all over the place).

To try and ensure this doesn't happen, I've capped my atlas textures at 2K*1K with a triangle
edge of 14 pixels (16 if you include a buffer to stop subpixel aliasing when drawing). This means
I've got 16384 triangles used on the atlas as a maximum, and as every triangle currently has
unique verts, that gives me 48K vertices as a cap per mesh object on export. 

Here's an example atlas texture:

![Atlas texture]({{ site.url }}/assets/week9/atlas_1.jpg)

I'm certainly not making the most of the texture currently, as I'm clamping projection
at a near distance which means the 16 pixel triangles will only ever be 4-5 pixels of the
source camera image. Fixing that will be another day or so of work. There's also a bit
of work to be done on defragging and consolidating on export. I never thought I'd need
to defrag a texture, but there you go.

The atlas textures are 2K*1K 24bit (5Mb uncompressed), and the resulting archive for the garage in the
second video is about 40MB. Uncompressed that gives me a 50MB COLLADA file and 12 textures
which weigh in at 30MB as PNG files.

On device, the textures are compressed and the mesh representation is much smaller, so
the runtime overhead is much less than half of of this. Game assets tend to be much smaller
than this (and look much better!) but we're not a million miles away from reasonable.


#### Meshing

The drift, and the way Chisel works, and the way I'm mangling the resultant meshes, are
all conspiring to produce very messy results. I need to see if one of my other Dev tango
devices gives me less drift, but it was never going to be really accurate results - the
point cloud data is just too noisy for that.

Chisel is producing double-walls and the like, due to the device drift,
which is going to be very hard to remove in any kind of automated fashion. I can maybe
work around this by only freezing once, but the "correct" thing to do here is to replace Chisel
with something more fitting for my specific purpose, which is a big chunk of work - really big
in terms of my prototyping window.

The welding gets me much less obviously glitchy results, but there's still some major issues
I haven't addressed. Mirrors, black surfaces and the like all
leave me with big holes in the mesh, and they're not easily fixable without using a different
mesh creation process, as IR is always going to be vague or wrong. Sunlight is also
an issue from the couple of outdoor tests I've done, and I'd really like to get out of
the garage at some point.

The Garage mesh is about 500K vertices (150K triangles). There's plenty I could do to
reduce the size of the mesh by merging coplanar faces, but that would complicate the
UV mapping immensely. Another research project here!

All in all, there's loads of things I could be working on, but they're all hard problems
that are likely to soak up a big chunk of time. Doable, but not critical.


## What next, then?

Well, the goal of the holodeck project is to attempt to make a holodeck until I succeed
or can't make any other progress, so I guess it's time to move on to stage 2: Networking.

## Why networking?

There's 4 key areas to this set of prototypes:

    * A representation of an environment

    * A representation of participants

    * gesture/skeleton recognition for participant pose

    * networking and voice comms to connect two or more participants

The environment is as good as it needs to be (and hopefully someone will provide a tool
that does it much better than mine does). I've looked at Photogrammetry, Phi.3D, Tango
Constructor and a few other capture mechanisms, and I'd like to be working with a tool that
doesn't break the bank yet gives excellent results.

As an example of what I think is state of the art for consumer capture, take a look on
Sketchfab for [GeoVC](https://sketchfab.com/geocv) and
[Paracosm](https://sketchfab.com/models?q=paracosm&sort_by=-likeCount). The best quality
I've seen as a commercial product is [Matterport](https://matterport.com/) but I've not
had a chance to see their resulting meshes, and their tools are not cheap right now.

I'm a *long* way away from this yet, and what I've got is good enough to move on.

I can get voice and networking up and going, but without something there to show presence,
there's not much point - I have a feeling, though, that a sphere with a smiley face on it
will be a good start. It's going to feel worse than AltSpace, but it should have the
added bonus of getting more folks directly engaged.

It's also a great segue into avatars and skeleton capture.

## Next week ...

Networking, Vive dev tests and getting some bigger area scans.







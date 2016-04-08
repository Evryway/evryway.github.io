---
layout: post
title: Dev Blog - How to build a holodeck, week seven
category: DevBlog
tags: DevBlog, weekly
keywords: texture, holodeck, realtime, rift, tango
---

This week, I have been improving mesh capture and playing with my new Oculus Rift.
Videos below!

## TL;DR

[Week seven garage rift](https://youtu.be/kULzWoGQkp0)
{% include youtubep.html id="kULzWoGQkp0" %}

[Week seven garage tango](https://youtu.be/4NyRwMsrDtA)
{% include youtubep.html id="4NyRwMsrDtA" %}

[Week seven walkabout - garage to living room](https://youtu.be/NCtxcZoTrhE)
{% include youtubep.html id="NCtxcZoTrhE" %}

## What have you been doing all this time?

Last week was a well deserved break with the family, but this week I've been lucky
to be able to spend nearly the whole week on improvements to the capture process and
the dynamic atlasing. I also got my kickstarter edition Oculus Rift CV1, which is pretty
darned cool - more on that in a minute.

### Meshing and texturing

The mesh returned from Chisel on the Tango is cut up into grid cubes, and I've spent
a good portion of the week re-doing the way I process these. Because they change under the
hood pretty much constantly, I "freeze" them (take a snapshot of the current state of the
grid cube) before I apply my texture. This ensures that the faces I'm applying the texture
to don't move around or get re-indexed.

Before this week, I had tried a load of variations on different ways to split this work up,
but it turns out that I get the best results if I basically do everything in one pop - freeze
the mesh inside the grid cube, apply the texture, reorganise the atlas. As long as the Tango
is looking directly at the cube, the texture projection should work for all faces that are
actually pointing towards the camera. I can then re-project onto side faces by simply walking
around and re-texturing the faces that are now a better match (better normal orientation or
larger size in the captured texture).

When I re-freeze, I lose all previously applied textures, so I currently have to re-texture
the mesh each time this happens. There's a lot of value in allowing a re-freeze, especially if
Chisel is set up to clear down the mesh segment, which removes lots of nasty artifact faces
and gives a much cleaner scan.

The more I improve this process, the more the limitations of the Chisel meshing become
apparent, such that I'm fighting with it as much as I'm using it. I know there's better ways
to do this, but I'm getting close to being out of time on this prototype, so it's likely I'll
park this (although I'm still not happy with the results).

Texturing is also a problem, and this is down to two issues - the image that I'm taking, and
the orientation of the image that I'm taking. For starters, the camera is currently set
to use auto-exposure, which means the brightness of the image varies constantly. 

![colour mismatch]({{ site.url }}/assets/week7/colour_mismatch.jpg)

You can see in this image, that some of the wall is bright, and some of the wall is dark.
this is because the triangles have been textured using two different frames of the camera,
and the atlas projection process has decided that the bright frame was the best match for most
of the right-side triangles, and the dark frame was the best match for most of the left
side triangles. It's the same surface, but the triangles look obviously mismatched simply
due to the exposure of the image. The same effect is also visible on the brickwork.

There's three key parts to this - the exposure / ISO of the camera, the lighting conditions
of the room, and the quality of the mesh I'm projecting onto. I can (loosely) control the
last two, but as of right now there's no way for me to read the exposure/ISO value of the
texture frame, and there's no way for me to lock the camera so it's at a fixed exposure value.
If I can fix this problem, the quality of the captures will be hugely improved.

[Edward Zhang has a really great post here](http://ed.ilogues.com/2016/02/02/3d-hdr-scene-capture)
where he talks about radiometric calibration of his captured scenes. This really describes
the problems I'm seeing, but unless I get access to the camera settings and/or store
additional metadata when I capture to the atlas, I'm not going to be able to trivially solve
it (if this could ever be called trivial!) - but a solution is going to be critical to
the quality of the environment.


The second major texture issue is that the camera projection simply doesn't match up to
the mesh I'm projecting it on to, and I don't understand why, even after spending a few weeks
bashing my head against it. The colour camera on the Tango device is offset from the device
origin itself (by about 60mm to the right) and it's also at an angle (tilted up and to the
left). I'm reading out the values for these offets/orientations and setting up my
reprojection frustum to match, but - it ain't right. This means that textures are all
badly offset from where they should be, and this introduces all sorts of nasty artifacts.

### Welding

The last main issue I've yet to properly address is the gaps between grid cubes in the
resulting mesh. In the Chisel data, because it's constantly updating, the mesh edges
are very rarely mis-aligned. 

![grid edges]({{ site.url }}/assets/week7/grid_edges.jpg)

in my recent scans, the edges of the grids are painfully obvious, where I've frozen a grid
at time t, and then frozen a neighbour at some later time t+30s. even a millimetre gap
between the edges of the grids is obvious. The solution is to weld the edges - find all
the vertices that should match up, and move them together. I've put a very early pass
of this in place, but (as you can see!) it's not working properly yet. This will make
a huge difference to the quality of the scans if I can get it working.


## Uploading to Sketchfab

I've (last night!) fixed up my COLLADA exporter to resolve a load of issues with my exports,
including bad texture paths, bad scale and more. I tried to import the model directly into
Sketchfab, but it wasn't working. Fortunately, I can export from Unity, so here's one
of the most recent scans.

<iframe width="640" height="480" src="https://sketchfab.com/models/778bd0300f404b93966148e9cccf3650/embed" frameborder="0" allowfullscreen mozallowfullscreen="true" webkitallowfullscreen="true" onmousewheel=""></iframe><p style="font-size: 13px; font-weight: normal; margin: 5px; color: #4A4A4A;">
    <a href="https://sketchfab.com/models/778bd0300f404b93966148e9cccf3650?utm_medium=embed&utm_source=website&utm_campain=share-popup" target="_blank" style="font-weight: bold; color: #1CAAD9;">entry.unity</a>
    by <a href="https://sketchfab.com/timmo.swan?utm_medium=embed&utm_source=website&utm_campain=share-popup" target="_blank" style="font-weight: bold; color: #1CAAD9;">timmo.swan</a>
    on <a href="https://sketchfab.com?utm_medium=embed&utm_source=website&utm_campain=share-popup" target="_blank" style="font-weight: bold; color: #1CAAD9;">Sketchfab</a>
</p>



## Rift CV1

And, on Tuesday, as if deliberately designed to break my focus, the
[Oculus Rift CV1](https://www.oculus.com/en-us/rift/) turned up on my doorstep, so I spent
the majority of the day fiddling with it, playing games and generally getting a feel for
the first ever consumer VR headset.

![Rift]({{ site.url }}/assets/week7/bananulous_rift.jpg)

What's it like, you say? It's excellent. It's NOT perfect - I find the flaring introduced
by the fresnel lenses pretty distracting - but it's an incredibly accomplished bit of
engineering. It WORKS. As the first ever headset with positional tracking that most people
will use, it's good enough for folks to get it.

There's reviews all over the net about it now, so I'll not do a "me too" here. The short
answer to the question "should I buy one?" is best answered by actually trying it out.
If you're anywhere near my in the UK and want to give it a shot, drop me a mail.

The content that comes with it is good, but there's nothing yet that has distracted me
enough to stop working on the holodeck, which is good in a way ;) I haven't bought lots
of games yet, but I will be over the coming weeks. Valkyrie is great, if a bit nausea-inducing.
Elite Dangerous is awesome. Lucky's Tale is really nice. Oculus home is pretty cool.

It all works pretty well with Steam VR too, which is great. That's probably the store
I'll be buying most content from, especially as my Vive is due to arrive next week.

If you check the videos up top, there's one where I show the limits of walking around in
the Garage capture - the cable isn't terribly long, so room-scale VR with the rift is
definitely not as viable as the Vive (or untethered). I think this is going to become
very important to people over the next couple of years.

The other main issue I have is my graphics card - it's simply not powerful enough, and
I'm a bit wary of dropping 500+ quid on a new card when the next-generation cards are
due out in a month or two (hopefully!). This might change when the Vive arrives, but for
now I'm probably going to hold off.


## Help!

I'm having big problems in the following three areas:

1. Getting the Tango's camera aligned correctly in the world so that projection
through the camera image onto the world mesh lines up properly. If you are good
at math and fancy talking through what I've done, I'd love the help.

2. Lighting. I'm no artist, as most of the folks who've worked with me can attest,
but even I can see that the exposure mismatches in the captured textures are throwing
everything off. because I'm not retaining the original image, it's going to be very
tricky to do radiometric calibration. I don't appear to be able to lock the camera
exposure/iso settings in Unity, so any bright ideas of how to address this would be
greatfully appreciated.

3. Getting stuck on one thing. The environment capture is a really interesting problem,
but it's not a holodeck. I've spent over three weeks on it now, and it's "working" but
it doesn't necessarily look any better than the scans coming from the Tango Constructor app,
which is really disappointing me. Ho hum. Not sure how folks can help on this one, but
it's definitely a downer.


## Next week ...

Portals! (and maybe some improvements to the mesh capture process).

I'm going to start exploring what it's like to move between virtual real-world spaces
in the real world, both at small room-scale and at house scale. I'm pretty sure there
will be a few accidents along the way.








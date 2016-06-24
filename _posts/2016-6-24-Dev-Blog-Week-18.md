---
layout: post
title: How to build a holodeck, week 18
category: DevBlog
tags: DevBlog, weekly
keywords: avatar, mesh, skinning, rigging
---

This week, I've been putting my [R200 scanner](http://click.intel.com/intel-realsense-developer-kit-r200.html)
to use capturing human body poses, and attempting to get them to animate. Videos and stuff below, read on.

## Scanning people

It's been really interesting looking at the results I get from scanning people,
and going through the actual mechanics of taking a scan.

I've been trying to get a few different packages working, but Reconstructme doesn't
want to play ball with the R200 sensor, and the RealSense example scanner tool isn't
terribly usable.

This means the best (and pretty much only!) tool I've had any decent results with so
far is [Itseez](http://itseez3d.com/). 

The results from my attempts to scan vary from hideously deformed to potentially usable.

Here's some examples of *good* scans (I've left the bad ones on the cutting room floor!)

#### Nic Head

<iframe width="640" height="480" src="https://sketchfab.com/models/2248352c5a004ad08acb833aca851fa3/embed" frameborder="0" allowfullscreen mozallowfullscreen="true" webkitallowfullscreen="true" onmousewheel=""></iframe><p style="font-size: 13px; font-weight: normal; margin: 5px; color: #4A4A4A;">
    <a href="https://sketchfab.com/models/2248352c5a004ad08acb833aca851fa3?utm_medium=embed&utm_source=website&utm_campain=share-popup" target="_blank" style="font-weight: bold; color: #1CAAD9;">Nic&#39;s Head</a>
    by <a href="https://sketchfab.com/timmo.swan?utm_medium=embed&utm_source=website&utm_campain=share-popup" target="_blank" style="font-weight: bold; color: #1CAAD9;">timmo.swan</a>
    on <a href="https://sketchfab.com?utm_medium=embed&utm_source=website&utm_campain=share-popup" target="_blank" style="font-weight: bold; color: #1CAAD9;">Sketchfab</a>
</p>

Not a bad scan, this was about the fourth or fifth attempt.


#### Tim full body

<iframe width="640" height="480" src="https://sketchfab.com/models/7e5e74c2c2244033a9dbefa2296fa11a/embed" frameborder="0" allowfullscreen mozallowfullscreen="true" webkitallowfullscreen="true" onmousewheel=""></iframe><p style="font-size: 13px; font-weight: normal; margin: 5px; color: #4A4A4A;">
    <a href="https://sketchfab.com/models/7e5e74c2c2244033a9dbefa2296fa11a?utm_medium=embed&utm_source=website&utm_campain=share-popup" target="_blank" style="font-weight: bold; color: #1CAAD9;">Tim full body</a>
    by <a href="https://sketchfab.com/timmo.swan?utm_medium=embed&utm_source=website&utm_campain=share-popup" target="_blank" style="font-weight: bold; color: #1CAAD9;">timmo.swan</a>
    on <a href="https://sketchfab.com?utm_medium=embed&utm_source=website&utm_campain=share-popup" target="_blank" style="font-weight: bold; color: #1CAAD9;">Sketchfab</a>
</p>

Here, you can see that the model has been captured leaning back - this is because
the person holding the scanner was a bit shorter than average! This was at least the fifth
attempt, possibly more.

## The mechanics of scanning

To accurately capture an object, to the best ability of the scanner, a lot of things need to
be done correctly. Lighting is important, and the lighting in my garage *stinks*. I'm going to have
to get some nice bright LEDs and some diffuser material, maybe set up a lighting box like you
see at professional photography studios. The texture quality coming back from the R200 colour camera
looks absymal, but hopefully I can improve that with better lighting.

Actually capturing the surface means the scanner needs to be around 1m away from the points you're trying
to capture. This means you need to move the scanner around to cover the full body. The process of
moving the scanner around is troublesome in itself, as I needed to order a 3m USB lead (the one
that came with the scanner was about 20cm long, thanks Intel!). Even a 3 metre lead isn't long enough,
so I've got some 5 metre leads on order. While scanning, you need to be able
to look at the screen for reference, to ensure you're "locked on" - if you lose lock on the object,
you've got to try and get back to a known position, which is pretty tricky sometimes. With the way
the camera is set up in the garage, it's hard to scan and see the sceen at the same time.

Walking around a person to capture them is very hard work - not only do you change the lighting
by moving around them, but it's really hard work trying to keep the scan stable, the camera pointing
in the right direction, etc. The whole process is pretty fraught and easy to break - I reckon I tried
about 10 times to get Nic's head before we figured out the correct scanning distance, how fast to move
the sensor, etc. The orientation you start at seems to matter (you need to be horizontal to start
capturing the initial face pose, otherwise you'll get a leaned back model).

It's also hard work for the person being scanned, as they need to hold the pose without moving for
the entire scan duration. It might sound silly, but holding anything close to a T pose for a few minutes
while looking straight ahead is quite tiring! It's proving very tricky to get accurate hands and
arms because of this - I might have to look into some sort of device to help hold the person
in a T pose! I tried a broom handle, but it didn't work.

## Turntables

Because of the issues with walking around,
a better solution is to have the subject rotate, and the 30 quid I've spent so far on wood and lazy
susan bearings was a very good investment. After looking around, the most reasonable turntable I can
find that is motorized and remote controlled [(the Arqspin 24)](https://arqspin.com/product/hardware/) is around 300 quid,
and the first one I found was over 1200. I doubt I'll get something as pretty, but hopefully with
some help I can knock something together that does the job for under 100 GBP.

The best three scans have been done by having the person
stand on the turntable plate, moving the camera up and down, rotating them around a bit, scanning
up and down, rinse and repeat. This gives more consistent lighting and means the scanning process
is a lot easier to manage.

![DIY Turntable](/assets/week18/turntable.jpg)

Having to rotate the turntable by hand is a pain in the rear, so I've got a motor on order, I think
a bit of rasp-pi magic is going to be required to get a nice controllable spin. This could be a side
project in itself, I've got a few nice ideas for how to get the turntable motoring. I'm also thinking
of building some sort of rig to hold the camera itself, to make it much easier to move it
smoothly up and down, in and out. More woodwork might be on the cards ...

You can see in this scan, the turntable is visible, and the scan quality is pretty decent - the
floor plane lines up nicely, for example.

<iframe width="640" height="480" src="https://sketchfab.com/models/f59c1ebc4de74741a137bcc56464c521/embed" frameborder="0" allowfullscreen mozallowfullscreen="true" webkitallowfullscreen="true" onmousewheel=""></iframe><p style="font-size: 13px; font-weight: normal; margin: 5px; color: #4A4A4A;">
    <a href="https://sketchfab.com/models/f59c1ebc4de74741a137bcc56464c521?utm_medium=embed&utm_source=website&utm_campain=share-popup" target="_blank" style="font-weight: bold; color: #1CAAD9;">Nic Full Body</a>
    by <a href="https://sketchfab.com/timmo.swan?utm_medium=embed&utm_source=website&utm_campain=share-popup" target="_blank" style="font-weight: bold; color: #1CAAD9;">timmo.swan</a>
    on <a href="https://sketchfab.com?utm_medium=embed&utm_source=website&utm_campain=share-popup" target="_blank" style="font-weight: bold; color: #1CAAD9;">Sketchfab</a>
</p>

The main problem with this scan (which is probably the highest visual quality) is that the legs
are effectively welded together. I don't have the skills to fix the meshes up, and I'd like this
process to be as simple as possible, so I think for future scans I'll have to go with a wide
legged stance. I'm not sure how well that will rig, but that's the next step!

I think it's going to take a LOT more practice to get meshes that are really usable for some form
of realistic human avatar, both in terms of mesh fidelity, texture quality and pose quality.

## Rigging and animating

I've tried to use [Adobe (previously Mixamo) Fuse](http://www.adobe.com/uk/products/fuse.html) but I get
repeated failures trying to import the meshes I've made from Itseez. The first error was that the mesh
was too complex. I ran a decimate in Blender to bring the number of verts down, and then ran into
another error relating to how the model UVs are set up. This is really sad, as I was hoping to be able
to just "make it work" in Fuse. ah well.

My next attempt was to use [Rigify in Blender](http://docs.unity3d.com/Manual/BlenderAndRigify.html).

I'm sure this is an excellent tool if you know
what you're doing, which I most definitely do not. I followed a variety of tutorials and videos,
such as this [video showing how to do rigging and skinning](https://www.youtube.com/watch?v=PTmVLD-1ilQ)
- I think I've managed to set up the armature to match my scanned mesh, but the automatic weight
process simply fails regardless of what I've tried (I've positioned all the bones as well as I can,
removed bones, all sorts of things) and when I try to manually paint the weights, I can't get anything
to export properly to Unity.

I've been thinking about how to automate this process (rigging and skinning) and then, serendipitously,
I stumbled on the [Mixamo auto-rigger](https://www.mixamo.com/auto-rigger).

this thing is MAGIC. it does exactly what I had hoped to do - you tell it about some of the key
points in your mesh, press process, and a few minutes later you get an FBX out the other end that
is properly set up for Unity.


## Putting the mesh into the holodeck

As I'd not finished skinning the mesh, I'd been itching to see what my scan avatar looks like in the
portals prototype. I spent a chunk of time getting the prefab set up so all "actors" in the world are
represented by my scan. It's pretty damn spooky.

[Week 18 - some form of human](https://youtu.be/CczOmS02Tt0)
{% include youtubep.html id="CczOmS02Tt0" %}

A bit of messing about with the Kinect Examples package, and I've got myself walking around in a
scene in Unity. Good lord, that looks even MORE spooky.

[Week 18 - Kinect test](https://youtu.be/6TaK39N6MNk)
{% include youtubep.html id="6TaK39N6MNk" %}


## Help!

If you've got experience rigging in Blender, or an alternative workflow that's both cheap (ideally free) and
works, please drop me a mail and tell me how to do this properly! I don't have access to Maya or Max,
which unfortunately rules out a whole host of good tools for this.


## Next week ...

I may spend some time looking at getting the Kinect tools into the portal demo, and get this stuff
working over the network. I think at that point, we've got all the ingedients for a very ropey telepartation demo.









---
layout: post
title: Dev Blog - How to build a holodeck, week three
category: DevBlog
tags: DevBlog, weekly
keywords: dev blog, how to build a holodeck
---

This week has been an exploration of walking around house-scale VR using Project Tango. It's raised more questions than
answers, and this is the point where the real hard work begins. Let's have a quick intro to 3D rendering, cameras and UI, and then get
into the guts of environments.

## TL;DR

[Week three, day 1 - my garage in the real world](https://youtu.be/4pIDbyjLHUE)
{% include youtubep.html id="4pIDbyjLHUE" %}

[Week three, day 2 - my garage in the holodeck](https://youtu.be/ZfFzvU_aqYc)
{% include youtubep.html id="ZfFzvU_aqYc" %}

[Week three - housewalk ](https://youtu.be/5OdHTkSMynE)
{% include youtubep.html id="5OdHTkSMynE" %}


## What am I looking at, exactly?

Ah, an excellent question. "What am I looking at?" and it's associated sister question, "How do my eyes work?". As far as 
I understand it (and I'm a long way from expert, here), this is broken down into:

### Photon transport

Something, somewhere in the universe, produces [photons](https://en.wikipedia.org/wiki/Photon). They then bounce around, interacting or reflecting with or through materials,
until such point as they enter your eye. Photons have to be one of the coolest concepts ever, with Einstein putting a lot
of the initial grunt work into understanding and explaining just how light works. My understanding of the actual physics
of light is very basic, and I can sum it up like this - photons are particles that are massless when they are not moving,
and they have a habit of moving at the [speed of light](https://en.wikipedia.org/wiki/Speed_of_light), which is very fast indeed.
We appear to live in a place we call the Universe, which is [pretty big](http://hitchhikersguidequotes.tumblr.com/post/13945214509/space-is-big-really-big-you-just-wont-believe), so even though light moves super fast, it takes a long time to get from the Sun (which produces
a lot of photons, enough for you to feel them when you stand in sunlight) - about 8 minutes.

### Our eyes

After they've bounced around all over the place, the photons end up going into [our eye](https://en.wikipedia.org/wiki/Human_eye).
At this point, they will have a specific energy, and our eye sends signals to our brain based on the energy the
photon carries, which our brain then translates into seeing a specific colour. 

For the purposes of our holodeck experiments, we need to construct some photons and then chuck them into our eyes. We do this
using a computer to synthesise a view of our virtual world, which we then push to a display device (the screens in your Rift, Vive,
or in my current case, the project Tango tablet screen). The screen generates photons, which are then guided by some lenses
and arrive at our retina, which our brains then interpret as a view into that virtual world.

Super-cool!

## Cameras

our eyes are incredibly complex biological systems, and modelling them properly isn't something I have any time to do - so we're
going to stick with the canonical representation that just about every game engine uses, which is a perfect
[pinhole camera](https://en.wikipedia.org/wiki/Pinhole_camera) as a model of our (considerably more complex) pupil, lenses and retina
system.

Normally [first-person games](https://en.wikipedia.org/wiki/First-person_(video_games)) use a single camera which is set up so that it's centred
in the middle of your screen, whatever that screen may be. This means that you "look out" into the world as though you had a single
eye in the centre of your head, or close to. It also means that, regardless of the size of your screen, the camera is always
centred on the screen centre for the [viewing frustum](https://en.wikipedia.org/wiki/Viewing_frustum) - the camera view axis
is orthogonal to, and travels through the centre of, the near and far [clip planes](https://en.wikipedia.org/wiki/Clipping_(computer_graphics)).

With VR, you need a camera to represent the view each eye sees, and you also have to think about how you translate the camera
view so it matches up with your actual eyeballs. Different people have different sized faces, meaning the [distance between your
pupils](https://en.wikipedia.org/wiki/Interpupillary_distance), or IPD, varies per person. The Tango demos give you a little control
over this, and cardboard is similar. One thing that the Tango demos do is make the view that you see on the physical tango screen use
orthogonal view frustums as described above. this has an immediate side effect of giving you black bars on the side of the screen, because
the tango screen is about 150mm across, yet the average IPD is about 62-65mm. this means your eyes are about 32mm either side of the
centre line, so you end up with a left eye view of 64mm, a right eye view of 64mm, and dead space in the remaining 25-30mm. I want to
have the entire screen being used (peripheral vision is really important, and the wider the
[field of view](https://en.wikipedia.org/wiki/Field_of_view_in_video_games) is, the better. In photography
this is often referred to as [Angle of View](https://en.wikipedia.org/wiki/Angle_of_view).
One of the concerns people have with the current Microsoft Hololens is the relatively small field of view, and both the Rift and the
Vive are striving to give FOV values over 100 degrees.

I've hacked in some non-orthogonal rendering matrices into my two cameras which lets me use
[off-axis view vectors](http://paulbourke.net/papers/HET409_2004/het409.pdf), giving full
screen coverage. That means no black bars - bonus. One thing I've not done is handle the distortion that the lenses bring,
which all of the existing SDKs and demos for all the other platforms do much better than my current demos, so (outside the centre
of the FOV) everything in my world looks wierdly distorted. I'll hopefully be fixing this soon!

I've also not got any sort of vignetting around the screen views yet, which means you get a really sharp divide between the left
and right eye views - this is pretty jarring initially, but you get used to it. I'll be experimenting with different vignettes
at some point, but it's not a big priority right now.


## Geometry and materials

The screen in most of our display devices is flat, which means when we want to display something that's not flat, we need
to figure out how to draw something on that screen that appears to have depth (distance away from the display screen). We also
need to capture the properties of what we're looking at, which we'll normally call "materials" or "surface properties".
[The basics are pretty simple to understand](http://people.csail.mit.edu/fredo/Depiction/1_Introduction/reviewGraphics.pdf) but
the details of how this works is a very deep research field - if you're interested in the state of the art, then you should be
looking at the output of [SIGGRAPH](http://www.siggraph.org/), where the majority of the cutting edge of research into rendering
and visualisation techniques are showcased.

The current prototype is using Unity's rendering system to convert our mathematical representation of the world into something
that we can observe on a display scene. It's a very capable rendering system that handles the geometry, shaders and materials
well enough for us to observe close-to-realistic representations of real world objects. As you can see from the example videos,
things currently look pretty abysmal, but that's not an issue with the rendering system itself, it's an issue with the information
that I'm providing to it - my mathematical representation of my house doesn't contain nearly enough information to give an
accurate picture of what we're wanting to see.

The initial results I'm getting back from the Tango sensors (which give back a [depth point cloud](https://en.wikipedia.org/wiki/Point_cloud)
at 5Hz and a 2D picture from the camera at 30Hz) are being turned into a mesh using Google's [Chisel](http://www.roboticsproceedings.org/rss11/p40.pdf)
process. This is giving me a mesh that's aliased into 50mm cubes, and each mesh vertex holds a colour value which is taken
from the picture created by the camera which matches up to the depth cloud at the same point in time.

Doing this kind of processing realtime was science fiction until some point this decade, so being able to do it at all
is basically blowing my tiny mind. The fact I can do it with 300 quid's worth of mobile hardware is simply astounding.

Still, the results are currently far from what I want from the holodeck, and it's probable that the hardware limitations
will mean the best I can possibly manage with the Tango alone won't be good enough. There's plenty of alternatives out there
right now (including Kinect and the [Occipital Structure Sensor](http://structure.io/) ) which provide better fidelity in
the distance field capture (more accurate scanning at a higher refresh rate, according to the numbers I've seen).

Getting a higher quality surface representation will require a combination of more mesh complexity and more colour/material
information in the mesh faces. The simplest way to go about this is to increase the point cloud density, but that's not going
to scale terribly well for rendering performance and it's going to reach limits of the accuracy of the Tango's point cloud data
at some point (probably once I hit around 10mm voxel aliasing).

## Texturing

The next, harder-to-do but obvious thing is to capture texture data from the camera and use this directly on the surface, instead
of simply colouring the vertices on the mesh and having each mesh face blend between those colours.

Unfortunately it doesn't appear that the Chisel implementation currently shipping with Tango does this natively, which means
writing some additional processing to get this working. Currently, I've got this pegged as my highest priority for the next
couple of weeks, and it's not going to be a trivial process to do in any kind of performant way. Still, let's take a bash at it!










## Help!


## Next week ...






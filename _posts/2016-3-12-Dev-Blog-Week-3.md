---
layout: post
title: Dev Blog - How to build a holodeck, week three
category: DevBlog
tags: DevBlog, weekly
keywords: dev blog, how to build a holodeck
---

This week has been an exploration of walking around house-scale VR using Project Tango. It's raised more questions than
answers, and this is the point where the real hard work begins. I'll briefly cover where I'm at with Cameras, UI, and
the realtime environment capture work I've done so far.
 
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

Something, somewhere in the universe, produces [photons](https://en.wikipedia.org/wiki/Photon). They then bounce around,
interacting or reflecting with or through materials,
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
which all of the existing SDKs and demos for all the other platforms fix with shaders, so (outside the centre
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
the distance field capture (more accurate scanning at a higher refresh rate and at a higher distance, according to the numbers I've seen).

Getting a higher quality surface representation will require a combination of more mesh complexity and more colour/material
information in the mesh faces. The simplest way to go about this is to increase the point cloud density, but that's not going
to scale terribly well for rendering performance and it's going to reach limits of the accuracy of the Tango's point cloud data
at some point (probably once I hit around 10mm voxel aliasing). There's a 
[whole](https://en.wikipedia.org/wiki/Marching_cubes)
[host of](http://www1.cse.wustl.edu/~taoju/research/dualContour.pdf) 
[alternative](http://www.sci.utah.edu/~shachar/Publications/MLSMesh.pdf)
[methods of](https://mediatech.aalto.fi/~samuli/publications/laine2010tr1_paper.pdf) 
[turning](http://graphics.csie.ntu.edu.tw/CMS/)
[the point cloud](https://github.com/personalrobotics/OpenChisel)
into a mesh, some of which require additional information that isn't trivial to abstract from a Tango scan. I'm going to look
at spending a bit of time going through OpenChisel to try and fully understand what's going on under the hood - this is undoubtedly
the very first of a long line of rabbit holes.

## Texturing

The next, harder-to-do but obvious thing is to capture texture data from the camera and use this directly on the surface, instead
of simply colouring the vertices on the mesh and having each mesh face blend between those colours.

Unfortunately it doesn't appear that the Chisel implementation currently shipping with Tango does this natively, which means
writing some additional processing to get this working. Currently, I've got this pegged as my highest priority for the next
couple of weeks, and it's not going to be a trivial process to do in any kind of performant way. Still, let's take a bash at it!

I'll need to do some form of UV mapping on the generated mesh, some form of texture capture and compression (ideally dynamically
scaling the captured texture based on how close you get when you capture it), some form of atlasing of the captured textures for
performance (otherwise I'll have an awful lot of materials and the resulting draw call cost).

## UI

UI is the bane of my life, and the area that sucked up a massive amount of time in a lot of my most recent game projects. I'm currently
using Unity's world-space UI system, and while it's a very capable system, my designer skills are atrocious and I'm not going to
devote a large amount of time to getting pretty menus working (as you can no-doubt see on the videos). Functional is going to have
to be good enough for the short term - maybe I can persuade some of my more artistic friends to help out with button styles and
transitions!

I'm currently creating another two cameras so that I can project the UI on top of the main scene after doing a depth clear, which
ensures that the UI is not occluded by geometry in the world scene. This makes the UI usable at all times, but brings with it
all sort of perceptual confusion when you're looking at menus that sit about a metre away, but there's something closer in the virtual
world that they cover. I've really done very little research into the best place to be putting this stuff for a most relaxing experience,
so if you, dear reader, have links to share on best practice here, I'd love to see them. I'm sure this is an area that most
teams are starting to get to grips with. From reading through some of the Unity and UE4 best practice docs, it looks like using shaders
on the UI elements is the normal way to handle the depth clear, presumably for performance reasons - I have no idea yet how
expensive it is to have another set of two cameras just to handle the UI layer.

It's been said that [the best UI is no UI](http://www.nointerface.com/book/). I'm kinda leaning in that direction, but there
is an enormous amount of effort to get to a natural user interface in VR. Speech recognition and gesture recognition are key parts
to this, and I'm also trying my hardest to make the UI purely gesture-based right now (so no need to carry around a controller).
Getting some traction on speech and hand/pose recognition is on my list, but it's waaaay down there right now. If I stall on the
textured mesh, I'll probably move it up the list.

## Help!

This week - where to begin? The more I dig into making this work, the more I realise I need to learn, and the bigger the
list of things to do becomes. Hit me up with VR UI research links if you've got them, if you have export code from UI that takes
runtime meshes and spits out a collada or FBX file, that would also be most excellent. 


## Next week ...

Texturing the captured mesh seems like a good thing to do - nearly everyone is underwhelmed by the quality of the resulting
environment. You're in something, but it's not the real world just yet.

I'm also super-intrigued by getting a handle on locomotion between spaces without leaving the safe zone, as this is going
to be critical to making the experience work, and my various tests this week have nearly all resulted in recognising just
how little space the average house has to work with this kind of experience. Unless we all get VR rooms, we're going to be
stuck in a 2m*2m motion constraint. After trying unconstrained house-scale movement, I believe in the core of my bones that
this is sucky. Totally sucky.

I've got a couple of ideas for portal / teleportation mechanisms that I think would be pretty interesting to try out.

I'm also interested to see if I can create a super-high quality environment using the existing tools at my disposal - I've tried
some photogrammetry capture using VisualSFM and Agisoft Photoscan, and I'm not getting great results. I know it's possible
to do this to a really high fidelity, but I'm darned if I can manage it myself yet.

Obviously, I'm not going to be able to do all three of these, and if I get one of them done next week I'll be happy. If you
have a preference for any particular area, tell me - feedback is really useful ;)













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

## Geometry and materials

The screen in most of our display devices is flat, which means when we want to display something that's not flat, we need
to figure out how to draw something on that screen that appears to have depth (distance away from the display screen). We also
need to capture the properties of what we're looking at, which we'll normally call "materials" or "surface properties".
[The basics are pretty simple to understand](http://people.csail.mit.edu/fredo/Depiction/1_Introduction/reviewGraphics.pdf) but
the details of how this works is a very deep research field - if you're interested in the state of the art, then you should be
looking at the output of [SIGGRAPH](http://www.siggraph.org/), where the majority of the cutting edge of research into rendering
and visualisation techniques occur.

The current prototype is using Unity's rendering system to convert our mathematical representation of the world into something
that we can observe on a display scene. It's a very capable rendering system that handles the geometry, shaders and materials
well enough for us to observe close-to-realistic representations of real world objects. As you can see from the example videos,
things currently look pretty abysmal, but that's not an issue with the rendering system itself, it's an issue with the information
that I'm providing to it - my mathematical representation of my house doesn't contain nearly enough information to give an
accurate picture of what we're wanting to see.

The initial results I'm getting back from the Tango sensors (which give back a [depth point cloud](https://en.wikipedia.org/wiki/Point_cloud)
at 5Hz and a 2D picture from the camera at 30Hz) are being turned into a mesh using Google's [Chisel](http://www.roboticsproceedings.org/rss11/p40.pdf)
process. This is giving me a mesh that's aliased into 50mm squares, and each mesh vertex holds a colour value which is taken
from the picture created by the camera which matches up to the depth cloud at the same point in time.

Doing this kind of processing realtime was science fiction until some point this decade, so being able to do it





## Help!


## Next week ...






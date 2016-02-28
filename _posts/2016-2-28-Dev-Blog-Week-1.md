---
layout: post
title: Dev Blog: How to build a holodeck, week one
category: DevBlog
tags: DevBlog, weekly
---
# Dev Blog: week one - Building a holodeck

Welcome to my "How to build a holodeck - follow along at home with sticky tape and scissors" dev blog. This is week one, which means we'll be figuring out how to do this (the process) as well as how to do this (the content) as we go. I’m hoping to make this a regular thing - and that really depends on whether there’s enough readers to make it worthwhile. If you like this, share it and tell me!

## TL;DR

[Week one on-device](https://youtu.be/lrL1TOYCkwk)
[Week one in the real world](https://youtu.be/HlTIzz9toiU)


I'm [Tim](https://www.linkedin.com/in/tim-swan-14b1b), and my goal is to build something functionally equivalent to the Star Trek holodeck, constrained by today's obvious technology limitations. That means (as far as I'm aware) no forcefields, no matter projection, no three dimensional holograms. If we take out all the science fiction, what hardware is actually available right now for us to use?


## Hardware

We'll need a selection of things to get this working. The first is some form of *display*. The second is some form of *input*. The third is some form of *motion*. That will get us up to the basics. Let's look at our options.

### Displays

You're most likely staring at this on a screen - a 2D display. While systems like the [CAVE](https://en.wikipedia.org/wiki/Cave_automatic_virtual_environment) use 2D displays and are wicked cool, they take a lot of hardware and effort to set up and they’re not terribly portable.

There’s a selection of [HMDs](https://en.wikipedia.org/wiki/Head-mounted_display) (Head Mounted Displays) on the market, and have been for many years, but recently there’s a couple of serious contenders that are either on the market or just about to be released. Anyone who’s excited about VR will most likely be aware of them:


#### [Oculus Rift](https://www.oculus.com/en-us/rift/)

This is the entry from Oculus, recently purchased by Facebook. There’s a lot of money behind this. I’ve got a developer kit (both a DK1 and a DK2) and most of my prototyping up to this point has been using this hardware. It’s awesome. The consumer version should be arriving some time in April. The Touch input system isn’t quite ready for consumers yet, and that’s potentially a critical issue we’ll see crop up in the next few months.

#### [HTC/Valve Vive](http://www.htcvive.com/uk/)

This is the entry from Valve, partnered with HTC. Valve’s recent VR research really pushed global understanding of working with VR. I was lucky enough see some of the GDC talks in 2013 by Michael Abrash and Joe Ludwig which went really deep on the issues with hardware at that time (display resolution, persistence, tracking latency and a whole host of other known problems). Off the back of this research, their Vive (pronounced Vy-ve) headset and Lighthouse tracking solution (combined with a nice long cable) give the Vive the definite edge for how far you can move from your computer.

#### [Razer OSVR](http://www.razerzone.com/osvr-hacker-dev-kit)

I love the idea of open standards and multiple manufacturers creating hardware to those standards. Razer’s OSVR Hacker Dev Kit is probably about the best available in that space so far, but I’m sure there will be lots of improvements and alternatives in the coming months.

All of these headsets provide incredible experiences that you’ve never felt before. If you haven’t had a chance to try them out yet, do it. Grab Elite:Dangerous and go fly a spaceship.

They all share one common problem, though - they are tethered to your computer. While both Rift and Vive are touting themselves as “room space” solutions, they don’t lend themselves to freely walking around - which is what I want from a holodeck! I’ve done a variety of tests with different laptops and tracking systems like feeding [Kinect](https://dev.windows.com/en-us/kinect/develop) data over the network to a laptop in a backpack hooked up to my DK2, and that gives you mobility at the cost of a much more expensive, cumbersome solution. It works - it’s cool - but it’s not particularly consumer friendly.

So, let’s talk about Mobile HMDs.


#### [GearVR](http://www.samsung.com/global/galaxy/wearables/gear-vr/)

GearVR is probably the best solution out there right now in terms of consumer friendlyness. You pop in a best-gen Samsung phone, and you’ve got yourself a mobile VR display. This is great - right up to the point you decide to move. Because they have no in-built tracking right now, the best you get is *orientation tracking* (i.e. where your head is pointing) but no *motion tracking* (i.e. where your head actually is). That means, unless you tie it with some other positional tracking system, you’re stuck in a chair. Not particularly holodeck.


#### [Google Cardboard](https://www.google.com/get/cardboard/)

Cardboard is the cheap-and-cheerful solution which works across a huge range of devices, turning a phone or tablet that you already own into a VR viewer. It has the same issues that GearVR brings to the table, and more besides (the display quality and headset quality are pretty cheap). The main advantage is that you can build one from a cereal packet if you so desire. Better than nothing at all, but not remotely on par with the best experiences you’ll get using a Rift or a Vive.

Where does that leave us?

What I want is a mobile, positional-tracking-capable, orientation-tracking-capable VR headset. Does such a thing exist?

#### [Project Tango](https://www.google.com/atap/project-tango/)

This certainly isn’t a consumer-friendly form factor right now - but that’s going to change this year for sure. And the template device for how it looks is most likely going to use some of the technology from [Project Tango] I’ve got a few of the developer tablets, and they’re simply incredible pieces of kit. Paired with a headset like the [Durovis Dive 7](https://www.durovis.com/product.html?id=5), you’ve got something that’s like Cardboard but the device also has built-in positional tracking.

Is it good enough? For getting this project up and running - hell yes!

I’m 100% certain that this year will bring great leaps in the mobile space, massive improvements and competitors in the desktop space, and (probably most importantly for everyone) a growing consumer base and consumer awareness of what VR and AR can do, and all of the devices above will be critical to that.

### Input

What I really want is speech and gesture recognition while I wander around in my holodeck - no devices in my hands, no special tags or trackers or special shoes. I’m kind-of-ok about having cameras watching the environment and the actors, as I think that’s going to be the best way to get this working right now.

Feeding in input is simplest with some form of joypad or remote or wand. Both Oculus and HTC have hardware that’s nearly ready for use, with the Vive controllers probably being the best example out there for most folks. At least this gets you to the point of tracking your hand motions and letting you press buttons to express intent. It’s not what I really want, but it’s a great start.

[Leap Motion](https://developer.leapmotion.com/orion) is probably the best example of hand and gesture tracking without needing to be holding a device. They have an Android SDK available at a very early preview state, so that’s something that’s definitely worth watching. On PC, it’s an obvious solution that’s already in place in a lot of games and VR meeting spaces.

Obviously, a bluetooth controller paired up with any machine (PC, tablet) is a viable, if a bit 20th-century, input mechanism, so in the absence of getting speech and gesture recognition working (that’ll come soon, I promise!) I’ve got myself a cheapo DroidBox controller for building the first prototypes.

### Motion

Moving around is a core part of what people do (unless you’re fat and lazy like me!) Our brains are very much hard-wired to expect certain combinations of sensory stimuli. If you move in VR but don’t make the corresponding motion in the real world, your brain is constantly telling you that you must be being poisoned and the best solution to that is to vomit. Anyone who’s tried a VR rollercoaster will have experienced this, but just about every seated VR experience where you move around is going to introduce this effect. You can learn to deal with it, but that’s a barrier that you have to push through.

For our holodeck, what we want is motion in the real world space that matches the virtual world space one-to-one. Vive’s room-scale VR experiences are probably the closest most people will have come to this. [Here’s an example](https://www.youtube.com/watch?v=VD4UlShicgY) of taking that to about as extreme as it gets, from the developers of Hover Junkers. You can see the absolute joy on their faces when they properly get sucked into the experience - as well as all the various pitfalls of doing this, like bashing into walls, falling off things, and having dangling cables everywhere. This is about as good as it gets, right now - at least, until we get this thing built!

The other alternative would be to use an omni-directional treadmill, or something like the [Virtuix Omni](http://www.virtuix.com/). I’ve not tried it myself, but it’s possible this will be the way people do this in the future. I’m not sure yet.

For now, I think (for my aims) the Project Tango device is the best solution given all the available constraints - it runs at a pretty decent framerate, it tracks pretty accurately, there’s no cable and it’s super-easy to develop for.

## Software

I’ll be trying to make this as quickly and as dirtily as possible. That means [Unity3D](http://unity3d.com/), with [Visual Studio Community](https://www.visualstudio.com/en-us/products/visual-studio-community-vs.aspx) and whatever plugins I can get my hands on that mean I don’t have to write things myself.

Tango comes with a [Unity plugin](https://developers.google.com/project-tango/downloads), so that’s a no-brainer. I’ve tried to get [Cardboard](https://developers.google.com/cardboard/unity/) working gracefully with Tango, but there’s issues with device orientation that I didn’t want to fight with, so for now I’ve written my own dual-camera rendering. You could also grab the [Durovis Dive SDK](https://www.durovis.com/sdk.html) for a good example of off-axis camera projections.

[Leap Motion Unity SDK](https://developer.leapmotion.com/unity) is another one that’s on the list. Getting the Kinect up and running in Unity is do-able, but a little bit trickier, so for now we’ll leave that to come back to later.

From my previous experience writing games, I know that a good codebase is a happy codebase, and that means a few design paradigms up front - DI, state machines driving the core logic, asset pipelines, Continuous integration builds, all that good stuff. Because I’m writing this from scratch, I’ll be using some free and paid-for content off the Unity Asset store. I’ve started with [StrangeIoC](https://www.assetstore.unity3d.com/en/#!/content/9267) to handle my DI requirements and [Rewired](https://www.assetstore.unity3d.com/en/#!/content/21676) to handle my joystick input requirements. I’ve written both of these types of systems from scratch before, and I simply haven’t got the time or inclination to do that again! We’ll be doing a lot of standing on the shoulders of giants during this development process.

I’ll be covering the software I’m actually writing in much more detail in future blog posts - if there’s any area you’d like to see covered specifically, [drop me a mail](mailto:hi@evryway.com).

## Progress so far

So far, I’ve got a project set up that allows me to do the following things:
- Track the headset inside an area
- Gaze-tracking activation of unity menu buttons
- some very basic Unity UI menus for interacting with the project
- loading an Area Definition File for better tracking accuracy
- Covered my garage in sticky tape so I know where I am in the real world
- a VERY long list of things to do.

See up top for links to videos of progress so far. 

Yes, this looks rubbish. I’m not much of an artist or designer, so the aesthetics of this prototype won’t be particularly beautiful. Let’s see if that matters!


## Help!

This week, I really need some lessons on how to best create and edit videos on a PC (ideally with free software). If you’ve got any advice, please share!






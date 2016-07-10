---
layout: post
title: How to build a holodeck, week 20
category: DevBlog
tags: DevBlog, weekly
keywords: slow week
---

Not much to report this week. I've been cleaning up the codebase
in preparation for a couple of new tools and a new approach for
projecting entities in the world.

## Kinect tracking

I've spent another couple of days working on the Kinect tracking to drive
avatars, and I'm just not getting the kind of results that justify putting
a lot more time into it, at least for now. It's always disappointing hitting
a roadblock, but it's normally a good sign to shelve things for a while, so
I'm going to chalk this one up as "too hard" and move on to a couple of new
experiments.

## Texture projection

One of the really cool demos for telepresence I saw a couple of years
back is this one:

{% include youtubep.html id="Ghgbycqb92c" %}

There's a [few more](https://www.youtube.com/watch?v=UyJ6P-gnBwM) videos
out there doing the same sort of thing now, and hopefully I can get something
similar up and running pretty quickly. I'm interested in the process of aligning
the various point clouds between the Kinect devices and potentially something
like Tango - I can definitely see a use case where someone uses a mobile device
as a camera/depth feed, as well as having a different device for the actual display.

One area this will fall down is if the participant in the recording also wants
to be in VR at the same time - as you're going to end up with the headset and cable
and the like all visible in the captured view. Obviously, wearing a mobile headset
or something like Hololens mitigates this to some degree, but you're still ending
up with something covering your eyes.

The solution to this is probably going to involve projecting a previously captured
face or face feature set on to the head (as well as eye tracking / blink feeds, that
sort of thing). 

This has lead me to have a variety of conversations around how you can merge
all this sort of stuff together, and how much work you do up front to generate or
portray an avatar. Potentially, you could run the gamut from a live-feed only avatar
(meshed similarly to above), a previously-constructed avatar that's textured in realtime
using a video feed from a known/tracked position, a fully-captured avatar like
I was looking at a week or two back, or some combination of all of these techniques.

Here's a [real-world example](https://vimeo.com/103425574), but doing similar stuff in a constructed
space is basically the same math. If you realtime capture some or most of the body, but just
project on eyes and the top half of the head, it may be good enough.

So, that's the plan for the next week!

## GTX 1070

My [Zotac 1070](https://www.zotac.com/us/product/graphics_card/GeForce-GTX-1070/all) arrived
yesterday. It's nice to finally have a graphics card capable of running all the VR content
without dropping frames and telling me my machine is rubbish (I know it's rubbish, thanks
Oculus). This has lead onto a Fruit Ninja binge, which raised an interesting question from
my brother. I told him that it was a good workout, to which he asked, "Do you have any
metrics?".

## Measuring how active you are in VR

We had a Fitbit Flex hanging around the house, unused. I spent a good chunk of friday trying
to get this working and failing miserably, which stopped me from getting any immediate numbers,
but it has lead me to think, wouldn't it be cool to have some proper numbers for titles - like
a fitness rating for the app (under normal use cases). I'm certain that a large amount of room-scale
VR content in the near future will be directly fitness related - Yoga teaching, sports
tuition and the like - remember Sharon Stone's Tennis tutor in Total Recall?

I'm going to try and get my hands on a working fitness tracker, and properly start measuring
this stuff. This will mean me playing a lot more games and spending less time working directly
on the holodeck, but I think it could be educational research ;) Plus, if it gets me fitter
then it's been worthwhile.




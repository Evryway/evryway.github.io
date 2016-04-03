---
layout: post
title: Dev Blog - How to build a holodeck, week six
category: DevBlog
tags: DevBlog, weekly
keywords: holiday
---

This week, I've been taking a well earned rest and spending time with the wife and kids.
I've made good progress with the atlasing, but the on-device performance of textured
capture is pretty slow with my current process, so some work needs to be done
to split work units over frames, that sort of thing.

The camera intrinsics I get back from the Tango device don't quite match what I'm expecting
from the camera image after I project it, so I need to spend a little time looking at
why the projection is distorted.

Here's a from-device realtime capture. Holes are due to how I'm freezing the mesh cubes, and
should be resolved early next week.

![Latest mesh]({{ site.url }}/assets/week6/texmesh1.jpg)

## Next week ...

Next week I'll be back on this full time, and my goal is to finish up with capturing
the environment and move on to portals and avatars. As soon as I can get a virtual copy
of three rooms of my house, we're good to go!




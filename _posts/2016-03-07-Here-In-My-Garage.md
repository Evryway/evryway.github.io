---
layout: post
title: Here in my garage
category: DevBlog
tags: DevBlog, update
keywords: garage blender 47
---

Here in my garage, I have the world. No Lambourghinis (yet). Not even virtual ones.

## TL;DR

[Week three, day 1 - my garage in the real world](https://youtu.be/4pIDbyjLHUE)
{% include youtubep.html id="4pIDbyjLHUE" %}

[Week three, day 2 - my garage in the holodeck](https://youtu.be/ZfFzvU_aqYc)
{% include youtubep.html id="ZfFzvU_aqYc" %}

## Capturing the real world

The goal for the next few weeks is to make some progress on capturing the real world, in real time, into the device. The most recent Project Tango SDK includes a big chunk of functionality to do this, which I'm hoping to get working shortly (and then I've got a load of ideas on how to improve the quality).

For starters, though, we need to see what the end results could look like, so I've used the Tango Constructor app to capture my garage and drop it into Unity. 

The process is pretty convoluted right now - if anyone knows of a more efficient way to do this, please tell me! I'm taking the output of the Constructor (which is a .PLY file with vertex colours), pulling it into Blender, [generating a UV map and texture](https://www.youtube.com/watch?v=UwbmLsYTeyU) based on the colours at the vertices, and then exporting this out as the mesh to be used in the Unity scene. Doing this realtime is possible but complex, saving out the resulting mesh and texture data will be non-trivial, and making everything sync up will be a tricky process too.

I've manually aligned the imported mesh in my Unity scene such that the origin of the scan and the origin of the Unity scene (and the ADF) are all aligned - approximately. It's good enough not to bang into the walls or fall over things, but it's 10-15 cm out at the edges of my garage, so it's certainly a hazard to run around in.

## That looks terrible

I know, it looks awful. It's a good job I have no eye for aesthetics, or I'd be tempted to stop right now. Fortunately, my art-fu is weak, so I'm happy to keep trucking.

The garage scene in the first video has about 500K tris, and runs "ok" on device. The source asset is around 50MB though, which I don't really want hanging around (and hopefully isn't remotely representative of the asset size I'm aiming for!). The second video, I used a decimate in Blender to drop the garage asset down to about 70K tris - this is a lot closer to the actual size of asset I'm aiming for (about 6MB binary source). The recording does drop frames (I'm using [adb screenrecord](http://stackoverflow.com/questions/28217333/how-to-record-android-devices-screen-on-android-version-below-4-4-kitkat)) in the low-quality version, and drops a lot more in the high quality version. When I'm not recording, it's hitting a pretty stable 30fps and I'll be looking to push this higher in the future - given that Rift / Vive are aiming for 90fps and above for very good reasons, it's important that the performance isn't a million miles away from that. 

The quality of the asset in the scene is abysmal. I took very little time to create the scan (less than 2 minutes) and the lighting in the real environment is bad. The Constructor process aliases to something like a 5cm grid, there's no real texture on the mesh, there's no planar reduction other than what happened when I ran the decimate, and there's holes everywhere in the mesh. You have to start somewhere! The bonus of it being so bad currently is that it can only improve in time.


At the request of /u/as334 I've tried to jump around a bit at the end so you get an idea of how strong the tracking is. If you jump too high, the gyro currently causes the device orientation to flip, which isn't ideal - I'll look at locking that down at some point!



## Next up ...

I'll be looking at all the details of the capture process and hopefully getting some real time mesh generation working. I might need to get AR overlays in place which I'm sure will take some time, so no promises as to when this will be working.






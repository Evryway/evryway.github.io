---
layout: post
title: House Scale VR - realtime environment capture
category: DevBlog
tags: DevBlog, update
keywords: house scale, live action
---

Today, I've got realtime meshing working in the Holodeck. Video below, technical details below that!

## TL;DR

[Week three - housewalk ](https://youtu.be/5OdHTkSMynE)
{% include youtubep.html id="5OdHTkSMynE" %}

## Walking around my real house in VR

One of the primary goals of my holodeck prototype is to have a mobile experience in real-world environments. There's plenty of ways to capture the real world, but one that really excites me is to have it captured by the device in realtime.

Google have recently released an update to the Project Tango SDK (release Izar) which includes a set of calls into their realtime meshing generation process. Unfortunately for me, the code that actually does the meshing is in a separate native library, so I can't get my hands dirty in there easily. Fortunately, it's super-easy to get up and running, so as a baseline for testing the process of realtime meshing, it's a fantastic starting place.

## How does the meshing work?

According to the release notes, the meshing process uses Signed Distance Fields to convert the point cloud (coming from the Tango depth sensor) into a surface, then marching cubes to turn that into a mesh. There's a few settings you can fiddle with (the size of the grid space being one) but you don't have much control over how it works. What you do get is enough output to generate a dynamic mesh (or a set of dynamic meshes) with vertex, edge, normal and colour information. I'm currently setting the grid size to 50mm - smaller generates more fidelity in the world, at the expense of processing, storage and rendering cost.

There's a huge selection of advances in the space of turning point clouds into meshes, and I'll be looking at some of these in the next few weeks and months. I'd also like to get texture mapping onto the surface, rather than vertex colouring, which makes the whole mesh very undetailed currently.

## Why do this realtime?

Because it's cool. Plus, even if you're not interacting with that space in the virtual world, I think it's massively valuable to have a representation of the real-world space - for safety reasons, if nothing else (like Vive's chaperone).

## Why does it look so rubbish?

There's lots of reasons why it looks so terrible, and I'll be going into detail on each of them in the coming weeks. The main ones are the lack of texture and the grid fidelity, both of which are non-trivial problems to solve, so I'll be taking a stab at them both soon.

## Can you save the generated mesh out?

Not yet. I've got to get an exporter working (probably Collada, as OBJ doesn't officially support vertex colours) and I haven't yet found anything good on the Asset Store for doing runtime export, so I guess I'll be writing my own. If anyone knows of a good chunk of code for doing mesh export at runtime, please point me at it!

## Can I try this out?

I'm not putting anything up on the app store yet, for a variety of reasons. If you're near London, I could be tempted to do a demo for beer ;) but that's a conversation for a few weeks from now when I've got it looking a bit better.







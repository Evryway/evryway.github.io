---
layout: post
title: Saving the world
category: DevBlog
tags: DevBlog, daily
keywords: collada exporter, unity, textured mesh
---

Today, I'm intending to get the textured mesh up to a much higher quality.
There's lots of things to fix (LOTS of things). One of the key parts of this is
being able to examine the mesh somewhere other than on device, so I've written
an exporter.

Pics below! apologies for the lack of video right now, but at least a few pictures will
save me a few thousand words.


## COLLADA

The first couple of days this week have been spent writing a
[COLLADA](https://en.wikipedia.org/wiki/COLLADA) exporter. I've previously shied away from using COLLADA as a format because
FBX is basically the de-facto standard in all the toolchains I've ever worked with in the games
industry. This is good because at least there's a standard - but it's bad, because the format is
both proprietary and wrinkly.

COLLADA, on the other hand, is bloody *lovely*. I've spent more time getting the XML serialiser
working than I have fighting with the [COLLADA format](https://www.khronos.org/files/collada_reference_card_1_4.pdf),
which you can see has had a lot of thought behind it. 

So, two days in, and I've got an exporter that generates valid COLLADA output, including mesh positions, normals,
a UV channel and textured materials. Not too shabby. From previous experience, writing an equivalent OBJ or FBX would have
taken me an awful lot longer.

## Test assets and round tripping

![Round Trip Cube]({{ site.url }}/assets/week5/round_trip_cube.jpg)

Writing an output file is all well and good, but you need to check it's valid. My friend Ryan was generous enough
to provide me with a fantastic test asset (a cube! with textures!) that had everything in it I needed to pass through
the export process. Using this, I round tripped his test asset over and over until the output was pretty much identical to
the input. I then hand-created my own cube with modified UVs, did some coder-art for textures, and created a second
round trip cube, as shown above. This let me identify a few issues with the COLLADA to Unity import process (having to
flip an axis due to LHS/RHS conversion, having to reverse the [triangle winding order](https://www.opengl.org/wiki/Face_Culling)
to compensate) which wasn't obvious in the original test asset, because it was symmetrical and the UVs were fully spanning
the faces.

An hour or two of round tripping got me to the point of being able to push the output back in as input with visually
identical results. Bonza!

## The moment of truth

Testing the mesh capture process in the editor is not easy - especially not without a mesh to work with! I've got a few
smaller test assets I've used for pushing through the export process, but once they were working, the time had arrived to actually
do a scan on device and see if anything came out the other end. And it did. 

![Black Hole]({{ site.url }}/assets/week5/first_mesh_from_device.jpg)

Yay! something vaguely resembling the garage appears!

Now, it's pretty obvious from this test image that there's a problem where the black hole at the centre of the universe
is sucking all the polygons in. This was caused by my conversion process from the original Chisel-generated meshes, which
had empty verts in the vertex array.

The second major issue was the lack of textures, which was caused by not actually saving them to disk with the right name.

## second effort

![Coloured Hole]({{ site.url }}/assets/week5/second_mesh_from_device.jpg)

This is looking "better" - the textures are being applied, the UVs are obviously working. There's still a black hole in
the universe, but the fix for that didn't take too long.

## third effort

And here we are, with this morning's work.

![Get back into the kitchen]({{ site.url }}/assets/week5/kitchen_firstnodeset.jpg)

This is a very quick scan of the kitchen. The scanning process took about 2-3 minutes (about the same as videoing the space would).
The generated output actually has a lot more geometry in it, but due to being over 65K triangles, Unity is splitting it up into
separate meshes, and that is causing some very wierd glitches - so I'm going to fix that up asap. This image shows just the first
65K triangles with associated textures.

## How long does it take to export and import?

Saving on device takes 20-30 seconds for a 2-3 minute scan currently. This is down to two things - firstly, I'm generating far
too many texture images (most of which are duplicated). This can be fixed. Secondly, I'm putting all of the output files (the
collada .DAE file and the associated texture .PNG files) into a ZIP archive so it's trivially easy to get off the device. This
takes quite a while because it's chewing through a couple of hundred PNG files.

Importing it into Unity takes about 30 seconds too - mostly processing the textures on import. It imports with no user-intervention
*apart from one thing* - the shader is set to Unity's "Default" shader, and I can't find anything in the COLLADA file to
influence this. I've dropped an email to a guy I know at Unity who can hopefully help me with this, but if anyone out there
reading this knows what I need to fix, please tell me! For now, I've worked around it by creating an
[AssetPostProcessor](http://docs.unity3d.com/ScriptReference/AssetPostprocessor.html)
which fixes up shaders during import, and also forces the materials to be named the same as they are in the .DAE file, instead
of using the texture names.

So - Scan time plus about one minute to generate a textured mesh you can work with in any art package.

## Can I take a look at the test asset?

Not right now, apologies. I can give you some numbers though:

The archive is 80 MB, with a 20 MB .DAE file (which compresses down to 4 MB) and 205 512x512 PNG files
which are about 250K each.
The generated mesh (of which the picture above is about 1/3 of the total) has about 100K verts as per the COLLADA file.
So the image above has about 45K verts (65K triangles). The total asset has around 140K triangles.
There's currently 1 material for every snapshot texture/grid cube, plus a load of duplicates.

The mesh size and .DAE file size compare very favourably with the exports I've done previously using the Tango Constructor app,
and at some point I'll try and do a like-for-like comparison - probably next week.



## Next steps

I really need to get the texture size down and improve the texture resolution on the mesh, and both of them should be solved
by the chunk of work I'm going to try next. Then there's welding the mesh cubes together. I'll probably stop with the
prototype at that point!




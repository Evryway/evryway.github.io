---
layout: page
title: Evryway Scanner
permalink: /apps/evrywayscanner/
---

Scanner is an environment capture prototype running on Google's project Tango tablet. Scanner can scan a room
in realtime to a textured mesh, and save that out as a collada object.

Scanner is currently in Closed Alpha - if you've got a Tango device (ideally not a yellowstone kit) and would like to
test drive the app, contact me for more details.

## How to use Scanner (Alpha version 20161205)

Scanner uses the Tango depth and colour cameras to create a textured mesh representation of the things it sees.

The first step is to start up the feeds, so Scanner has some data to work with. Hit the feeds button, and
enable Texture and Pointcloud.

Once the feeds are enabled, start depth processing and texture processing (currently by turning on Chisel and Meshing,
respectively).

When everything is enabled, your screen should look something like this:

![Feeds Active](/assets/apps/scanner/feeds_active.jpg)

If you don't have at least two green indicator lights, something has gone wrong.

At this point, the device should start capturing what it sees. The capture region isn't currently shown on the screen,
but it covers about half of the top half of the screen. You'll get a feel for it.

You will need to keep the device still for the texture to be captured. Look at the fourth indicator - red means you're
moving, green means it should be capturing.

By default, Scanner will try and localise against the newest ADF file on device. If it successfully localises, the third
indicator will go green.

To Save, go back to the main menu and hit "Save Mesh". If it doesn't crash, you should end up with a zip file under
/sdcard/EvrywayScanner, timestamped to the time the mesh is saved. Inside the zip file should be a collada (.dae) file and a textures
directory containing the various atlas textures.

You should be able to load the file into Unity, Blender, etc - anything that supports Collada. For now, upload to
Sketchfab doesn't work (either of the raw file or in app) - it's on the list.


## Features that ain't present or working yet:

* Export to OBJ
* Export to Sketchfab
* Colour balancing
* Mesh chunk welding
* ADF selection
* ADF creation
* Any kind of fancy UI
* Any kind of tutorial
* Privacy policy

*Please note* - this app may explode your device, cause an alien or other-dimensional invasion and/or imbue you with
super powers, wanted or not. In other words, if something breaks, no liability is implied and you're on your own.






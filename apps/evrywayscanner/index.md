---
layout: page
title: Evryway Scanner
permalink: /apps/evrywayscanner/
---

Scanner is an environment capture tool running on Google's project Tango hardware. Scanner can scan a room
in realtime to a textured mesh, and save that out as an OBJ or collada object.

Here's an example:

<div class="sketchfab-embed-wrapper"><iframe width="640" height="480" src="https://sketchfab.com/models/26e2ce9d17644ef8a1a20867244b7393/embed" frameborder="0" allowvr allowfullscreen mozallowfullscreen="true" webkitallowfullscreen="true" onmousewheel=""></iframe>

<p style="font-size: 13px; font-weight: normal; margin: 5px; color: #4A4A4A;">
    <a href="https://sketchfab.com/models/26e2ce9d17644ef8a1a20867244b7393?utm_medium=embed&utm_source=website&utm_campain=share-popup" target="_blank" style="font-weight: bold; color: #1CAAD9;">Garage V2 on Phab2Pro 4cm</a>
    by <a href="https://sketchfab.com/timmo.swan?utm_medium=embed&utm_source=website&utm_campain=share-popup" target="_blank" style="font-weight: bold; color: #1CAAD9;">timmo.swan</a>
    on <a href="https://sketchfab.com?utm_medium=embed&utm_source=website&utm_campain=share-popup" target="_blank" style="font-weight: bold; color: #1CAAD9;">Sketchfab</a>
</p>
</div>

## How to get scanner:

#### Scanner ALPHA/BETA CONDITIONS

Scanner is in Closed Beta. please [contact me](mailto:hi@evryway.com) for instructions on how to join.
Testing is currently limited to Phab 2 Pro owners. Scanner works on Yellowstone too, but the experience
is not ideal.

* Don't expect anything to work. ANYTHING.
* Respect my work (don't steal / share / dissasemble the app)
* Use scanner for good, not evil.

*Don't agree to these conditions? No app for you.*

If you want to try it, expect to be asked to test things repeatedly. If you don't want *me* to be bugging *you* then
don't ask!

#### Download the app

Once you're granted access, [download the app from the play store.](https://play.google.com/apps/testing/com.evryway.scanner.a1)
 
#### Join the Evryway Feedback community on Google+

Please [join the community and give feedback.](https://plus.google.com/communities/104588434400522026854)

## Release notes:

V1.0.1.1 (20161217)
Added Sketchfab export, using Oauth2. As long as your mesh is a reasonable size, you should be able to export directly to Sketchfab.
You will need to manually setup your model after import on the website, as it will be in Draft mode. Ideal settings are Unlit, with
a touch of sharpness.


## How to use Scanner:

### V1.0.1.0 (20161214)

Scanner uses the Tango depth and colour cameras to create a textured mesh representation of the things it sees.

The main screen looks like this:

![Main screen](/assets/apps/scanner/main_screen.jpg)

You've got three sub-menus - feeds, save, visualisation.

you'll also see four coloured boxes on the screen - hopefully all green!

If you don't have at least two green indicator lights, capture won't work.

* ONE: Tango system connected. If this is RED, try restarting the app, rebooting your device.
* TWO: Tango pose received. If this is RED, you're not getting a pose. try waving the device around a bit.
* THREE: ADF recognised. If this is RED, you're not connected to an ADF (expect drift).
* FOUR: Camera moving too fast. if this is RED, hold the device still.

#### Capturing the mesh

The first step is to start up the feeds, so Scanner has some data to work with. Hit the FEEDS button, and
enable Texture and Pointcloud by tapping on them. They should light up.

![Feeds Active](/assets/apps/scanner/feeds_active.jpg)


Once the feeds are enabled, start capture by hitting the CAPTURE button to turn it ON.

When everything is enabled, your screen should look something like this:

![Capture Active](/assets/apps/scanner/capture_active.jpg)

At this point, the device should start capturing what it sees. The capture region isn't currently shown on the screen,
but it covers about half of the screen.

#### Getting valid results

You will need to keep the device still for the texture to be captured. Look at the fourth indicator - red means you're
moving, green means it should be capturing.

By default, Scanner will try and localise against the newest ADF file on device. If it successfully localises, the third
indicator will go green.

If you can't seem to capture an area, try a different view on it - walk to one side, get closer or further away, etc.
the capture region should be about 1-3 metres in front of you. Technical details on how to get good results should
come soon!

#### Saving your mesh

To Save, go back to the main menu and hit "Save". This brings up the Save menu.

You can save as Collada or OBJ format. I'd recommend OBJ format right now, as that should be usable on Sketchfab.

If it doesn't crash, you should end up with a zip file under
/sdcard/EvrywayScanner, timestamped to the time the mesh is saved. Inside the zip file should be your and a textures
directory containing the various atlas textures. If you hit "Save OBJ" you should have a .OBJ and a .MTL file.
If you hit "Save Collada" you should have a .dae file.

##### OBJ format

You should be able to upload the zip directly to sketchfab.

##### Collada format

You should be able to load the file into Unity, Blender, etc - anything that supports Collada. For now, upload to
Sketchfab doesn't work (either of the raw file or in app) - it's on the list.


## Features that ain't present or working yet:

* Sketchfab preset settings
* Colour balancing
* Mesh chunk welding
* ADF selection
* ADF creation / learning mode
* Any kind of fancy UI
* Any kind of tutorial
* Privacy policy

*Please note* - this app may explode your device, cause an alien or other-dimensional invasion and/or imbue you with
super powers, wanted or not. In other words, if something breaks, no liability is implied and you're on your own.






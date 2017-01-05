---
layout: page
title: Evryway Scanner
permalink: /apps/evrywayscanner/
---

Scanner is an environment capture tool running on Google's project Tango hardware. Scanner can scan a room
in realtime to a textured mesh, and save that out as an OBJ or collada object.

Here's an example:

<div class="sketchfab-embed-wrapper"><iframe width="640" height="480" src="https://sketchfab.com/models/4f2a6820bb20437f96492c045ac25347/embed" frameborder="0" allowvr allowfullscreen mozallowfullscreen="true" webkitallowfullscreen="true" onmousewheel=""></iframe>

<p style="font-size: 13px; font-weight: normal; margin: 5px; color: #4A4A4A;">
    <a href="https://sketchfab.com/models/4f2a6820bb20437f96492c045ac25347?utm_medium=embed&utm_source=website&utm_campain=share-popup" target="_blank" style="font-weight: bold; color: #1CAAD9;">Kitchen V21 4cm Phab 2 Pro</a>
    by <a href="https://sketchfab.com/timmo.swan?utm_medium=embed&utm_source=website&utm_campain=share-popup" target="_blank" style="font-weight: bold; color: #1CAAD9;">timmo.swan</a>
    on <a href="https://sketchfab.com?utm_medium=embed&utm_source=website&utm_campain=share-popup" target="_blank" style="font-weight: bold; color: #1CAAD9;">Sketchfab</a>
</p>
</div>

[A Gallery of examples here.](https://sketchfab.com/Evryway/collections/evryway-scanner){:target="_blank"}

## How to use Scanner:

### V1.0.2.1 (20170105)

Scanner uses the Tango depth and colour cameras to create a textured mesh representation of the things it sees.

The main screen looks like this:

![Main screen](/assets/apps/scanner/main_screen.jpg)

(note, this is in portrait mode - you can start the app in either portrait or landscape, just hold the device
in the format you want *before* pressing the icon to launch it. Scanner is rotation-locked once it's running
as it's frustrating having the screen rotate during a scan).

On the left : Record, Save, Clear.

Up top left : Settings.

At the top right: Status indicators.

#### Status indicators

You'll see four coloured boxes on the screen - hopefully all green!

*If you don't have at least the top two green indicator lights, capture won't work.*

* ONE: Tango system connected. If this is RED, try restarting the app, rebooting your device.
* TWO: Tango pose received. If this is RED, you're not getting a pose. try waving the device around a bit.
* THREE: ADF recognised. If this is RED, you're not connected to an ADF (expect drift).
* FOUR: Camera moving too fast. if this is RED, hold the device still.


#### Recording a scan

Press "Record" to start recording. the button will go red, and say "Recording".
Press "Recording" to stop. the button will go white and say "Record".

#### Clearing your scan

If you're not happy with what you've scanned, hit "Clear" to start anew.


## Capturing the mesh

Start recording by pressing "Record". The button should go red, and
you should see stuff appear on screen. If you don't, try moving around and pointing the 
camera somewhere else. (If you have problems with this, please say something!)


At this point, the device should start capturing what it sees. The capture region isn't currently shown on the screen,
but it covers about half of the screen.

![Recording](/assets/apps/scanner/recording.jpg)

#### Saving your scan

To Save, from the main menu hit "Save". This brings up the Save menu.
![Save Menu](/assets/apps/scanner/save_menu.jpg)

You can save as Collada or OBJ format. I'd recommend OBJ format right now, as that's the simplest format to work with.

If it doesn't crash, you should end up with a zip file under
/sdcard/EvrywayScanner, timestamped to the time the mesh is saved. Inside the zip file should be your object and a textures
directory containing the various atlas textures. If you hit "Save OBJ" you should have a .OBJ and a .MTL file.
If you hit "Save Collada" you should have a .dae file.

##### OBJ format

You should be able to upload the zip directly to sketchfab, or unzip and work with any modelling package that
supports OBJ files.

##### Collada format

You should be able to load the file into Unity, Blender, etc - anything that supports Collada. For now, upload to
Sketchfab doesn't work (either of the raw file or in app) - it's on the list.

##### Sketchfab

Hit the Sketchfab button to export to Sketchfab. You'll be kicked to a browser to do Oauth2 authorization. When you
grant access, select the Evryway Scanner app to handle the result, and your model should be uploaded.

If you don't have a Sketchfab account I can highly recommend getting one. [Sketchfab Referral](https://skfb.ly/XSHs)

### Settings menu

#### Help

Press the help button to be taken to this page.

#### (EXPERIMENTAL) ADF selection

Scanner works best when you are localised to an Area Definition File. If you have ADFs stored on your device,
you can select one from the dropdown.

#### (EXPERIMENTAL) Resolution

You can increase or decrease the resolution of the scan using this dropdown. larger resolution scans will be
more blocky, but can capture a much larger volume for the same memory cost. use 40mm for room scale, and
go smaller for a more refined mesh or larger if you want to cover a bigger space. Smaller resolutions will
automatically reduce the distance Scanner sees (3.5m at 40mm resolution down to 1.25m at 10mm resolution).

#### Debug menus

You've got two debug menus : Feeds and Visualisation.

Feeds lets you turn on and off the texture feed and the pointcloud feed. You shouldn't need to mess with these,
but sometimes it's handy for debugging issues.

Visualisation lets you turn on and off the pointcloud and texture debugging tools.

Pointclouds are shown as a spread of colours, going from Red (close to the camera) through to blue (far away
from the camera) in bands roughly one metre wide.

### Getting good results

You will need to keep the device still for the mesh and texture to be captured. Look at the fourth indicator - red means you're
moving, green means it should be capturing.

#### Creating an ADF

By default, Scanner will try and localise against the newest ADF file on device. If it successfully localises, the third
indicator will go green. *you will get much better results if you use an ADF*.

There's no option to create an ADF inside the app just yet. The simplest thing to do is to use
[Tango Explorer](https://play.google.com/store/apps/details?id=com.projecttango.tangoexplorer){:target="_blank"}

 to create
a new ADF of the area you're about to scan. You can switch between ADFs in the Settings menu.

#### Working around chunks

Mesh chunks only get captured or updated when they are visible to the camera - and that's the whole chunk cube, not
just what you see. If there's a hole in the mesh that you can't seem to update, or If you can't seem to capture an area,
try a different view on it - walk to one side, get closer or further away, etc.
the capture region should be about 1-3 metres in front of you. 


## How to get scanner

Scanner is in Closed Beta. please [contact me](mailto:hi@evryway.com) for instructions on how to join.
Testing is currently limited to Phab 2 Pro owners. Scanner works on Yellowstone too, but the experience
is not ideal.

<a name="betatester"> </a>

#### Scanner Beta Test User Conditions

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




## Features that ain't present or working yet:

* Sketchfab preset settings
* Colour balancing
* ADF creation / learning mode
* Any kind of fancy UI
* Any kind of tutorial

*Please note* - this app may explode your device, cause an alien or other-dimensional invasion and/or imbue you with
super powers, wanted or not. In other words, if something breaks, no liability is implied and you're on your own.

[Privacy policy is here.](https://www.evryway.com/apps/evrywayscanner/privacy_policy)

## Release notes

1.0.2.1
ADFs can be selected from the settings menu.
Scan resolution can be selected from the settings menu.

1.0.2.0
Added multitexturing (preserve and reproject all relevant textures).
Added regenerate pass on save.
More bug fixes and performance tweaks.

1.0.1.7
More data clearance on CLEAR (hopefully that's the last of the SDF data removed)
new icon! (Thanks Hen)

1.0.1.6
NEW: experimental mesh regeneration
(this should fix cracks and some missing geometry)
Changed how textures are stored and applied
Fixed help button

1.0.1.5
Turned back on retexturing. (disabled by mistake!)

1.0.1.4
Main menu UI changes:
Added RECORD, CLEAR.

1.0.1.3
Fixed rotation of texture visualisation quad (it's nearly the right size and in nearly the right place now).

1.0.1.2
Added portrait support (much easier to hold on Phab)
Scanner will start up in whatever orientation you are in when you press the icon. If you want to run in Landscape, then start the app with the device in landscape mode.

1.0.1.1
Added Sketchfab upload - please test and see if it works for you!
Toast added to save flow, so there's a vague idea of what's happening.

1.0.1.0
"works on Phab".
Lots of changes to handle device orientation.



---
layout: page
title: Evryway Scanner Tutorial
permalink: /apps/evrywayscanner/tutorial
---


## [V1.0.2.9](index)

Scanner uses the Tango depth and colour cameras to create a textured mesh representation of the things it sees.

### Starting the app

You can start Scanner in either portrait or landscape mode. Hold the device in the orientation you want to use
then start the app. Scanner is rotation locked while running to ensure the device doesn't flip orientation
while recording.

### Taking a scan


![Main screen](/assets/apps/scanner/intro_1_crs.png)

To start scanning, hit the "Record" button. It will turn red, and show "Recording". Hold your device still, and
you will see the environment appear on the screen. Scanner pauses capture while the device is moving.

![Recording](/assets/apps/scanner/intro_2_crs.png)

To stop scanning, hit the "Recording" button. It will turn white, and show "Record".

To clear your scan and start a new one, hit "Clear".


### Status indicators

In the top right corner are four status indicators.

![Status](/assets/apps/scanner/intro_3_status.png)

*If you don't have at least the top two green indicator lights, capture won't work.*

* Tango system: If this is RED, try restarting the app or rebooting your device.
* Tango pose: If this is RED, you're not getting a pose. Check that the camera is not covered.
* ADF recognised: If this is RED, you're not connected to an ADF (expect drift).
* Camera motion: if this is RED, hold the device still.

### Saving your scan

To Save, from the main menu hit "Save". This brings up the Save menu.
![Save Menu](/assets/apps/scanner/intro_4_save.png)

#### Save to Sketchfab

If you have a Sketchfab account, you can upload your model directly to Sketchfab by hitting the "Sketchfab" button.

Scanner uses OAuth2 to authorize your account with Sketchfab. If you have not authorized recently, you will be taken
to a browser window. Hit "Authorize". If this is your first time uploading, please ensure you select "Evryway Scanner"
to handle the authorization response. You will be taken back to the app to complete your upload.

If you don't have a Sketchfab account I can highly recommend getting one. [Sketchfab Referral](https://skfb.ly/XSHs)

#### Save to device (OBJ and Collada formats)

You can save your scan directly to your device by hitting the "Save OBJ" or "Save Collada" buttons. Your capture
will be saved into the /sdcard/EvrywayScanner folder on device as a zip file containing your object in the relevant
format (.OBJ and .MTL for OBJ, .DAE for Collada) and the textures in a subfolder.

OBJ format is recommended, as most content creation tools will work with this format.


## Settings menu

### Help

Press the help button to be taken to this page.

### ADF selection

Scanner works best when you are localised to an Area Definition File. If you have ADFs stored on your device,
you can select one from the dropdown.

### Resolution

You can increase or decrease the resolution of the scan using this dropdown. larger resolution scans will be
more blocky, but can capture a much larger volume for the same memory cost. use 40mm for room scale, and
go smaller for a more refined mesh or larger if you want to cover a bigger space. Smaller resolutions will
automatically reduce the distance Scanner sees (3.5m at 40mm resolution down to 1.25m at 10mm resolution).

### Debug menus

You've got three debug menus : Experiments, Feeds and Visualisation. *Use with caution!*

Feeds lets you record, playback, enable and disable the texture and pointcloud feeds. You shouldn't need to mess with these,
but sometimes it's handy for debugging issues.

Feed recording and playback allows for capture of the raw frames from the sensors for later diagnosis. I recommend
not using these unless you're asked to.

Visualisation lets you turn on and off the pointcloud and texture debugging tools.

Pointclouds are shown as a spread of colours, going from Red (close to the camera) through to blue (far away
from the camera) in bands roughly one metre wide.

## Getting good results

You will need to keep the device still for the mesh and texture to be captured. Look at the fourth indicator - red means you're
moving, green means it should be capturing.

If you find you have holes in your mesh, or the texture isn't as expected, try capturing from a different angle or distance.
The optimal capture distance is around 1-2 metres away from the device.

## Creating an ADF

By default, Scanner will try and localise against the newest ADF file on device. If it successfully localises, the third
indicator will go green. *you will get much better results if you use an ADF*.

There's no option to create an ADF inside the app just yet. The simplest thing to do is to use
[Tango Explorer](https://play.google.com/store/apps/details?id=com.projecttango.tangoexplorer){:target="_blank"}
to create a new ADF of the area you're about to scan. You can switch between ADFs in the Settings menu.


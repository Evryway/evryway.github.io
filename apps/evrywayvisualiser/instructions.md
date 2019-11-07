---
layout: visualiser
title: Evryway Visualiser Instructions 
permalink: /apps/evrywayvisualiser/instructions
---

[(back to Evryway Visualiser)](index)

# How to download

[Evryway Visualiser is currently available via Itch.io.](https://evryway.itch.io/evryway-visualiser)

# How to install

### Via SideQuest

Ensure you've got the latest version of [SideQuest](https://sidequestvr.com/#/) installed.

Download the APK, browse to it in Windows Exploder, and drag it on to the SideQuest window.

![install sidequest](install_sidequest.png){:height="50%" width="50%"}

### Via ADB

You'll need [ADB installed](https://www.howtogeek.com/125769/how-to-install-and-use-abd-the-android-debug-bridge-utility/)
and on your path.

Open up a command prompt in windows. 

Check ADB is recognising your device by typing

'''
    adb devices
'''

if nothing appears, check your Quest is connected via a USB cable. Make sure you've only got one device connected.

Once your Quest is connected, use ADB to install Evryway Visualiser:

'''
adb install -r path_to_your_downloads/com.Evryway.EvrywayVisualiser_Release.apk
'''

# How to visualise

As of Nov, 2019, Visualiser will begin playing a demo song.

use the LEFT HAND STICK to skip the current track forwards and backwards.

use the RIGHT HAND STICK to skip to previous and next track.

Press the MENU button on the left controller to bring up the menu at any point.

Select TRACKS for a list of music tracks. 
* Browse sources by highlighting them with the pointer and clicking with the trigger.
* You can use the joystick to scroll (just point away from the menu).

Select SETTINGS for application settings.

Select INFO to find out additional details about the app.

If you keep your hands still for a while, they'll fade away. Move them to bring them back.






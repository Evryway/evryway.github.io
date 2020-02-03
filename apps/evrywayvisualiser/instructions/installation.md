---
layout: visualiser
title: Instructions - Installation
permalink: /apps/evrywayvisualiser/instructions/installation
---
[(Back to instructions)](index)

# [How to download](#how-to-download)

[Evryway Visualiser is currently available via Itch.io.](https://evryway.itch.io/evryway-visualiser)

# [How to install](#how-to-install)

## Via SideQuest

Ensure you've got the latest version of [SideQuest](https://sidequestvr.com/#/) installed.

If you have already downloaded the APK from Itch.io, you can manually install it via Sidequest.

browse to the APK in Windows Explorer, and drag it on to the SideQuest window.

![install sidequest](install_sidequest.png){:height="50%" width="50%"}

If you don't have a local copy already, you can grab it while in Sidequest.

[Sidequest app link](https://sidequestvr.com/#/app/325)

If you have claimed your key on Itch, you can click the "Update On Itch" button in Sidequest.
If you're on the latest version you may see "Buy on Itch" or "View On Itch" instead.

![install via itch1](install_sq_itch_update.png)

Next, click "Download"

![install via itch1](install_sq_itch1.png)

 then pick the latest release APK.
SideQuest will download and install it for you.

![install via itch2](install_sq_itch2.png)

If you don't see the "Download" button on the Itch.io page, and you've already claimed a valid download key,
make sure you're logged in to Itch.Io while in Sidequest. You don't ever need to purchase more than once!

## Via ADB

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
---
[(Back to instructions)](index)


---
layout: visualiser
title: Evryway Visualiser Release Notes
permalink: /apps/evrywayvisualiser/release_notes
---

[(back to Evryway Visualiser)](index)

# 0.102 (20201228)

Latest Oculus SDK (23.1, 1.55.1) and Unity updates.
Various profile bug fixes, including incorrectly storing the display refresh rate on Quest 2.
Merry Christmas!

# 0.94 (20201209)

Improved hand tracking (re-write of all input tracking to poll transforms multiple times per frame, removed legacy
XR calls and cleaned up all XR device interactions).

# 0.92 (20201110)

Demo mode released!


# 0.90 (20201028)

New effect : Kaleidoscope

# 0.89 (20201019)

90 Hz mode now supports quick switching (set the mode in Sidequest, press the power button, wait for the beep,
press the power button again).

# 0.88 (20201017)

Quest 2 is now properly supported!
90 Hz mode!
Quest 2 bug fixes, including re-enabling local file system support.

# 0.87 (20201014)

Quest 2 version! Some of the Effect Graph effects were using Alpha blending, which seems to perform terribly on Quest 2.
I've switched them over to Additive instead, they look better and don't drop frames.
Just about everything else looks like it's working fine.

# 0.84 (20200923)

Added support for Oculus system "Menu" hand gesture (additional to thumbs-up hand gesture).

# 0.83 (20200923)

Unity 2020 version. That was a proper slog, I can tell you. So many bugs logged, so many heads banged into desks.
But we're up and running ;)

# 0.81 (20200921)

Maintenance update.

# 0.80

Update to OVR 20.
More changes to support Unity 2020 XR plugin architecture. Nearly there.

# 0.79

Update to Unity 2019.4.8f1, Update to OVR 19.
Lots of system changes to support Unity 2020 XR Plugin architecture, lots of package updates, lots of regression fixes.
Not many effects - once we're over to 2020, that's next.

# 0.78

Update to Unity 2019.4.3.
Performance improvements.

# 0.76 (20200616)

New effects : More dancers!

# 0.75 (20200615)

New effect : Dancers

# 0.74 (20200609)

Unity update to 2019.4.0 LTS

# 0.73 (20200603)

Bug fix for menu position when the app is paused (backgrounding then resumed)
Bug fix for track names being displayed when user prefs are set to "Never" for track info.

# 0.72 (20200526)

Added option to disable track info text, progress bars etc for a more immersive experience.

# 0.71 (20200525)

Bedtime mode is now Recliner mode - added new recliner options.

Lots of bug fixes and improvements.

Updated to latest Unity and OVR Plugin versions.

# 0.68 (20200420)

Track transport hand menu - buttons now move based on your finger push. Nice!
Happy 420!


# 0.67 (20200420)

Moved most of the effects over to using the pulse engine for tempo matching.
Track transport now shows a button press - halfway where to making the buttons decent.

# 0.66 (20200417)

Visualiser is now in Beta.
Automatic beat matching algorithm now in place - not used on many effects yet, but I'll be moving most pulsing effects over soon.
DLNA improvements.
Unity upgrades.
New effects (Fire flow, Laser show)

# 0.57 (20200401)

New effects. Shader graph effects and custom render textures - first tests.

# 0.53 (20200311)

DLNA improvement - fix for Plex not responding in DLNA mode.

# 0.51 (20200226)

New effect : Ring Swirls.

# 0.50 (20200225)

Fixed bugs in effects and hand colour.
Unity upgrades.

# 0.49 (20200222)

New effect - chase lines. (more to come this month!)
Hand colour can be changed in the settings menu.

# 0.47 (20200210)

Improved transport menu - no more random presses with the wrong hand.

# 0.46 (20200209)

Fixed hand tracking thumbs-up for menu. Oops!

# 0.45 (20200209)

Added in transport menu - hold your hand palm-up to open it.


# 0.44 (20200203)

Added instructions panel when using Hand Tracking
Fix for intructions webpage link.

# 0.43 (20200203)

Hand tracking improvements.
Lots of bug fixes and tweaks to menus.
Better snowfall!
Update to Unity 2019.3.0f6, fixed all the input to use new XR input devices.
Instructions update and new video!

# 0.41 (20200123)

Hand tracking! Oculus quest hand tracking now working.
Since there's no buttons, just give a thumbs-up with your left hand to get the menu.
More gesture support coming soon.
Improved DLNA server detection and reliability - should work with many more DLNA servers now.
added snowflakes. Needs update.

# 0.33 (20191214)

Added Bedtime mode.
Added Rainfall effect.

# 0.31 (20191207)

Added effect cycle delay setting.

# 0.30 (20191202)

Unity Visual Effects Graph is go! Fireworks go boom.

# 0.25 (20191130)

Another DLNA fix.

# 0.24 (20191130)

Switch over to URP in Unity.
Fix for DLNA server app on Android.

# 0.23 (20191127)

Added effects settings - you can now enable/disable effects individually.
Upgrade to Unity 2019.3 - URP here we come.

# 0.21 (20191116)

Added HearThis.At search - experimental!

# 0.20 (20191114)

Added VR Keyboard.
Enabled Net Search.
Turned VR Keyboard back off because search didn't work properly.

Added HearThis.At feed support - experimental!

# 0.18 (20191110)

Added profile, added "press menu button" tutorial flow, fixed alpha sorting bug (thanks @johnneke)

# 0.0.17 (20191109)

Fixed bug with scrub bar and tracks locking up. (thanks @2tmb)

# 0.0.16 (20191106)

New effect added.

# 0.0.15 (20191103)

Added licence texts, and some instructions in-app.

# 0.0.1 (20191030)

First Alpha build! It might even work. It might even work for you!


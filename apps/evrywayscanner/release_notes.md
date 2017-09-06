---
layout: page
title: Evryway Scanner Release Notes
permalink: /apps/evrywayscanner/release_notes
---

[(back to Evryway Scanner)](index)

1.2.0.0 (20170901)
Now working on Zenfone AR!
Update to Ikariotikos SDK.

1.1.2.0 (20170617)
Update to Hopak.
Fix for lockup when backgrounding / restoring app.
 
1.1.0.3: (20170329)
Farandole release 
 
1.1.0.2 (20170321)
Update for Additional Tango device support
 
1.1.0.0 (20170213)
General release
 
1.0.3.7 (20170209)
Faster saving process.
Removed Collada export.

1.0.3.6 (20170208)
Performance and memory improvements.
Increased point cloud processing quality.
Optimized save flow.

1.0.3.4 (20170203)
Added memory usage display

1.0.3.3 (20170202)
Fix for lockup during scan on large datasets

1.0.3.2 (20170131)
Performance improvements
Open beta time!

1.0.3.1 (20170130)
Performance and quality improvements

1.0.3.0 (20170128)
IL2CPP release build
UI updated

1.0.2.9 (20170127)
Improvements to texture occlusion
Performance and stability improvements
Tidy up preparation for open beta

1.0.2.6 (20170119)
Occluder experiment enabled by default.
Lots of improvements to occluder flow.

1.0.2.5 (20170118)
Fix for atlas corruption on edges of models
Sketchfab shadeless setting and "ready to publish" notification
New experiments:
Feed replay and record to local device
Stats display 
Depth occlusion on projection mapping

1.0.2.4 (20170116)
Sketchfab authorisation flow improvements
Experimental settings menu

1.0.2.3 "Cream and Jam" (20170109)
Atlases now cleared on defrag
Android back button works in menu flow

1.0.2.2   (20170106)
Black world + grid (no more skybox)
UI overhaul. Bigger buttons.

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
Works on Lenovo Phab 2 Pro.
Lots of changes to handle device orientation.

1.0.0.7:
removed READ_PHONE_STATE.
Switched to using device-orientation corrected intrinsics. May need to rotate texture on phab due to this.
Deferred feed construction until tango service is connected.
lots more logging.

1.0.0.6:
Added READ_PHONE_STATE perm, not sure if this is absolutely required for device UUID (will remove if not).

1.0.0.5:
fixed pointcloud visualisation. 

1.0.0.4:
fixed supported devices to only Tango 


1.0.0.3:
Update to Argentine.
Added OBJ exporter.

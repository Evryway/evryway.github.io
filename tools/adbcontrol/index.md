---
layout: page
title: Evryway ADB Control
permalink: /tools/adbcontrol/
tags: unity unity3d adb logcat quest oculusquest android tool
---

Evryway ADB Control allows you to control your android devices from inside the Unity Editor.

* Start, pause and stop your android app.
* Inspect the logcat output directly in the editor, with customisable filters.
* Switch between multiple devices, or enable TCP wireless connections with a button press.
* Extend with your own custom build pipeline functions, and easily write your own ADB utilities.


## First steps

Install the package from the Asset Store.
If you wish, you can move the ADBControl directory anywhere in your project.
You should have an "Evryway/ADB Control" menu option - select it, and the "ADB Control" window will appear.

## ADB Control Window

You'll see four panes in the window.

At the top of each pane, you will be able to see the currently selected device, as well as three buttons
allowing you to start, pause and stop your application on the device. This is controlled by the Android player
package name - simply change the package name if you wish to control a different application.

### Devices

![Devices](/tools/adbcontrol/devices.png "Devices"){:width="640px" class="imgcenter"}

Here you can:

1. see a list of available devices
2. select your current device from the list
3. Change a device from a USB connection to a TCP connection
4. Reset all available devices

All devices that have been connected are stored in the list. The connections are cached in a file in your unity project at
Library/Evryway/AdbControl/adb_control_devices.json.

When a device is connected, you are able to select it. The currently selected device will be shown in yellow - any commands
that require a specific device will target the selected device (e.g. logcat, run and stop, etc).

Sometimes it's helpful for a device to be connected in TCP (wireless) mode, rather than wired via a USB cable. When a device
is connected with USB, you can select "To TCP" and the device will be reconnected as a TCP device. You can then disconnect
the USB cable and still access the device via ADB over the TCP connection.

### Log

![Log](/tools/adbcontrol/log1.png "Log"){:width="640px" class="imgcenter"}

Here you can:

1. View the logcat output for the currently selected device
2. Copy and reset the log output
3. Select active channels for the filter

The Log window gives you a via of the logcat logs for the currently selected device.
By default, the "Unity" log channel will always be displayed, as will the "System" log channel.
Selecting "Channels" will give you a list of channels which can be toggled on and off.

![Log Channels](/tools/adbcontrol/log2.png "Log Channels"){:width="640px" class="imgcenter"}


selecting "Show All" lets you see all output, unfiltered.

### Build

Here you can:

1. Assign your own custom build functions to a button

To assign a custom build function, See the "How to configure ADB Control" section for more details.

### Utilities

![Utilities](/tools/adbcontrol/utilities.png "Utilities"){:width="640px" class="imgcenter"}

Here you can:

1. Toggle the ADB command output in the editor console
2. Take a screenshot
3. Assign your own custom utility functions to a button

If an ADB command does not function correctly, you can enable command output to the console to help diagnose the issue.

Pressing "Screenshot" will capture a screenshot from the currently active device.

To assign a custom utility function, see the "How to configure ADB Control" section for more details.


## How to configure ADB Control

take a look at Editor/ADBCConfigExample.cs. You'll see examples of how you can:
1. Set an override path to adb.exe
2. Provide a build function
3. Provide a utility function

Please ensure you place your version of this class in an editor assembly - either under an Editor directory in your project,
or controlled by an editor-only assembly definition file.

## Feedback and support

We'd love to hear your feedback (good and bad!) for ADB Control. If you have any problems, or great ideas for how to improve
ADB Control, please get in touch:

* email support@evryway.com
* twitter @evryway
* https://evryway.com


Evryway ADB Control is copyright Evryway Limited, 2020


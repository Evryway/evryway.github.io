---
layout: post
title: Dev Blog - How to build a holodeck, week 11
category: DevBlog
tags: DevBlog, weekly
keywords: 
---

This week I've been enjoying the sun and the family time.
I've also spent a little time working on a game prototype on the Vive
and finished up my codebase refactor so I can spin up new prototypes quickly. Details below.

## TL;DR

No videos this week, just words.

## Family time

I've been going slightly garage crazy over the last few weeks - a combination of hitting
some brick walls on the environment capture prototype, not having a team of excellent
folks around me to help me out (shouts out to my [Boss Alien](http://www.bossalien.com) crew)
and having to put some real thought into architecture - it was all combining to kill my motivation.

What better way to rejuvenate than to spent time with my kids and wife enjoying the sunshine?
So that's what we've been doing. I'm in that lucky place where I can decide exactly what
I'd like to do with my time, and I've been heads-down since I left Zynga, which has finally caught up with me.

A few days of relaxation and sunshine have worked wonders for my mood,
even if they haven't solved any of my technical problems.

## Tango upgrades

I've been keeping on top of the Tango SDK updates pretty religiously, which has been
a good call, all the way up to Lucida Anseris (the latest SDK release late last month).
For some reason, a big chunk of my code stopped working in the editor (well, a variety
of reasons, once I started digging). I appreciate the effort that goes into this kind
of project, so the good folks at Google get a pass this time, but I hope it's not a sign
of things to come. Fingers crossed the next release resolves some of my specific problems
and doesn't go any further backwards.

## Vive game prototype

Part of my research list includes working with the Vive motion controllers. The more time
I spend in the Vive environment, the more it's solidifying for me that room-scale (and larger)
is the best way to experience VR. The 1-to-1 mapping of motion to experience, the freedom
to interact with a wider environment in a natural fashion - I'm totally loving it.

To satisfy this bullet point on my list, I've kicked off a small game prototype that lets
me move items around in the virtual world. I've spent a lot less time on this than I'd like
this week, and I might focus more on it next week - if I can get something worth showing off
(without being too blatant about the idea) I'll pop up some vids on it next week - I might
keep a lid on this a little longer though, as I think it's possibly more than a throwaway concept.

## Refactoring

I've now split out my prototype codebase into a set of git submodules, and my projects into
another set of git repos, and moved hosting. I've probably re-done this three times now this
week, but I'm finally happy with the structure.

Unity has a single directly location for all assets, called Assets. This means any submodules
need to be imported under this location, so I end up with a full repo copy of my submodules
for each project - not the end of the world. I could potentially work around the multiple copies
issue with symlinks, but what I've got works well for me and I've got plenty of disk space (for now).

My top level repo is projects (under /repos/projects). Each project it included in this as
a submodule itself, e.g. repos/projects/scanner, repos/projects/portals, etc. the submodule
master copy lives under repos/shared/whatever, and then gets pulled into the respective project
under the Unity folder, e.g. repos/projects/scanner/scannerUnity/Assets/submodules/...

This might seem over-complicated for a couple of throwaway tech demos, but it means I
can spin something up in a few minutes that brings in Tango, OVR, Vive, Strange, Rewired,
etc (with all my changes as required) and the relevant core systems I'd like to use in the next prototype.

I'm nearly done dragging out the three primary demos that existed in my original core
prototype codebase into their own projects, along with their own UI and flow control paths.
I should be mostly finished this early next week.

## 360 video

After a chat with some old workmates, it looks like there's value for more than just myself
in learning how to produce and release 360 videos, so I'll be spending some time on that next week.
While I'm not a big fan of 360 photos and videos myself (they're better than 2D, but monoscopic
360 isn't really VR, and stereoscopic 360 without positional tracking isn't much better) - the
current personal device landscape (mostly phones and tablets) means that
until VR becomes considerably more prevalent, the best most people will get to see will be the
worst VR has to offer; 360 monoscopic content.

I'm going to spent a little time to see if I can capture content live from my demo apps to
a sharable format, as the existing videos I'm sharing only capture the eye view of what I'm seeing,
and that's hardly representative of the actual experience.


## Next week

Hopefully a lot more sun! I'll also be getting the portal prototype spun out into it's own
app, and bring controller support into the core framework in preparation for networking tests.








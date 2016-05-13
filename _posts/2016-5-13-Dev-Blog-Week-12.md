---
layout: post
title: Dev Blog - How to build a holodeck, week 12
category: DevBlog
tags: DevBlog, weekly
keywords: 
---

I've spent a big chunk of this week looking at 360 video, plus
I got Photon networking dropped into the Portals prototype. Videos
below!

## TL;DR

[Week 12 - networking](https://www.youtube.com/watch?v=Qo3dGY-96R4)
{% include youtubep.html id="Qo3dGY-96R4" %}
[Week 12 - shared space](https://www.youtube.com/watch?v=VkvR9RD2OLw)
{% include youtubep.html id="VkvR9RD2OLw" %}
[Week 12 - 360 video](https://www.youtube.com/watch?v=YubznG1aKIg)
{% include youtubep.html id="YubznG1aKIg" %}

## 360 video (and stills)

While I'm not a big fan of current 360 videos, I realised that I knew
very little about the process of creating and capturing 360 images and
video, so there was an opportunity to educate myself.

I've managed to get my hands on a [Theta S 360 camera](https://theta360.com/uk/about/theta/s.html)
which seems to be about the cheapest 360 camera you can lay hands on right now
that produces (somewhat) acceptable quality. You can spend hundreds of grand
on kit if you want, and processing the resulting frames (still or video) is
also a bit of a labour of love right now. The third video above is my third
very quick capture, which I almost managed to process correctly. The Theta S
software only allows for editing on an attached smartphone at the minute, but
at least the file formats are standard, so you can take files off the device
and process them in the normal tools.

Stitching, colour/exposure calibration, orientation, all the other things I've been fighting
with in the environment capture prototype - they are all issues in capturing
video from multiple cameras at the same time. Google has gone so far as to create
a whole product around this, called [Jump](https://www.google.com/get/cardboard/jump/)
which provides processing software to work with video generated from multicamera rigs,
including the [GoPro odyssey](https://gopro.com/odyssey).

The outputs of my Theta S are all mono photospheres, but the multicamera rigs can
generate stereo 360 content, normally in the
[Omni Directional Stereo or ODS](https://developers.google.com/cardboard/jump/rendering-ods-content.pdf)
format.
If you've tried out the Cardboard Camera on Google Cardboard, or any of the more explicit VR
content, you've likely been watching ODS video.

Viewing this content, in current VR headsets at least, isn't as simple as it should be.
It's getting there, but it took me a big chunk of time for me to find good viewer apps
and ways to watch the content. So far, the easiest method is to use
[Virtual Desktop](http://store.steampowered.com/app/382110/) which has a "360 videos" section where you
can paste a URL, and it'll then download and present the content.

The best examples of 360 captured videos I've found so far are the
[Jump world tour](https://www.youtube.com/watch?v=xPhdLz2Ebfw) video, and the most recent [Hellblade
teaser video](https://www.youtube.com/watch?v=fDyPppFLAlI), both of which are stunning
experiences, and both of which show off the shortcomings of the format (currently) which
are going to be tricky to overcome in the short term.

#### 360 video resolution

The Hellblade video above is 3840x2160 over-under ODS - so the entire image is split in two
vertically, and you're left with 3840x1080 per eye, each eye showing the full 360 degree * 180 degree
field around the observer. When you then look through each eye on (e.g.) the rift, you're looking
at around 400-500 pixels horizontally per eye, and maybe 500 vertically. This means the
resulting image is both heavily pixelated, blurry and (because you're watching video) full of
compression artifacts. On top of the artifacts the HMD display and optics introduce, the
whole experience is pretty grainy and chunky - nothing at all like what you're seeing in
VR (which is nothing at all like looking at real life, but it's a lot closer).

It's like going from HDTV back to an old PAL set playing back a dodgy VHS tape.

#### Lack of tracking

In fact, it's worse than that, because you're looking at an image that doesn't track with
your head. The orientation around in a circle (if you rotate your head and keep it level)
gives you depth, and that works excellently, but even rotating your head will highlight
that the tracking isn't working exactly as planned. For some media (again, most explicit
VR content right now) this is fine, as you're assuming a fixed pose for most of the experience,
but for things like real-world movies, game trailers and the like, you *want* to look around,
and even though the scene has obvious depth, it's just not quite right.

#### And yet - it's awesome.

Ultimately though, the experience is incredible, and shows where passive media consumption
is inevitably heading. Bump the resolution up 4-8x, and play back your favourite memory.

#### Content creation and editing pipelines

Capturing real-world content in Mono is kind-of there at a consumer level. Capturing ODS is
still not something anyone is doing down the pub yet, but that's (for me) the base-line of
where we need to be.

Capturing generated (rendered or realtime) content is currently a total nightmare, but with
NVIdia's latest drivers and [Ansel](http://www.geforce.com/hardware/technology/ansel) I'm
expecting a boom over the next year of people generating 3D trailers for their VR games.
It's pretty crazy that right now, on both the Oculus store and the SteamVR store, the
trailer videos for games are all in 2D. Expect some interesting moves in this space real
soon!

Generating the content directly to video is obviously where most people will be in the near
term, I'll be looking to find more compelling examples.

#### What next with 360?

It's been an interesting week catching up on this stuff, but I think I'm going to park it
for a little while, at least until I get on to ...

## Lightfields

One area of research that's high up my list but will need to wait until I've made a bit more progress
on networking, is Lightfield capture. There's a whole host of interesting research and products
I'm going to dig into in the next month or so, but capturing 360 photospheres is a good place to
start generating content. Look for more on this shortly.

## Networking

So, what else have I been doing with the week? Networking (finally), that's what! After
a couple of weeks of non-visible progress work (critical but crushing) I've finally got around
to dropping [Photon](https://www.photonengine.com/en/PUN) into the portals demo. The first
two videos show off mixing Rift, Vive and Tango in the same virtual space (and also in the same
real space right now, because I've yet to get a kit up and running in someone else's house!).

Having more than one Tango in a space seems to work ok, at least in my garage, although that
does lead to the possibility of nasty collisions. Put a Vive in the mix (with a cable) and people
are very quickly going to get damaged. At least the process works in practice. Vive lighthouses
don't seem to interfere with the Tango tracking, or at least not so badly the error is obvious
over and above all the other tracking issues I've got.

#### Tracking space alignment

I've yet to get the Tango ADF save and load functions to work properly, so I'm recording the
Area Definition on each tango individually currently, which means they're all out of alignment
and recognise different features. This means that two tangos held side-by-side think they are
50cm apart. That's fixable with a day or two's effort.

The Rift can be thrown into the mix by offsetting the tracking space, and with a load of manual
effort I've got it mostly lined up in the right place at the right height. I've got to go
through a similar process with the Vive, but ultimately I need some tools to help align tracking
spaces on the fly, otherwise this just isn't going to work in shared physical spaces. I'll
be thinking more about this in the next few months, I'm sure.

#### Networking data

I'm currently just chucking down a pos/ori node set for each head, and that's already highlighting
latency issues (I'm using Photon servers in the cloud, so there's a fairly large round trip, on top
of the local wireless network latency). It's visible when demoing locally, but I think it's acceptable
for remote work. I've also got some terribad interpolation code going on, which helps but doesn't
remove all the jerkyness. I need to dig into how Photon works a bit more to understand the data
stream rates, that sort of thing. Lots to learn here.

#### Voice comms

The next obvious thing to get in is Voice chat. I've not tried it yet, but Photon has a voice addon
which looks like a great candidate, so hopefully I'll have that working next week, and I can
look at doing some remote tests with floaty heads.


## Next week ...

Voice comms, then taking a Tango out on some visits to capture some other locations. Being able
to step (not walk) from my house to another house and visit a friend is the goal.





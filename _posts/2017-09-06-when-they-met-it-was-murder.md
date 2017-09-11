---
layout: post
title: When they met, it was murder
category: DevBlog
tags: DevBlog
keywords: tango murder product ar google apple development virtualreality
---

# A tale of Tango, ARCore and ARKit

That's right - It's time for a heart to heart. A little bit of intimate conversation, if you will,
about how Google has effectively killed Tango by a variety of small cuts and a few big chops.

## Cast your mind back ...

A few years ago, I got my hands on something absolutely incredible - one of the second iteration
Project Tango tablets. It was so good, I quit my job (1). With in-built position and rotation tracking,
local spacial awareness and (best of all!) a frikkin laser (2), I very quickly realised that this
was going to be the future of mobile computing. A device that understands where it is, and can make
sense of the environment around you? Who's not going to want that?

## And then ...

The next year or so has been a real whirlwind, as I've been exploring AR and VR. I spent pretty much
an entire year just messing around with various pieces of kit as they arrived. First was the Rift, then
shortly after the Vive, followed by a procession of addons, RGB-D cameras, goggles, 3D cameras, input devices, you name it.
But the Tango has always had a special place in my heart. Inside-out tracking, SLAM and an untethered form
factor really are the future of both AR and VR, as will become quite evident over the next couple of years.

Then [Pokemon Go!](http://www.pokemongo.com/)
came out, and for some reason everyone went bananas over it, even though I found Niantic's previous
game [Ingress](www.ingress.com) more interesting personally. You could actually hear the lightbulb going on
in the mainstream media - sticking virtual stuff into the real world is cool, yo. The implementation may have
been ropey as all hell (compared to recent ARKit/ARCore demos) but people got it.

During that time, I'd made some fantastically fun VR and AR demos, with my favourites being a multiplayer tilt-brush
clone that you could use Tango as a viewer for. Realising that context is critically important for content,
I proceeded to dump a huge amount of effort into my environment scanning software, such that I could capture
static environments and then walk around them virtually in AR and VR.

## So what happened to Tango?

That's a great question. Around the time that Pokemon Go! came out, the Tango SDK release cycle started to go a bit
tits up. From being a monthly release cycle, and fairly well tested software, the SDKs started to become irregular
releases. Bugs were raised by myself and many others in the community, and they were often ignored, and occasionally
(mind-bogglingly) the functionality related to the bug would be removed. In fact, a few critical parts of the software
stack have rotted or been deliberately disabled, such as exposure control in the camera, up to most recently
the ability to actually acquire the frame from the camera at all using the default API. The fisheye camera was readable
on device last year, but on the latest hardware (Zenfone AR) you can't get access to that image.

### Non-existent support

These issues are frustrating as all hell to deal with in the best of times, but the support channels were simply
non-existent. Looking at the [Tango support page](https://developers.google.com/tango/support), the *primary* support
channel is supposed to be [Stack Overflow](https://stackoverflow.com/questions/tagged/google-project-tango).
I dare you to find an official response (go look, I'll wait) and those that
did happen were often weeks or months after the posts were made. This certainly isn't from lack of interest - there's
lots of developers trying to make things work, and failing miserably because the support simply isn't available to them.
The few people I did manage to engage with were often friendly, but just as often unable to help me resolve my issues.

There's also a [Google G+ group](https://plus.google.com/communities/114537896428695886568),
which is (again) filled with posts from external developers - showing off their apps,
asking questions, looking for support. The amount of engagement from official Tango staff is *incredibly* small, and
went from bad a year ago to invisible over the last few months.

It just blows my mind that this is the level of technical, programming, development support available from Google.
It's almost as though they don't have a clue how to do it properly, which just can't be the case. And if that's not
the case, then what's the motive for being so f**king inept at it? (3)

### Obsolete hardware

The Peanut hardware (the first Tango device) can be forgiven for being ropey, and the Yellowstone tablet (the second
Tango device, and the one I purchased four of) can also be given a bit of a pass. Unfortunately, it shipped with Android
4.4, right around the time Android 5.0 came out. And then Android 6.0 came out, and Tango was *still stuck on 4.4*.
"When is this getting fixed?" cried every developer. And do you know what the answer was? It was tumbleweed! Of course!
Not any kind of rational communication, just a complete lack of acknowledgement that it was an issue (and would remain
so until the hardware was explicitly moved into obsolete status).

As Android moved on, the Tango kit became more and more flakey - core services like Play Store and others would auto-update
to the latest shipped version, and then crash until they were reverted or disabled. Im the latter months of using
Yellowstone for development, I had to (not a word of a lie) press the "close service" button every 10-15 seconds
on the device, because something would be crashing that I couldn't disable. I was not alone, in that just about every
other developer was in a similar situation.

This was when the [Lenovo Phab 2 Pro](http://www.techradar.com/reviews/phones/lenovo-phab-2-pro-1322905/review)
became visible (in app analytics before any official communication was made), and
then finally there was an official post telling people "The only supported tango device from now on will be the Phab 2 Pro".

Fine says I, I'll get one. it's a 600 quid phablet that's too big to fit in my pocket, but hey, Tango's going places, I need
to keep up. Folks in the states had access to them months before I did, but I finally managed to get my hands on one,
fix up my [Scanner app](http://www.evryway.com/apps/evrywayscanner/) and various demos, and catch up to where everyone else was.

Now, Google and Lenovo are obviously *best buddies* because the amount of product support that came alongside the Phab 2 Pro
was awesome. No, wait, that's wrong - it was non-existent. The Phab (which is actually a great bit of hardware) shipped
with Android 6.0 just as 7.0 was shipping, and - can you guess? - Isn't ever going to be updated to 7.0. And it's not
Daydream compatible. And it's using last year's Qualcomm hardware. Did I mention it's insanely expensive?

So we're sitting on a tiny subset of devices that actually work, with the same old products that were originally touted
as cool at the end of 2015 (and some of the coolest ones don't now work on Phab 2 Pro).

And then we get to the [Asus Zenfone AR](https://www.asus.com/uk/Phone/ZenFone-AR-ZS571KL/),
which was released in the UK last month. It's now my daily driver phone, I love it.
Great performance, good battery life, and a heart-attack-inducing 800 pound price tag. And as the Zenfone AR is released,
the Phab 2 Pro unofficially moves to obsolete status. The Zenfone AR also supports Daydream - but not at the same time as
running the Tango stack. Because why would you want that? Why would you want positional sensing AND 3D rendering
at the same time? who knows. (4)

I get that this is all developer angst, but we're talking about consumer released products here (not devkits). purchasing
a device that then becomes unsupported for the singular thing that makes it stand out less than
six months later - not cool.

### Obsolete software

And then [Apple gets into the ring with ARKit](https://developer.apple.com/arkit/),
which obviously throws spanners into everything that Google are trying to
achieve, because Apple do the obvious thing of making it just use the existing hardware (cameras and all) for spacial tracking. It's
nowhere near as cool as Tango is, but it does the basic stuff that you need to make Pokemon Go! actually work properly.

So what do Google do? Double down on Tango? Of course not. They decide to rush a tiny subset of Tango into production
called [ARCore](https://developers.google.com/ar/).
And they do it in the most half-assed way imaginable - they take the core code from Tango,
[rip the guts out of it, rebrand it, and slap it back into production](https://developers.google.com/tango/).
It's such a half-assed effort that if you try and run it
on Tango devices, it won't work - the ARCore and Tango services can't co-exist (because they're basically the same service).

So not only is my Phab 2 Pro obsolete, now my Zenfone AR is obsolete too - I can't do ARCore development on it.

## You knew this was coming, right?

Yes. Yes I did. Talking to various folks, and from being in software development in large companies for the last couple of
decades including Disney and EA - I know how product development works, and I especially know the signs when a product
is being decapitated for non-technical reasons. Tango has shown every sign of being DOA during my time developing on it,
despite my hopes and dreams that it would make it out into the real world in enough numbers that the general public would
be able to get it.

It grinds my gears, but I knew this was coming. It's a damn good job I didn't stake my career on this. (5)

## What's next?

Well, instead of everyone getting to see the future right about now, we're going to have to wait a few years while
the mainstream media goes ditzy over mobile AR, and then realises that compared to mobile positionally-tracked VR it's
a pile of shite, and then realises that Tango was where it was at in the first place.

The laser sensor isn't essential to do most of the things I'd like to do, so as the hardware and SLAM stacks improve
and folks release new and cool synthesis techniques for photogrammetry and object recognition we'll start to see
much of the future begin to happen anyway.

And we're going to see a metric shitload of apps and demos with virtual things hanging in "real" space while they
slowly drift across your table, then disappear when you move your phone too fast.

And then, if we're all very lucky, we'll get to the point where you're carrying a device that can show you a 3D,
enhanced view of the real world with accurate tracking from global scale down to local scale. Shops and bars will
have product reviews and menus floating outside them, waiting for you to look. You'll see an arrow pointing to your
friend, over on the other side of the park. Everyone will have karma auras, and things will be good.

But we're not there yet. I'm not angry, I'm just disappointed.

## Footnotes

(1) Not really.

(2) Yes, IR counts. there were warnings on the box and everything.

(3) If anyone at Google would like to talk to me about how the adults do software development, please drop me a mail.

(4) this is LITERALLY the killer-app, and they blew it.

(5) It may appear that I've staked my career on this, but that's an illusion.



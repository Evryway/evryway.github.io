---
layout: post
title: Finding the Largest Interior Rectangle in a simple polygon
category: DevBlog
tags: DevBlog
keywords: Largest Interior Rectangle Simple Polygon Implementation Unity3d Mathematics
---

## Abstract

Often, a solution to a problem is out there - but a working implementation needs to be constructed to meet the needs of
the problem. This article details the process involved in solving such a problem, namely finding the largest interior
rectangle inside a simple polygon using C# and Unity 3D. There's some mathematics, some pictures, and a link to a fully
working implementation.

The largest interior rectangle in a simple polygon is a useful piece of information in many fields and applications.
While I was looking for solutions to the problem, I found articles relating to meat factories and t-shirt designs, as
well as the particular problem I was trying to solve - the largest rectangular space inside my VR room boundary.
As far as I'm aware, there is no trivial, fast solution to this problem, so this implementation might be useful. If you
do find it useful, and you improve upon it, please share the improvements!

I'm writing this article in the style of a journal entry, and will be discussing some of the issues I've found while
creating both the implementation and this article. 

## 1. Introduction

When I first started working full-time on VR applications in Unity back in 2016, many of the tools (both hardware and
software) were in a state of flux. Unity itself has changed many times in the intervening four years, including some
fairly fundamental changes in how you write code that works on VR devices. One of the largest recent changes has
been Unity moving away from built-in code that talks to specific hardware (for example, Oculus headsets) to using a
"Plugin" architecture, that allows manufacturers to add in their own code without the need for Unity to release a
new version of the Unity Editor whenever there are code changes needed for that VR hardware.

The motivation behind this architecture (which I will be calling "Unity's XR Plugin architecture") is good - and
the implementation is almost on par now with the previous way of doingthings (that I'm going to call
"Unity's Legacy VR architecture") One area that has caused me problems, however, is the Boundary data.

When a headset user sets up a Boundary (or Guardian) area, they are drawing out a region in space that's safe for them
to play inside. This normally helps the player avoid moving into unsafe areas - for example, running face first into
a wall, or down a staircase, or smashing their TV with their controller. This Boundary area typically comes in
two flavours; the raw "boundary data" (a wobbly line the user draws around the outside of the safe region) and
the interior "play data" (typically, a rectangular area inside the boundary).

Some of my prototypes use the rectangular area for specific reasons (for example, locking menus to the walls).
Unfortunately, the latest XR Plugins do not give me that data any more - I can only access the full
boundary data.

My first instinct was to say "That's fine - I'll work out the rectangular area myself. How hard can it be?"

It turns out - pretty hard. Distinctly non-trivial, in fact.

As I went through the process of trying to find a simple solution, I also went through the process of researching
how other people have solved this problem, and spent a fair few days looking at journal papers describing
those solutions. For many of the problems I've been trying to solve over the last few years, this is a fairly
standard process for me. I try and clarify to myself the problem I'm attempting to solve. I then try and learn
what it's actually called by everyone else in the world (which may or not bear a small resemblance to the words
and terms I am already aware of). Then I try and find working code examples (in C# first, as it's my current
favourite language - then in Python, then in any other c-like language, then in any other programming language,
then finally in some human language, normally with mathematical formulas).

This has lead me to a startling insight:

#### The best documentation for a solved software problem is a working implementation with source code.

There are *many* kinds of documents describing methods to solve mathematical and numerical problems, but
a working implementation not only tells you how to solve it - it does solve it.

To that end, as a solution to this particular problem for anyone in the future, I'm going to attempt to construct
a document containing that working implementation, in parallel with the algorithmic description.

This might sound like a very verbose way to describe yet another "here's a way to do this" post. Quite why
this is the typical formal approach to journal entries is something of a mystery to me, but that appears to
be the times we're living in - so here goes.

## 2. Background to the problem

The specific problem I'm aiming to solve is to take a set of points in a 2D plane which describe the boundary of
a simple polygon, and from those points, calculate the largest interior rectangle that is contained by that
simple polygon.

A [simple polygon](https://en.wikipedia.org/wiki/Simple_polygon) is a polygon which may be convex or concave, does not intersect itself, and has no holes.



There appear to be a variety of 











## That fateful, hateful moment is here. Oculus is now Facebook.

Yeah, I'm pissed off. And on the face of it, I'm being unreasonably angry. 

Hey, I know. It was obvious all along, right? Oculus really is just Facebook by another brand, has been for years.
Expecting Oculus *not* to use a Facebook ID to log in to your developer account, or
have access to multiplayer, is just plain crazy talk. Why so serious, Tim?

Except it wasn't always that way. 

Let's go on a quick Trip down Memory Lane, and look at what the world of VR was like when I first got properly interested.
Maybe that'll explain some of the (I believe justified) horror at the moment finally arriving. Buckle in!

## Oculus Rift - the first one.

In 2012, There was a Kickstarter for a device called the Oculus Rift. A lot of the good folks at BossAlien were, at the time,
super-stoked with the idea of actually playing around with a proper VR headset.

So, we backed the Kickstarter (to the tune of four headsets in total, if I recall correctly), sat back, and waited.
Around the end of August 2012, monies were taken from accounts, grins were fixed in huge smiles, and we all sat back and
waited a little more.

And waited.

But not too long, by Kickstarter standards - because on March 29th, 2013, the Devkits started shipping.
That's the [Oculus Rift DK1](https://en.wikipedia.org/wiki/Oculus_Rift#Development_Kit_1), to anyone in the 2020s - but of course at the time, like those in the Great War - there
was only one.

and it was INCREDIBLE.

[![Rift DK1](/assets/2020_oculus/dk1.jpg)](https://xinreality.com/wiki/Oculus_Rift_DK1)

640*800 per eye resolution.
3DOF tracking.
Looks like a brick under non-linear transformation.

The best thing, though?

It worked. It actually worked. It was a VR headset, it cost under $400 per unit, it did the stereo display thing,
and you could write software that would actually run on it.

Sure, it wasn't 6DOF. There were no controllers (unless/until you plumped for hydras, which were also INCREDIBLE).

And the day those devkits arrived was the day I realised that VR was actually going to happen (soon) and it was going to be awesome.
Because up until that point, it had all been personal science fiction - but it was now actually science fact. And I had one of them,
sitting in my lap.

2012 and 2013 were hella years for me, btw - I'm having to look this stuff up, because more important things than this
were making the daily rounds, but looking back on it, it's pretty pivotal none-the-less.

This is truly the stuff that dreams are made of, because while the functionality of that headset was terribad in just about
every way that mattered (FOV, framerate, tracking, input, latency, pipeline, platform support, controllers, ergonomics, 
oh my god the list is so long ...) It gave everyone a reference point and said "go." And all of those points have since
been addressed, in spades, in under a decade.

Crucially though - it had been financed by US. It almost felt as though it had been built by US. The collective US
that backed the kickstarter. WE, the people of VR-land. The ones who dreamed, and took a punt, and got lucky.

Carmack joined. "Crystal Cove" was discussed. Prototypes were prototyped. Eve Valkyrie was announced.

## Oculus Rift two - electric boogaloo

And then 2014 happened. Two things in VERY quick succession, in fact.

**March 19th 2014**, we got to see this :

{% include youtubep.html id="OlXrjTh7vHc" %}

That's right. DK2, my peeps. Oh man - the first, proper, awesome, 6DOF headset.

And then exactly one week later, **March 26th 2014**, we get the next update (#52):

### Oculus Joins Facebook.

Now at this point, every right minded person is recoiling, but still horribly, passionately interested into getting their hands
on a DK2. Because WE MADE IT, yah hear? it was OURS. But Facebook was buying it out from under us.

And if memory serves me, we didn't need to put in any more money at this point - we were going to get a DK2 at some point,
Facebook was about to drop a metric ton of cash into Oculus, Abrash was about to join ...

So what do you do? Do you sit tight and get a DK2, or do you take a moral position of "Facebook is a creeping literal evil,
helmed by an amoral billionaire who enjoys selling the secrets of children to the sandman - so I'm out" ?

This is a proper question, by the way. What would you do?

Because I sucked down my moral position, waited for my DK2, told people that this (inevitable) day would come and
we would all regret it, and then moved on as a staunch Oculus supporter. Oculus - NOT Facebook. Never Facebook. because
regardless of the money, WE had made this happen, and Oculus was OURS.

And the DK2 arrived.

[![Rift DK2](/assets/2020_oculus/dk2.jpg)](https://xinreality.com/wiki/Oculus_Rift_DK2)

And it was INCREDIBLE.

And then Elite Dangerous came out, and it worked on the DK2, and *oh my noodly stars what the hell is this am
I actually living in the future and flying a spaceship? spaceship **spaceship** **SPACESHIP***

Yes, I'm actually flying a spaceship. I'm sitting here at my desk, with a borrowed HOTAS, piloting a spaceship
out of a space station with a docking slot that's impossibly far above my head. I can feel the ice forming
on the windshield in front of me, and the lure of the dark is pulling me. I engage hyperspace, and arrive
with a visceral kick, right beside an enormous blue giant star. Warnings scream.

Someone taps me on the shoulder, and asks if they can have a go.

These moments, lost in time like tears in rain. And it was still only 2014.

It's very easy to ignore the creeping literal evil when it's not actively eating your face.

## And now?

Many things have happened in the intervening six years. Life has moved on for all of us. Brexit, Trump, COVID-19.
The Valve Index. PSVR. The Oculus Quest. Facebook hiring some of the best people in the world, and pouring literally
hundreds of millions of dollars into VR research and products. The Rift, becoming an actual product (CV1 for those who
had been riding the train all along) which was INCREDIBLE, before it became "just ok" comparatively,  before it
became an EBay collector's item. 

But let's not forget, behind all of this, the political machinations of the rich elite have continued to twist our
lives (for better or worse). And certainly since 2014, Facebook, under the guidance of Mr Zuckerberg, has actively
played a critical role in nearly every life on the planet.

Capturing your thoughts, messages, photographs, videos. Your children and your friends. Your ephemeral connections
to everyone you know, and the world around you.

And then selling that shit to whoever pays the most, especially people with an agenda for change, like Cambridge Analytica.
But if they can't find those people, then why not just sell into the product market to make sure you keep on participating
in the economy like a good little consumer.

I know, Facebook isn't the only one doing this. But it's certainly in the bad group. It's up there. It's active.

Then, consider that a VR device isn't a text message, or a photo. It's a virtual *everything* that consumes
and surrounds you, like the goddamn force except real. And the device you're interacting with can track *you*.
How you move. How you talk. Your reaction times. Your environment. Which finger you twitch first when you're being
offended. This data is incredibly valuable, and currently no-one is selling it wholesale. Yet.

And we're finally at the point where my Oculus account is required to become a Facebook account, and I have to
*actively* make the choice to re-enter the Facebook ecosystem to be able to continue to making the content I want to make.
And if I make that content, I'm *actively* recommending that the users of the content engage, and participate in,
that same ecosystem.

Am I angry? You bet. Am I complicit? Of course.

Do I have a choice?

Now there's a question for you.


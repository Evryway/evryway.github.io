---
layout: post
title: Finding the Largest Interior Rectangle in a simple polygon
category: DevBlog
tags: DevBlog
keywords: Largest Interior Rectangle Simple Polygon Implementation Unity3d Mathematics
---
This article presents a solution to the problem of finding the largest interior rectangle inside a simple polygon.
The solution is implemented using C# in Unity 3D. There's some mathematics, some pictures, and a link to a fully
working implementation.

## Abstract

The largest interior rectangle in a simple polygon is a useful piece of information in many fields and applications.
While I was looking for solutions to the problem, I found articles relating to meat factories and t-shirt designs, as
well as the particular problem I was trying to solve - the largest rectangular space inside my VR room boundary.
As far as I'm aware, there is no trivial, fast solution to this problem, so this implementation might be useful. If you
do find it useful, and you improve upon it, please share the improvements!

## 1. Introduction

One of the largest recent changes in Unity has been a move away from built-in code that talks to specific hardware
(for example, Oculus headsets) to using a "Plugin" architecture, that allows manufacturers to create, and update,
their own code without the need for Unity to release a new version of the Unity Editor.

The motivation behind this architecture (which I will be calling "Unity's XR Plugin architecture") is good - and
the implementation is almost on par now with the previous way of doingthings (that I'm going to call
"Unity's Legacy VR architecture") One area that has caused me problems, however, is the Boundary Data.

When a headset user sets up a Boundary (or Guardian) area, they are drawing out a region in space that's safe for them
to play inside. This normally helps the player avoid moving into unsafe areas - for example, running face first into
a wall, or down a staircase, or smashing their TV with their controller. This Boundary area typically comes in
two flavours; the raw "boundary data" (a wobbly line the user draws around the outside of the safe region) and
the interior "play data" (typically, a rectangular area inside the boundary).

Some of my prototypes use the rectangular area for specific reasons (for example, locking menus to the walls).
Unfortunately, the latest XR Plugins do not give me that data any more - I can only access the full
boundary data.

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
be the times we're living in.

I've lso creating a post describing the process of researching the solution, which I hope you find an interesting
accompanyment to this solution. 

## 2. Background

The problem I'm aiming to solve is to take a set of points in a 2D plane which describe the a *simple polygon*,
and from those points, calculate the *largest interior rectangle* that is contained by that simple polygon.
It's a subclass of the [Largest Empty Rectangle](https://en.wikipedia.org/wiki/Largest_empty_rectangle)
problem.

A [simple polygon](https://en.wikipedia.org/wiki/Simple_polygon) is a polygon which may be convex or concave,
does not intersect itself, and has no holes.

A rectangle is a four sided shape, with two pairs of parallel sides, each pair being the same length. (This
may seem obvious, but it's worth being clear what everything means!)

![LIR](/assets/images/lir/lir_1.png){:width="640px" height="480px"}

Figure 1: the largest interior rectangle in a concave polygon.

Figure 1 shows 

There appear to be a variety of different algorithms that solve variants of this problem, with related works
going back to the 1970s that I've found. One of the best papers covering the problem is written by Karen Daniels,
Victor Milenkovic and Dan Roth, titled [Finding the Largest Rectangle in Several Classes of Polygons][ref_1].

I'll discuss the solution and implementation of this specific problem in [part 3](#part3), but first, I think
it's valuable to talk about the bigger problem - researching papers on the internet.

### 2.1. Finding the correct research

Like many of the papers I've tried to read, this one is found as a PDF of a journal paper. Luckily, it's a 
Harvard paper, and there is a direct link available. Many of the papers that it references are not directly
available. If you're lucky, there will be a PDF freely available at a site such as
[ResearchGate](https://www.researchgate.net/about) or [ScienceDirect](https://www.sciencedirect.com/).
If you're unlucky, you'll run into a referenced paper that you need to pay for.

This chain of references is necessary to build the accumulation of knowledge required to understand the contents
of the paper. If you can't follow the reference chain, you're unlikely to be able to accumulate the knowledge.
Often, this is often termed the knowledge base, as though it's a simple foundation to build upon. It's really
much closer to a tree, with some form of a shared trunk of knowledge, and many twisting branches, often interpenetrating,
growing and spreading from that shared trunk.

### 2.2. Finding the correct terminology

If you don't manage to find a good starting point on your first (or second, or tenth) attempt, you may need
to change the terms you're searching for. Largest Interior Rectangle? Maximum Empty Rectangle? Biggest Interior
Polygon? Contained Bound In Polygon? Some or all of these may get you on to a branch of the research tree. If
you don't luck out on search terms, you might find yourself dangling on a tiny branch, hunting for a solution
that's just out of your grasp.

### 2.3. Errors and omissions

If you do manage to climb the knowledge tree


### 2.4. Mathematical equations

### 2.5. Other considerations

## 3. Solving the problem - Largest Interior Rectangle.
{: #part3 }

# References
[Ref 1: ][ref_1]

[ref_1]: https://dash.harvard.edu/bitstream/handle/1/27030936/tr-22-95.pdf

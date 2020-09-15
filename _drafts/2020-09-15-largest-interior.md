---
layout: post
title: Finding the Axis Aligned Largest Interior Rectangle in a simple polygon
category: DevBlog
tags: DevBlog
keywords: Largest Interior Rectangle Simple Polygon Implementation Unity3d Mathematics
---
This article presents a solution to the problem of finding the axis aligned largest interior rectangle inside a simple polygon.
The solution is implemented using C# in Unity 3D. There's some mathematics, some pictures, and a link to a fully
working implementation.

## Abstract

The largest interior rectangle in a simple polygon is a useful piece of information in many fields and applications.
While I was looking for solutions to the problem, I found articles relating to meat factories and t-shirt designs, as
well as the particular problem I was trying to solve - the largest rectangular space inside my VR room boundary.
As far as I'm aware, there is no trivial, fast solution to this problem, so this implementation might be useful. If you
do find it useful, and you improve upon it, please share the improvements!

![LIR](/assets/images/lir/lir_2.png "Largest Interior Rectangle"){:width="320px" height="320px" class="imgcenter"}

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

This article details the algorithm and implementation specifics. Parallel to this, I've also written an article
about the [process of solving this problem][solution], which you may find interesting.

## 2. Background

The problem I'm aiming to solve is to take a set of points in a 2D plane which describe the a *simple polygon*,
and from those points, calculate the *largest interior rectangle* that is contained by that simple polygon.
It's a subclass of the [Largest Empty Rectangle](https://en.wikipedia.org/wiki/Largest_empty_rectangle)
problem.

A [simple polygon](https://en.wikipedia.org/wiki/Simple_polygon) is a polygon which may be convex or concave,
does not intersect itself, and has no holes.

A rectangle is a four sided shape, with two pairs of parallel sides, each pair being the same length. (This
may seem obvious, but it's worth being clear what everything means!)

![Figure 1](/assets/images/lir/lir_1.png){:width="640px" height="480px"}
Figure 1: the largest interior rectangle in a concave polygon.

Figure 1 shows a concave polygon - a set of points (shown as white dots) connected via edges (shown as
red lines) to form a closed simple concave polygon. Inside the polygon, there is a rectangular region
showing the largest axis-aligned interior rectangle that does not cross a polygon edge or contain
any of the polygon points.

There appear to be a variety of different algorithms that solve variants of this problem, with related works
going back to the 1970s that I've found. One of the best papers covering the problem is written by Karen Daniels,
Victor Milenkovic and Dan Roth, titled [Finding the Largest Rectangle in Several Classes of Polygons][ref_1].
The level of understanding required to implement their solutions is currently beyond me, however. I've read
this paper through a few times now, and the necessary understanding still has not yet sunk in.

A brute-force solution is possible, but that process would be terribly slow (as it would involve testing
every vertex against every polygon edge for every possible variation of certain properties). One assumes that
if it was a viable solution, it would be documented and implemented - and the papers I have digested all discuss
the brute-force solution in terms of O(n^4) or O(n^5) - in other words, with the number of vertices I'm hoping
to work with (up to 1000) I would be looking at billions or trillions of calculations. 

A paper that I did manage to understand, and the one I used as a basis for this implementation, was written
by Zahraa Marzeh, Maryam Tahmasbi and Narges Mirehi, entitled [Algorith for finding the largest inscribed
rectangle in polygon][ref_2]. Taking this as a basis, I created a working implementation in Unity using C#.

## 3. Implementation

One approach to solving the problem is to divide the space covered by the polygon into an axis-aligned grid
of rectangles, and then find the largest rectangle formed from these sub-rectangles.

[step 1] requires finding the smallest area rectangle that contains the simple polygon.  
step 2 constructs the grid of rectangles, using each vertex of the polygon as the x and y coordinates for
the grid lines.  
step 3 optionally refines these rectangles (adding more rectangles, and hence more granularity to the resulting grid).  
step 4 scans this rectangle grid, and determines whether a rectangle is inside or outside the polygon.  
step 5 determines which rectangles are linked to (adjacent) other rectangles, in the horizonal and vertical directions.  
step 6 uses this adjacency information to calculate, for each rectangle, the largest area rectangle that can be
constructed by moving up and to the right.
step 7 iterates all interior rectangles, calculating the areas for the adjoining rectangle regions, and tracking the best one.

Each of these steps is simple to understand, and all steps can be solved in a linear fashion, feeding the results
from each step into the next.

## 3.1 Finding the smallest area rectangle








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
[Ref 1: Finding the Largest Rectangle in Several Classes of Polygons (Karen Daniels, Victor Milenkovic, Dan Roth)][ref_1]
[Ref 2: Algorithm for finding the largest inscribed rectangle in polygon (Zahraa Marzeh, Maryam Tahmasbi, Narges Mirehi)][ref_2]


[ref_1]: https://dash.harvard.edu/bitstream/handle/1/27030936/tr-22-95.pdf
[ref_2]: https://journals.ut.ac.ir/article_71280.html

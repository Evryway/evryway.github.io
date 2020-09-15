---
layout: post
title: A tale of two problems - finding the solution to Finding the Largest Interior Rectangle in a simple polygon
category: DevBlog
tags: DevBlog
keywords: Largest Interior Rectangle Simple Polygon Implementation Unity3d Mathematics Academia Papers Please
---
Often, a solution to a problem is out there - but a working implementation needs to be constructed to meet the needs of
the problem. This article details the process involved in solving such a problem, namely finding the largest interior
rectangle inside a simple polygon using C# and Unity 3D. 

## Abstract

Finding the solution to a software problem is often as simple as downloading a package, or cloning a repository.
Using someone else's hard work is a very effective way to solve some of the hardest problems. But what do you do
if you can't find a solution that already exists?

Sometimes, the answer is to create the software. This article talks about that process - researching existing
solutions, understanding details found in research papers, creating a working implementation, and finally sharing
that solution.

I'm writing this article in the style of a journal entry. The reasons for this will hopefully become clear to you
as the article progresses. I will be discussing some of the issues I've found while creating both the
[implementation][implementation] and the documentation for that implementation.

## 1. Introduction

When I first started working full-time on VR applications in Unity back in 2016, many of the tools (both hardware and
software) were in a state of flux. Over time, the tools have somewhat stabilised, but there are still moments when
a change breaks something fairly fundamental, and needs a proper solution. Unity's XR Plugin architecture changes
brought me one of those breaking changes - namely, losing access to some of the boundary data.

When the boundary data information coming back from the Unity API changed, and I no longer had access to the
"Play Area" rectangle, my first instinct was to say "That's fine - I'll work out the rectangular area myself.
How hard can it be?"

It turns out - pretty hard. Non-trivial, in fact.

As I went through the process of trying to find a simple solution, I also went through the process of researching
how other people have solved this problem, and spent a fair few days looking at journal papers describing
those solutions. For many of the problems I've been trying to solve over the last few years, this is a fairly
standard process for me. I try and clarify to myself the problem I'm attempting to solve. I then try and learn
what it's actually called by everyone else in the world (which may or not bear a small resemblance to the words
and terms I am already aware of). Then I try and find working code examples (in C# first, as it's my current
favourite language - then in Python, then in any other c-like language, then in any other programming language,
then finally in some human language like English, often with mathematical equations).

This has lead me to a startling insight:

#### The best documentation for a solved software problem is a working implementation with source code.

There are *many* kinds of documents describing methods to solve mathematical and numerical problems, but
a working implementation not only tells you how to solve it - it does solve it.

On the other hand, a badly scanned PDF of a paper detailing an abstract solution does not solve the problem.
In fact, it often introduces more problems along the way. And that is, of course, if you're lucky enough to
have access to the paper in the first place.

In this article, I'll detail some of the issues I've come across while trying to implement my solutions based
on the research of other people, and some possible ways they can be solved in the future. If you are considering
writing up a solution to a particular problem, please consider the issues I'll be raising, and see if there is
some way you can minimize them in your documents.


## 2. Background to the problem - researching a problem.

The specific problem I was aiming to solve over the last month (August 2020) was to take a set of points in
a 2D plane which describe the boundary of a simple polygon, and from those points, calculate the *Largest
interior rectangle* that is contained by that *simple polygon*. It's a subset of the
[Largest Empty Rectangle](https://en.wikipedia.org/wiki/Largest_empty_rectangle) problem.

A [simple polygon](https://en.wikipedia.org/wiki/Simple_polygon) is a polygon which may be convex or concave,
does not intersect itself, and has no holes.

A rectangle is a four sided shape, with two pairs of parallel sides, each pair being the same length. (This
may seem obvious, but it's worth being clear what everything means!)

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



[implementation]: {{link_to_other_post}}

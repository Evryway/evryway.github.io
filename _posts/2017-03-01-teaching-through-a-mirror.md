---
layout: post
title: Teaching through a mirror
category: DevBlog
tags: DevBlog, year1
keywords: VR teaching holodeck
---

## Presenting content in VR

At some point (hopefully soon) someone is going to create a virtual environment in VR
such that people can join, watch a presenter, comment or interact somehow, and gain value from
the experience. A canonical example I'll use in this context is a classroom, and the presentation
material here could be (again for example) a lesson on geometry.

Let's say you're the presenter. You want to be able to show the students some geometric primitives
such as triangles and squares, some axes in space, and perform operations on these items. Picture
interactions like [Fantastic Contraption](http://fantasticcontraption.com/) - (dragging, rotating etc)
but the vertices are all labelled with the coordinates, the coordinate system basis vectors are
present, etc.

You want to be able to annotate the world-space content, and maybe write up notes on a presentation
plane (analogous to a blackboard) such that the students can see the annotations and notes.

In a normal classroom experience, the first part of this is physically impossible (having geometry
floating around in space) but the second is typical - everyone's seen a blackboard or whiteboard,
and most have probably clustered around one, reading it or interacting with it.

All of this is do-able (and might form part of my next set of prototypes), but one interesting
aspect is, what does the student see of the teacher? Where does the content live relative to both?

In a normal classroom, you have a teacher sitting at a desk in front of an array of students. The
teacher looks out, over the students. The students look back, at the teacher, and most likely at
the blackboard on the wall behind them.

## Facing the issue

As a teacher, to be able to write on the blackboard, you must turn around (facing away from the students)
and modify the blackboard contents (write a formula, draw a graph, etc). At this point, you've lost
the face contact you previously had with the students.

If you simply draw the content in space in front of you, you can still see the students, but another
problem arises - the students will see your content from the other side of the space you're drawing in.
If you're drawing onto a virtual plane (or blackboard) in front of you, and the student is sitting
on the other side, they will see a mirror image of what you're creating.

Wouldn't it be awesome for them to see the same content, while still being able to watch you? And in VR,
that's trivial to achieve (at least in the context here where the teacher is one side of a presentation
plane, and the students are on the other side) - you can simply mirror all the content behind
the viewing plane across the vertical axis. The teacher can draw on the virtual blackboard, and you
can see them and their content as expected, at the same time.

## Sharing the space

Of course, another way to share the content is simply to share the space - both teacher
and student side by side (or cohabiting!) on one side of the blackboard. You're not getting that
facial interaction, though - which for one-to-many presentations is very important. How many
lectures or presentations have you been to where the presenter always faced away from you, and how
did that impact the presentation?

In typical classroom scenarios, you have one teacher and many students. If you're all sharing the same
space, what does that do to the experience? From the student's perspective, you could simply remove
all other students and interact only with the teacher (or ghost in the other students, potentially
basing the visibility on something like their interactions, who spoke last, that sort of thing).
From the teacher's perspective, if you have 30 students all standing right beside you, all overlapping
in physical space - how do you interact with individuals? As a student, how do you get the attention
of the teacher? (Do you just raise your hand, metaphorically or actually? Does the teacher select
from those with hands raised to promote to visible student status?)

## Watching a lesson

These questions are not only relevant for live interactions, but they're also relevant for recordings
of presentations or lessons. I've spent a good chunk of time in the last year reading white papers
(such a lonely thing to do in my garage) and watching youtube videos, while also working through
Khan Academy and Udemy lectures on various topics. Just about every time I watch these videos or slideshows
on 3D geometry, I think "wouldn't this lesson be awesome in VR". Another one on my todo prototype list
is to create a lecture covering some basic geometry concepts in VR that someone can watch at a later
date (and potentially interact with). Combining this with some live presentation aspect would be wonderful,
especially if you could present the interactions as well as the lesson - kinda like the Q&A value you
get at the end of some youtube videos of presentations.

To date, my favourite educational content in VR is the
[Apollo Experience](https://www.kickstarter.com/projects/1436197736/the-apollo-11-virtual-reality-experience-education),
and the team that created that are making a
[Titanic experience](https://www.kickstarter.com/projects/1436197736/titanic-vr)
next - I'm excited to see this, and I'm sure it'll be put together in a quality fashion (given how awesome Apollo was).
I think a mix between this quality of presentation and having someone who you could ask questions of would
be incredible.

Even for something like a Udemy video of linear algebra, though, I can see the value in the blackboard
being much larger than your screen, and the depth of the space being used for additional content - let
alone being able to interact with examples (teacher draws triangle on blackboard with the lesson
being triangle congruity - student can grab the corners of a triangle to move them around, triangle
goes from red to green when it matches - that sort of thing)

I'm going to continue to mull on this one while I work through my ICP implementation on Scanner - hopefully
someone else will knock this together so I don't have to ;)



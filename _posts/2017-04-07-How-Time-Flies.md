---
layout: post
title: How Time flies
category: DevBlog
tags: DevBlog, weekly
keywords: 
---

## Quiet in here, innit?

When I stopped doing my weekly updates, I expected that I'd be able to spend a bit more time and focus on
creating some content with meat in it, rather than a quick precis of the week before.

Then, on a random off chance, I ended up hooking some consultancy work in an area I'm particularly interested in.
It may have seemed remarkably quiet here the last couple of months, but that's because I've been heads-down working
on someone else's stuff. This is great from a revenue perspective, but terrible for progress on my own projects!

I'm lucky that I should be able to continue spending a day or two a week working on my own things, once I manage to climb
the mountain of tasks that come with actually having a viable business off the ground.

Hopefully I'll get the chance to discuss what I'm working on commercially at some point, but I'm keeping it under
wraps for now.

## Scanner and Tango

I've been working with the [Phab 2 Pro](https://www.youtube.com/watch?v=5KShuL6FbUA) for a few months now, and while it
is a great platform, it's just too damn big to use as my daily device, so I'm waiting (and waiting ...) for the
[Asus ZenFone AR](https://www.asus.com/Phone/ZenFone-AR-ZS571KL/) to get some sort of wider release - I think it could
be the device that finally brings a viable market to develop in. I've had around 40 purchases of the Scanner app so far,
which is bringing in just about enough revenue to buy ramen each week, but with two growing boys that's just not enough
to be my sole focus right now (hence the jump to a proper revenue stream elsewhere).

I still have a lot of hope, and faith, that this technology is going to be yuge this year, so I'm going to continue
making improvements to Scanner while I wait for the market to grow.

## Next up - pointcloud alignment

As per Christmas time, the two main issues with Scanner are pointcloud accuracy and colour correction. I've been reading
a LOT of white papers and other people's code over the last couple of months, looking at the best ways to approach each of these.
I spent some time last month putting in a first pass of ICP for point cloud alignment, but it's currently not remotely fast
enough to add as a realtime process.

One thing that's clear from looking at the results that I get is that the main source of inaccuracy in the clouds is
translational error (lateral drift) rather than rotational error. This means there's a couple of approaches that might be
much cheaper than ICP that will still give me decent results, so I'm going to get cracking on those next week.

If there is any interest, I'll write up the research I've covered so far learning about how to approach ICP - there's
a fair amount of heavy math here and even a simple solution requires good math libraries. As I'm writing Scanner in C#
and I like to have a good understanding of how things work, I've been writing my own versions of everything so far, but
when it comes down to fast matrix math calculations, you really need to lean on something else to do the heavy lifting.
My first port of call was [Math.Net](https://www.mathdotnet.com/) - it does everything I need to do (large matrix inverts,
eigenvector calculations, SVD, etc) but unfortunately as of right now I'm unable to get it running on Android - so I can
test things on PC, but I can't actually see it running on device.

I've also put in place a simple KDTree for closest point calculations - there's some good reference code / discussion on
implementing this [here](https://forum.unity3d.com/threads/point-nearest-neighbour-search-class.29923/) which I used for
reference, but googling is your friend here if you want to find better implementations - I've just gone for a super-basic
version for now. populating the tree is on the order of a few milliseconds for a 8K cloud, and neighbour queries are super-fast.
Compared to my first go around using brute force for closest neighbours, it's a crucial optimisation (as expected!)

Once I've got something working nicely, I'll do a proper writeup. Until then - enjoy!







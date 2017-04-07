---
layout: post
title: Multiple Unity Cache Servers
category: DevBlog
tags: HowTo
keywords: 
---

I've been promising an article that's actually useful for a while, and something that's been
really useful for me over the last few years is the Unity Cache Server. I've recently set it
up to work with multiple versions of Unity, so that I have different caches for each
version of Unity. Care about why and how? then read on!

## What's Unity Cache Server?

Unity stores assets in converted binary form under the Libraries folder of your project. Whenever
an asset is imported (the first time Unity sees it, and after each subsequent modification) the
relevant import binary result is stuck in that folder, named according to the GUID assigned to it
in the asset database (the number you see in the .meta file alongside the asset, assuming you have
visible metafiles turned on).

The cost of importing is pretty expensive, so having a copy of the data lying around is a great thing.
As long as you don't switch platform, all is good. As soon as you start switching platform, however
(for example, from PC to Android, or Android to iOS and back) Unity has an annoying habit of re-importing
everything from scratch. This allows for the same source asset to have platform-specific binary versions,
but Unity in it's infinite wisdom decided to put all of the output conversion data into the same location
regardless of platform - so as soon as you switch, everything relevant to the old platform becomes stale,
and a very expensive re-import is required.

If you're like me, and you're switching back and forth between platforms on a regular basis, this becomes
incredibly expensive time-wise.

Back in the old days, there were a couple of workarounds for this - one is to path the library folder to a
platform-specific symlink, intercept the platform switch, and re-path to the relevant data. Works, but
can be error prone.

The other (and much simpler) option is to use [Unity's Cache Server](https://docs.unity3d.com/Manual/CacheServer.html)
which keeps all the relevant assets in a separate cache directory. When you switch platforms, instead of
doing a full re-import process, the output binary asset is pulled from the cache server instead, and something
that potentially took minutes now takes seconds. Unity Cache Server used to require a pro licence, but I believe
it's now available for everyone to download.

If you're not using Unity Cache Server on your project, you should probably start - it takes minutes to set up,
and will probably save you that amount of time the very first time you switch platform settings.

If you work in a team of developers, then the cache server is even more of a time saver - not only do you
get the benefits yourself, but everyone else will be able to use the cached asset post-import, so they don't
pay any cost themselves for importing that new texture you just added to the project.

## Setting up Unity Cache Server locally

The cache server itself comes as a Node process which you start via a shell script or batch file of some sort.
on windows, this is the RunWin.cmd batch file, which by default will use a cache directory local to the
cache server executable itself. That's great for a simple setup, but actually you probably want to have
a bit more control over where the cache lives - that makes cleaning it up later a much simpler process.
The cache also has a default size limit (which I think is 50GB?) which may be much more than you need, or
it may be far too small for your project (or projects - you can use the same cache server for as many projects
as you want).

A better option is to feed some commandline parameters to the batch file, and the most important ones are

{% highlight bash %}
    --path <path_to_cache_location>
    --size <size_in_bytes>
{% endhighlight %}

and assuming you're using Unity 5, you should disable the legacy unity 4 cache too:


{% highlight bash %}
    --nolegacy
{% endhighlight %}

point the cache to a nice fat SSD, and you're good to go. 

by default, the cache server is set up to use port 8125 on the machine it's running on. You can change this
to any port you like with the --port <xxxx> parameter. If you're sharing the cache server across your team,
you can then point your local Unity to the relevant machine's IP and port, test the connection works, and
enjoy the speed benefits.

## That's all super-obvious, tell me something cool ...

So, the last couple of months I've been working on a project that has required hopping between multiple versions
of Unity and jumping platforms. One down side of the way the cache server works is that switching Unity versions
doesn't necessarily mean a new unique GUID for an asset, even if the binary output is different due to some
change in how Unity handles the import between versions. That's bad, because it means even if you have
the cache server set up, you can end up with horrible import times each time you switch between Unity versions
on the project (for example you have something running in 5.5.3, and jump back to 5.3.7 to check how it
should look, then back to 5.5.3 to fix it up, resulting in two lots of expensive re-imports).

It's a bit of a pain, but I've now got a process in place that lets me work around this. Multiple local cache servers!

I'm assuming that data between unity versions that have the same version number digits is probably reliable enough
to share the same cache. This means I need some way to tell Unity that, for each product version, it should point
to a version-specific cache.

One further stumbling block is that Unity (at least as of version 5.5.3) stores the cache server settings in
a single location in the registry on Windows - so you set it up in 5.5.3, then load 5.3.7, and 5.3.7 now points
to your 5.5.3 cache! not good. Hopefully Unity will have enough sense to change this, but fortunately there's a workaround.

You can pop some editor code in place that will be run when Unity first starts up your project, and it appears to be
run early enough that setting up the cache server properties can happen before any importing occurs, which means
it won't pollute the other version's cache data after a switch.

Here's the code I'm using:

{% highlight csharp %}

using UnityEngine;
using UnityEditor;
using System.Text.RegularExpressions;

[InitializeOnLoad]
public static class EditorStartupSettings
{
    // override cache server based on Unity Version, etc.

    public static string cacheServerIPAddress = "CacheServerIPAddress";
    static EditorStartupSettings()
    {

        // key cache server IP port to unity version
        int port_key = 123;
        int port_base = 9000;
        string ver = Application.unityVersion;
        var verre = new Regex(@"([0-9]+)\.([0-9]+)\.([0-9]+)([fp])([0-9]+)", RegexOptions.None);

        Match match = verre.Match(ver);
        if (match.Success)
        {
            int maj = Mathf.Min(9, int.Parse(match.Groups[1].Value));
            int mnr = Mathf.Min(9, int.Parse(match.Groups[2].Value));
            int mni = Mathf.Min(9, int.Parse(match.Groups[3].Value)); // cap at three digits
            port_key = maj*100 + mnr*10 + mni;
        }
        int port = port_base + port_key;
        var oldaddress = EditorPrefs.GetString(cacheServerIPAddress);
        var newaddress = string.Format("127.0.0.1:{0}", port);
        if (oldaddress == newaddress) return;
        Debug.LogWarningFormat("Changing cache server in Editor from {0} to {1}", oldaddress, newaddress);
        EditorPrefs.SetString(cacheServerIPAddress, newaddress);

    }
}
{% endhighlight %}

pretty simple stuff - the InitializeOnLoad attribute makes Unity run the static constructor on editor startup.
I then work out a specific port number based on the Unity product version (e.g. Unity 5.5.2 will map to port
9552) and set it in the Editor Prefs.

Outside of unity, I then have a selection of batch files to start cache servers for each version of unity,
all pointing to a unique cache path and running on the relevant port. Here's an example batch file:

{% highlight bash %}
TITLE UCache 552
cacheserver\552f1\RunWin.cmd --path X:\unitycache\Storage552 --port 9552 --nolegacy
{% endhighlight %}

I can now run as many cache servers locally as I need, one for each specific version of Unity that I'm loading
the project into.

One thing to note is that I *do* have multiple copies of the project locally - I have a clone of the repo for
each version of Unity that I'm working with, so everything is separate. I'm not sure how well this will work
if you are trying to load the same project directory into different versions of Unity back and forth, but I'm
pretty confident it won't be a joyful process!

I hope someone else finds this as useful as I do. I also hope that Unity realise that this setting should be
editor version specific, and make the hoop-jumping go away!






---
layout: post
title: "Low Power Mode"
---

The 12" Macbook pro is a super cool laptop, but it has two things that make Cryptovoxels run really slow:

* A weak GPU
* A retina display with many pixels

I just had a report from `Deiv` in the discord that the app was running smoother on his phone than on his mac, and asking if there was a way to run the engine in mobile mode on desktop.

And so now there is! [/play?performance=low](https://www.cryptovoxels.com/play?performance=low)

![](/images/posts/low-power-mode.png)

It enables mobile rendering mode, with a simpler skybox, lower view distance, stronger fog and less visual effects (no vignette). While I was there, I also call `engine.setHardwareScalingLevel(2)` to downsample the canvas that is rendered to. This gives an even greater speed bump, but causes the graphics to look like DOOM from 1993, which is actually a kind of cool aesthetic.

Anyway, if you're on a weak GPU, or you're getting a bad framerate and really want to stomp around at high speed, try running the engine in low performance mode. 😊
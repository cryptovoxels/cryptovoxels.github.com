---
layout: post
title: "Performance work"
---

I want Cryptovoxels to be buttery smooth. So fast and smooth that you don't even think of it as a game. It's just a really fast 3d webpage. No stutter, no lag, no waiting while big pieces of geometry page into the world. I want Cryptovoxels to be faster than google maps and load quicker than twitter. It's a long term goal, but I think it's doable. Here are the steps I've been taking to work towards it.

![](/images/posts/performance-leaks.png)
<cite>Heap allocations and garbage collection</cite>

## Threading

Javascript is a famously single threaded language, that means it can only use one CPU core at a time. But, using webworkers, we can run javascript in multiple threads, and then send arrays of data back between threads.

I use this already to do the voxel meshing on a seperate thread. Recently I moved polytext onto a thread as well. So these threads do all the complex math, and then format the data in an efficient format (floatArrays internally) to send back to the main thread.

## Better meshing

Meshing is currently done 3 times per parcel (once for glass, one for opaque and once to generate the collision mesh) using three different ndarrays - which is silly. It should be done in 3 passes of one ndarray, by the same thread, that is already warmed up to the voxel data. This data then needs to be sent back to the main thread as efficiently as possible and then sent to the GPU when we have time between frames.

## Job queues

![](/images/posts/performance-chunks.png)
<cite>Basic time-bound job processor</cite>

Previously, all features on a parcel were loaded synchronously. All-at-once. Which meant that if you had a lot of images or text or .vox models, the browser would freeze up until it had finished loading.

I now split any large jobs up into an array of tasks to complete, and then process as many tasks as we can in the time budget. Once that time budget for this frame is spent, we defer those tasks to run after the next frame. It's not perfect, there are still some tasks that take longer than 16ms, which causes dropped frames, but we're getting better and better at it.

Between threading and properly implemented job queues we should be able to prevent pauses due to slow or expensive code running on the main thread.

## Babylon.js tweaking

Babylon has a whole page on [optimizing your scene](https://doc.babylonjs.com/how_to/optimizing_your_scene). I'm slowly working through all the steps in there. It's worth keeping in mind that Cryptovoxels is a bit different from other babylon.js games, in that all the content is built in world by other game players, and we don't do any server side processing of the geometry, and also - all content it loaded on demand as you walk around the world. This means that lots of the pre-processing steps that would make things load faster aren't available to us.

I've already had to do some hacks like freezing materials and so on - but babylon.js has dozens of levers that you can push and pull to let the engine know how to render your scene quickly. So working my way through all these levers we should get faster and faster.

## Measuring

Testing on my macbook (with a radeon GPU), my thinkpad (with integrated graphics), iphone and oculus quest gives me a pretty good cross-section of performance on different devices. But I think with time I'll add some formal benchmarking code, probably using puppeteer so that I can detect dropped frames. That way we could have a subset of the world that you could run as a test suite on your own hardware, and it'd let me know when the browser is locking up, and what we need to optimise next.

## Continual improvement

Performance is not a one-time fix. I implement features in the most idiomatic (lazy?) way, and often have to come back to them later to improve the performance. So as Origin City builds out, and new features are added, I'm sure we'll come across new bugs and edge cases to solve - so by measuring, tweaking, threading and optimizing, we'll work towards that perfect goal of 100% speed, 0 dropped frames, no hovercraft mode.

(Hovercraft mode is when it sounds like your laptop is going to take off because the fans are running at full speed). 🦑
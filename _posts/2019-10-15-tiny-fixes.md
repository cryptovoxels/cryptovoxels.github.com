---
layout: post
title: "Tiny Fixes"
---

I'm not sure if it's just a Cryptovoxels thing, but I find that it's always the smallest tiniest improvements that make the biggest difference.

I started a performance branch yesterday, that uses [tape](https://www.npmjs.com/package/tape) to render 240 frames using `requestAnimationFrame`, which should take about 4 seconds. In reality, while the world is loading, it takes at least 14 seconds to render these 240 frames, which means that while the world is loading, you get that thing where the screen is locked up and not responding to the mouse moving.

This is awful, really bad performance and a really bad user experience. You can't walk, you can't turn, it's like somewhere between your computer being locked up and having your head in a vise. Especially in VR, it means that the screen locks (you get that thing where the edges of your vision go black because it's attempting to warp the screen to match your head tracking, but the world is rendering so slow it can't keep up).

Anyway - so I'm trying to fix that this week. Move everything onto a thread, pump the main thread carefully and make sure I don't do anything slow on the main thread.

Probably fetch the parcel JSON on a worker as well, create the voxel fields, then pass the JSON back to the main thread to load the features after that.

Anyway - back to the simple tiny fix!

<video src="https://cdn.discordapp.com/attachments/431671342044020749/633395876143955986/loading-order.mov" autoplay muted loop></video>

I did two things here:

* Render a plain white material while the textures for the parcel loads
* Load the features *after* the voxel geometry loads

Which makes the world seem to load way faster for parcels with custom tiles.

But next up is to fix all those much performance bugs that are causing loading lag. Those are much harder, but at least now I've got my perf tool branch that gives me some metrics to work with (and improve).

☕️ This post bought to you by too much coffee and not enough focus. 🦑

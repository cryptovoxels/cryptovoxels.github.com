---
layout: post
title: "Press M to Move Features"
---

In cryptovoxels, anything that's not a voxel or an avatar is called a feature. The images on the wall, the big 3d text, the push buttons, particle effects. And the tool for editing features was really creaky. It was designed for laying 2d things on the walls, and until now, it hadn't really worked properly for the 3d features. After todays release, it now works amazingly well for editing 2d and 3d features, and I added the `M` key. 

Tap M then click on a feature to quickly move it around the world.

<video src="https://i.imgur.com/7f4sfNE.mp4" autoplay loop muted></video>

I also made a bunch of performance fixes (mainly using the `predicate` argument on `scene.pick()`), so now you may find that you can't go straight from parcel to parcel with editing enabled - instead you have to... Oh wait - I just realised how I can fix that. Ok - for now, you have to reopen the editing menu each time you go to a new parcel - but I'll make a fix so that you can walk from parcel to parcel with your edit menu armed.

Anyway - it's a great performance / functionality improvement, and I feel much more comfortable about creating more 3d model types for editing.

I also got to delete this comment:

![](/images/posts/m-to-move.png)
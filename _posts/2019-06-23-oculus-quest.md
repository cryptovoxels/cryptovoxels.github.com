---
layout: post
title: "Oculus Quest Support"
---

This is pretty exciting news, Oculus Quest support just dropped. It's very beta, but it works. Put your Quest on, load `cryptovoxels.com`, then click `enter in vr`.

<video src="/images/posts/oculus-quest.mov" autoplay loop muted></video>

## The quest is my #1 VR device

I've got a vive, a rift, a gear vr, and the quest. And I gotta say, the quest is my favourite. It's the only one that I think about killing some time in, or if I have some downtime, it is the mosts attractive. Not being tied to a computer is amazing. And compared to the Oculus Go / GearVR, the quest is so much more comfortable it's a world apart.

If you haven't tried the Quest you really should give it a go, it's something else man.

## WebVR support on the Quest is first class

The Oculus Browser comes pre-installed on the quest, and is really easy to use and nice. I had to do a bit of work to get the Babylon.js webvr support running nicely on the quest, and I disabled the default controls, because they are really weird on the quest controllers.

The controls are now, look and walk around with positional tracking, then cast a ray with your right controller and click `A` to teleport.

It's very basic. You can't see chat, you can't click on links, you can't use voice chat, you can't see the menu and you can't build. But you can see other users, and you can teleport around the whole city which is pretty amazing. The only content that is disabled is `Polytext` at the moment, since that often blocks for 3-4 frames and those frame drops feel really ugly in VR mode.

I think I'm also causing too much garbage collection and tracing the teleport ray against too many meshes (I should be using the low poly imposter to trace against), because it seems the headset is doing Asynchronous TimeWarp (ATW), and you can see black bars at the edge of your vision if you move your head too fast.

## Performance is Everything

So, my first priority with Quest support is to get it buttery smooth. 60fps, no judder. I've got it running pretty well in my development build, but it seems to get a bit more jittery when put up into production, so I have  bunch of research, measurement and development to do before the Quest support is as good as I want it to be.

After that, I want to work out how to log in on the quest (how do you get your JWT session token onto the quest?), then enable building. It'd be so cool to be able to fly around your parcel and shoot voxels, what an awesome way to build the world.

## Exokit?

Eventually it'd be great to make a native exokit build, that will have some native modules (probably for meshing), and use lots of threads and SIMD instructions for mad speed. This relies on Oculus's permission to publish Cryptovoxels on their store (I've already applied but they said no for now - until I can explain how the cryptocurrency aspects of CV will interact with in-app-purchases on the Oculus store), so it's more of a long term goal, but it's an exciting end-goal for the javascript codebase.

More VR support coming down the pipe. Next up: Using the thumbpad to walk smoothly instead of teleporting. 🦑
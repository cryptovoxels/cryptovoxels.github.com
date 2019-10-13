---
layout: post
title: "The Ultimate WebVR Setup"
---

Now that desktop and mobile are starting to look pretty good (other than performance issues, but that's a story for another blog post), I finally got some time to dig into the VR experience for Cryptovoxels.

![](/images/posts/webvr.jpg)

It's pretty terrible at the moment to be honest. I did a bunch of small fixes and pushed them on Sunday, so it's slightly better - and the performance lag means that you can only really run it on a Gaming PC, the Quest runs at about 30 frames per second, but I'm working on it. You can now navigate using the thumb joystick, and I've working on a search UI so you can navigate quickly in world. After that will be making the interaction ray able to press buttons and run scripts in world.

So there's a lot to do, but in getting my Rift and Gaming PC set up - I discovered the Ultimate WebVR Setup, that I'll be using for future development.

I have a Dell 3419W monitor, which is a 3840x1440 wide screen. It supports picture-by-picture, so it displays my macbook (on usb-c) on the left half of the screen, and my windows pc (on display port) on the right side of the screen. I then have my rift plugged into the HDMI port of the windows pc, and finally, I use [Synergy](//symless.com) to share the mouse back and forth between computers.

![](/images/posts/webvr-split.jpg)

This means that I can use sublime text to edit the code and serve the cryptovoxels client from the mac, and then move the mouse over to the right side of the screen to debug firefox. Firefox has pretty good WebVR support, so I can then enter the world using the rift and navigate around. And if I'm debugging weird bugs, I can just leave the rift sitting on top of my head, and it renders the same content in the Firefox window, so I can debug camera math stuff without giving myself vertigo if I mess up the maths while wearing the rift.

Anyway - it's a super good VR setup, and I'm hoping that with some aggressive performance work (a future blog post) and a few nice pieces of UI, it'll be a really fun and immersive VR experience.

Crypto-art galleries in VR. Nice. 🦑
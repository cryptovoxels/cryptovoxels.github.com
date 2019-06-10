---
layout: post
title: "Animated .GIF support!"
---

This one has been a long time coming, and was blocked on me working out how to convert a gif into a sprite sheet.

![](/images/posts/gif-support.png)

I finally worked it out, and with a bit of work on the new image server, and like literally 5 lines of code in the client, we have support for Bitcoin $4000 guy!

![](http://i.imgur.com/TKiAJWX.gif)

The trick was to take the .gif, run it through ffmpeg, then run it through montage (from imagemagick) and then you get a nice .gif spritesheet. In a quick hack, I made the spritesheet 1 dimensional (all images are appended on the x-axis). This turns out to be a bit of a image quality fail, because the maximum texture size is something like 4096px wide, so the individual frames get seriously squashed.

I’m going to add a call to a metadata endpoint so I can query the number of frames in the .gif, then I can configure montage to create a square montage with an equal number of rows and columns. This should give us nice high quality (well 128px by 128px jpeg quality) animated gifs at a super high speed.

Shout out to babylon.js for their observables API. Updating the texture offset before each frame was really easy.
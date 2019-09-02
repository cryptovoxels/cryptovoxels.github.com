---
layout: post
title: "Color Voxels and a Better Editor"
---

Today I released a feature that’s been kicking around for over a month. Support for full color tiles. If you have enough COLR (1 COLR per voxel), you can upload and use color tiles. Your favourite minecraft skin, the super mario tiles, or some hand drawn specialty tiles of your own.

![](/images/posts/color-tiles.png)

To place a COLR tile, you need to select the multi color palette option at the bottom of the tile menu, then select your color tile. Currently $COLR accounting is a bit out of whack so you may find you can place more color tiles than you have budget for, but that’s on my todo list to fix.

(Yeah, the tile / color tile / tinted tile UI is getting really confusing and weird, it’s on my todo list to refactor all that stuff, it’s pretty gross to be honest with you)

## In world tile editor

A big part of enabling this change was that I worked out how to atlas the tiles into one texture, in the browser - using the HTML5 canvas. In effect, this means that you can go to the tile menu, click ‘Edit Tiles’, and a pop up menu will appear with all the tiles you’re using the current parcel. You can then drag and drop tiles from your computer onto the tile atlas, and it’ll live update. So if you want to see what a wall will look like with a new tile, just drop the tile into your atlas and it’ll instantly update the wall.

![](/images/posts/atlas.png)

It’s a great way to experiment with new tiles and color schemes, without ever having to leave the world. Just remember to hit *save* when you’re finished editing, so that everyone else can see your new tiles.

The tiles are uploaded and cached by the image server ([source code](//github.com/cryptovoxels) and will be served by the CDN soon, so that your parcel loads quickly and reliably.

We’ve been using these monochrome tiles for a long time, I’m pretty excited to see what people get up to with full color voxels! :)


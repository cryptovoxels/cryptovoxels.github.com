---
layout: post
title: "Speeding Up Loading"
---

Cryptovoxels has just broken 1500 minted parcels, and has reached the threshold where we could no longer load the world in a single request, and instead had to break it up into a bunch of smaller requests.

Since the world was first created, the world client has been loading all the content in the world as one JSON blob. This includes all the compressed voxel data, but not the images and sounds and .vox files, which are loaded separately from a CDN.

At home on my 100mbit fibre connection I never noticed that this file was starting to get bigger and bigger, but at the office where the international bandwidth is a bit more constrained, it was taking 10-15 seconds to load the massive 20mb world bundle.

And the problem is only going to get bigger. The data in the world is only going to increase in size, so I started digging into the problem.

The actual world layout bundle is only 40kb of .json.gz, so that loads super fast. So we do that, and then fetch the data for each bundle with a seperate `fetch` request. The only problem is that this is a lot more load for the server, all these tiny requests, and if you were to fetch these smaller blobs from far away from the server (the server runs in the United States and I’m down here in New Zealand), it would probably have made performance worse.

So that’s where content addressable URIs and CDNs come in. Every time the parcel is loaded, we generate a `sha1` hash of the content in the parcel. And so when a user fetches the content of a parcel - they send the hash, and we can make sure they’re requesting the latest version. For example the fetch URL is:

    /parcels/:id/at/:hash.json

This also means that we can request these hashes through the CDN network - since each modification to the parcel generates a new hash, so if someone is editing their parcel and you’re reloading it to see the updates, you’ll fetch for the new `hash` (we send it to all connected clients via the websocket connection) and the CDN will fetch the parcel content from upstream at our server.

Anyway - it means the world view loads about 5x faster to first parcel on a slower internet connection down here in New Zealand, and is still lightning quick on a strong internet connection.

Next up I noticed some bugs around how long it takes the voxel content to appear, and it’s also seems like further away parcels are rendering before close parcels, there’s always more performance work to do. :D
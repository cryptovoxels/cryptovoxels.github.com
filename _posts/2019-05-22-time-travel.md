---
layout: post
title: "Time Travel"
---

In the tradition of adding awesome features in half an hour, this morning I added time travel to Cryptovoxels. If you go to your parcel settings page, you can see all the previous versions of your parcel, so you can review your build progress.

![](/images/posts/time-travel.png)

And - if you want to **revert to an older version** of your parcel, you can do that to!

This makes people much free-er to edit their parcel and try crazy changes, then decide they liked it better at the start of the day, and then revert back to that version.

![](/images/posts/time-travel-warning.png)

We've been storing parcel edit history since April, so far there are about 50,000 edits stored in the database. This is one of the advantages of doing this early development on Cryptovoxels in one big database, we can easily implement tools like this.

If we ever get to the future where we host parcels in dat:// archives, we should be able to give even finer grade revision tools.
---
layout: post
title: "Repackaging Garage Band 2011"
author: "Ricky"
tags: [OSX, iLife, management, munki]
header-img: "img/home-bg.jpg"
---

This Winter Break, some colleagues and I at Ohio University decided to embark on a completely modular workflow for faculty/lab/staff machines.  We know that this will be a time consuming, tedious process, but totally worth it.  This will _ultimately_ save us time and allow our Munki/MunkiServer environment to be utilized to it's fullest.

In the coming months, I will attempt to document the trials and tribulations that we have encountered, will encounter, and will conquer.  In this first edition, I will discuss repackaging Garage Band 2011.

Like most AppStore apps, GB 2011 is a no-brainer.  Download the latest _.app_, wrap it in a DMG, and upload to MunkiServer.  *Deploy!*  The hardest part is just making sure you're only deploying to machines that can actually use the software.  That said, a little problem happened when I deployed it on the first machine. Not so much of a problem but an annoying next step. The app installed and launched with no problem, but then I saw something like this: ![GarageBand Content Download](http://i.imgur.com/wdpbn.png).

While this might be fine for a faculty/staff member, we can't have this type of behavior in our labs or on classroom machines, so, what to do?  By firing up PackageMaker, I was able to find out that the downloader was caching a file named GarageBandBasicContent.pkg.  A quick google search and it pointed me to [http://downloads.apple.com/static/gb/gb11bc/GarageBandBasicContent.pkg](http://downloads.apple.com/static/gb/gb11bc/GarageBandBasicContent.pkg).  After downloading the large package, I wrapped it in a DMG, uploaded to MunkiServer, made it an update for my GarageBand installer, and we were off to the races.

Note: There is no guarantee that this file will exist on Apple's servers forever (and certainty not at that URL), but odds are pretty good.  And if you're wondering where the content get's downloaded, check out: <pre><code>/Library/Application Support/GarageBand</code></pre>


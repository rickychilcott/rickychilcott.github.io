---
layout: post
title: "Forcing Mac OS X Updates"
category: 
tags: [OSX, management, munki]
---

Our university is in the process of making our Mac OS X installs a little more enterprise-y with AD authentication, management via MCX, centralized software update servers, and Apple Software Updates on a regular basis.  In our journey to do the last thing on that list, I looked around to see how others were making it happen.

Plenty of times, I've used ARD to force a client to download and install all the updates, but I can't remember to do that regularly.  Moreover, what if installs need a reboot, or really, several reboots -- _it could be way out of date_.  How am I to know?

I found this in my search and it is a neat way to solve the problem [A script to install all required Software Updates](http://hints.macworld.com/comment.php?mode=view&cid=119150).  It's a bit hacky, but seems like it could do the job.  We could also modify the launchd tasks to run a certain times for labs and certain times for staff machines, minimizing user interruption and distributing load on our Apple Software Update servers over several time periods.

While this _could_ work, it's seems like the solution to only one set of problems.  What we need at our university is more of a holistic approach to Mac management.  Looking at [Munki](http://code.google.com/p/munki/), we might be able to solve many problems with one solution.
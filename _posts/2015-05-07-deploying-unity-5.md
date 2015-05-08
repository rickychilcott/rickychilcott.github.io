---
layout: post
title: "Deploying Unity 5"
category: 
author: "Ricky"
tags: [OSX, management, unity]
header-img: "img/home-bg.jpg"
---

The Scripps College of Communication teaches Unity for game development.  Over the past few years, we've been able to download the Unity from their website and easily deploy via munki.  Largely, there was no changes that needed to happen to the package, because the metapackage contained all the needed compontents.  Since moving to Unity 5, however, Unity has change the way they deploy the software.

When you download Unity, you now download a small .app called ```Unity Download Assistant.app```. This app is pretty tiny (less than 3 MB) but only contains a set of scripts that will download and install the packages.  Unfortunately, the scripts are not exposed within the Unity Download Assistant, so I needed to reverse engineer the installation process.  This blog post shares the coded needed to do so.

I wrote a script which (explained below) which will install the needed Unity 5 packages. To use the script, simply follow the following:

{% gist rickychilcott/99fb18b608f5223d383c use.sh %}

### How does it operate?

The download_unity5.py script does the heavy lifting.  The script, below, inspects the ```Unity Download Assistant.app``` installer looking for the ```./Contents/Resources/Settings.ini``` file for the URL to download another ini file.  This second ini, we will call the manifest file.  The manifest lists all Unity packages that need to be installed, where to download them, the md5 of each package, etc.  This file get's parsed, the packages get saved to a temporarily location and then installed.

This script must run at root since it will download and install the packages.  I hope it's helpful to you.

{% gist rickychilcott/99fb18b608f5223d383c download_unity5.py %}

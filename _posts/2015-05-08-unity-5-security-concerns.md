---
layout: post
title: "Unity 5 Security Concerns"
author: "Ricky"
tags: [OSX, munki, management, unity, security]
header-img: "img/home-bg.jpg"
---


In my last blog post, I talked about how to [Deploy Unity 5]({% post_url 2015-05-07-deploying-unity-5 %}).  While working on that project, I uncovered a small, but important attack vector that should be fixed by Unity.

As I describe in the blog post, I introspect the ```Unity Download Assistant.app``` for a Settings.ini file which yields some URLs.  This settings.ini file has 4 URLs, all of which are served over HTTP.  The first 3 URLs seem to work, but the 4th has been unrepsonsive every time I try. 

The bigger issue here is that these files are served over HTTP and the resulting packages are installed on users machines as a privledged user. NOT serving over HTTPS make the installer highly susceptible to a man-in-the middle attack and should be rectified ASAP. The Unity developer tool is installed on easily 10s of thousands, if not 100s of thousands of machines and Unity should fix the problem ASAP.

{% gist rickychilcott/cd66d7f97abd90c2d6f7 %}
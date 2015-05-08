---
layout: post
title: "Adding a User in Mac OS X Snow Leopard via Command Line"
author: "Ricky"
tags: [OSX, command line, management]
header-img: "img/home-bg.jpg"
---

Sometimes, it's nice to add local users to a computer via a script or the command line via ARD instead of the GUI.  In the middle of the quarter, I needed to add a local user to each computer in our lab that would have no password and be a standard user.  The reason is because we had some problems with Logic and our Network Home Setup -- something I'd like to post about later.  I did some searching around and found some code that worked in Leopard, but not Snow Leopard.  DSCL's (Directory Service's Command Line) syntax changed slightly in Snow Leopard, so I had to modify it to do what I wanted.


Here is an example of creating a local user by the name _logicuser_ that is added to the local directory service.


<pre><code>#Create a new entry in the local domain
sudo dscl . -create /Users/logicuser

#Create and set the shell property to bash.
sudo dscl . -create /Users/logicuser UserShell /bin/bash

#Create and set the user’s full name.
sudo dscl . -create /Users/logicuser RealName "Logic User"

#Create and set the user’s ID.
sudo dscl . -create /Users/logicuser UniqueID 503

#Create and set the user’s group ID property.
sudo dscl . -create /Users/logicuser PrimaryGroupID 20

#Create and set the user home directory.
sudo dscl . -create /Users/logicuser NFSHomeDirectory /Local/Users/logicuser

#Set the password.
sudo dscl . -passwd /Users/logicuser</code></pre>


Execute the above code, and you'd have a local user you can log into.


__Edit:__ Much later on, I learned that while this DOES work, it's not the best way.  Because there is no password for this user, it's not really that big of a deal.  However, if we wanted a password, we would be creating a user insecurely via the command line.  Imagine, someone sniffs your network traffic while issuing this command -- they now know your password.  To fix this problem, I suggest investigating the InstaDMG Create User package.  Some further resources for study include [InstaDMGs Source Code](http://code.google.com/p/instadmg/downloads/list), [InstaDMGs List Serv](http://groups.google.com/group/instadmg-dev?pli=1) and [AFP548 Forum](http://afp548.com/forum/index.php?forum=45).
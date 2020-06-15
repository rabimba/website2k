---
title: '“In order to continue the installation, please close the following application: iTunes” : Xcode Menace'
date: 2011-11-04T21:22:00.000-05:00
draft: false
aliases: [ "/2011/11/in-order-to-continue-installation.html" ]
tags : [Macintosh, Apple, Xcode]
---

  

Just when I thought everything was alright…I got “In order to continue the installation, please close the following application: iTunes” and it was showing after it completed almost 97% of the installation.

  

Yes….I was trying to install Xcode 4.1 into the Snow Leopard…

Developing app for MAC is something I always wanted to do,and now when I was just going to utilize my Apple Developer membership this stupid error cropped it's head.  
  
  

![](http://bencollier.net/wp-content/uploads/2011/07/Screen-Shot-2011-07-20-at-23.12.03.png)

  

I checked the dock bar, and iTunes wasn’t running at all. I also have an app called QuitsAppsMBI which is a handy tool for quitting applications, nothing on there to say iTunes was running. Lastly, I checked Force Quit to see if there was anything, and there was nothing in there at all.  
  
  
Not wanting to potentially ruin the installation, I wasn’t sure I wanted to just kill the Installer, so I seeked the help of Google to see if there were any suggestions on what to do. I came across the following post on James Greenhalgh’s blog: [http://james.greenhalgh.eu/2011/in-order-to-continue-the-installation-please-close-the-following-application-itunes](http://james.greenhalgh.eu/2011/in-order-to-continue-the-installation-please-close-the-following-application-itunes)

  

This post detals exactly the problem I was having, and a really simple fix! Open up Terminal (found in Applications\\Utilities) and type in the following command:

  

_ps x | grep iTunes_

  

This will list all the processes running on your computer with iTunes in the path. This returned the following for me:

_189  ??  S     0:00.04 _

_/Applications/iTunes.app/Contents/MacOS/iTunesHelper.app/Contents/MacOS/iTunesHelper -psn\_0\_57358  
2613 s001  S+     0:00.00 grep iTunes_

  

So this shows that the iTunes Helper is still running in the background. To kill this off, you then enter the following command:

_kill 189_

  

The first number from the first command is a process ID, so you’re telling it to kill the process with ID 189. Change the 189 to whatever the ID shows as from the first command, and it’ll end the iTunes Helper. After a few seconds, the Xcode installer will clock onto this and continue the installation!
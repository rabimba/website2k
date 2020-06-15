---
title: 'Get Google Glass on your Nexus (or in that case Android)'
date: 2013-05-28T13:26:00.000-05:00
draft: false
aliases: [ "/2013/05/get-google-glass-on-your-nexus-or-in.html" ]
---

[![](http://3.bp.blogspot.com/-JptofALCRSM/UaTxlLj_-yI/AAAAAAAAF6Q/ONai3mNrLmk/s1600/glass.jpg)](http://3.bp.blogspot.com/-JptofALCRSM/UaTxlLj_-yI/AAAAAAAAF6Q/ONai3mNrLmk/s1600/glass.jpg)

  

Guess we all are interested about Google Glass. Pretty interested I might say. And all the more since the Glass Explorer prototypes started making its way to the dev community. Last day while reading a idea gist about what might be some good things to implement in glass fro Wikimedia I was pointed to the Glass Viewer in Google Glass Developer portal([Playground](https://developers.google.com/glass/playground)).

  

And today I found a way to run Glass apps in my Nexus 4.

Thanks to Michael Evans(as he pointed that out) and Google we now have working factory images for the XE5 root.

Get them at [https://plus.google.com/114052868601022948953/posts/Y3bFHYp7tCZ](https://plus.google.com/114052868601022948953/posts/Y3bFHYp7tCZ)

  

The build process is also very detailed. 

And then we have another dump (which is very useful) from [AndroidPolice](http://www.androidpolice.com/2013/05/08/download-google-glass-xe4-and-xe5-system-dumps-please-do-something-cool-with-these/)

  

Now how would you like if these were repackaged as install-able APK's which you can try in your android?

  

  

Google Glass's build process is fairly conservative - they don't use hidden APIs often, and when they do, they use reflection. Thus, it is relatively easy to repackage the Glass APKs for other devices.

  

### Modifications to the base APK

The use-library element in AndroidManifest is removed, as it refers to unused code.

com/google/glass/hidden/HiddenViewConfiguration.smali is patched to always return 0xffff instead of calling the nonexistent View.getDeviceTapTimeout

An instructional video (don\_doff\_background.mov, 8MB) is removed to save space.

All native libraries required are shipped with the APK, as are all the Glass fonts.

For the camera, instead of calling Camera.open() to get the rear facing camera, Camera.open(0) is called to get the first camera, as the Nexus 7 doesn't have a rear camera.

### [](https://github.com/rabimba/Xenologer#install)So without Further Ado: Install

Download the APK:

Home: [http://goo.gl/JHIL2](http://goo.gl/JHIL2)

Camera: [http://goo.gl/7JDEs](http://goo.gl/7JDEs)

Maps: [http://goo.gl/Tb7av](http://goo.gl/Tb7av)

Setup: [http://goo.gl/32FXv](http://goo.gl/32FXv) This one's been modified so that instead of scanning a barcode, it uses the existing Google Account to setup and then force closes.

Install just like any other boring APK. None of the Google Glass apps need system privileges. I do not recommend installing these APKs as system APKs, as the Glass apps will attempt to reboot the phone after a force close.  
  
It works on both Nexus 4 and Note 2 (not tested by me).  
  
Everything including the raw image and apk and build process for these are in github.  
I'll update this post with the links very soon.  
  
Till then Go-Glass!!
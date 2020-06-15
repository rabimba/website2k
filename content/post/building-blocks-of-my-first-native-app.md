---
title: 'Building Blocks of My First Native App'
date: 2012-07-24T12:46:00.000-05:00
draft: false
aliases: [ "/2012/07/building-blocks-of-my-first-native-app.html" ]
---

![](http://blog.rimits.com/wp-content/uploads/2011/03/collage21.png)

  
  
  
  
A few months back when I was at the NASSCOM Tech-Unique (yes the second version of the [It-NIketan](http://rkrants.blogspot.in/2011/07/nasscom-it-niketanan-eventful-saturday.html) where I had to deliver a speech last time) it seemed the event mostly centered about how Mobile Web is emerging and how we should embrace it.  
In the discussion there we several interesting points raised and people started dragging PhoneGap in. While this was a very interesting topic, it disturbed me for certain reasons.  
  
  
I raised my worries, and unfortunately the speakers or the panel couldn't come to any solutions. So I am still at a loss for the cons of this method.  
Nevertheless I decided to put my mind out on the matter.  
  
  
I consider myself well-versed in web development, and I was excited about the features that PhoneGap brings to web apps. Going the HTML5 web app route seemed like the most sane route.  
  
  
**Pros**  

*   You don't have to learn any new languages if you're already a decent web developer
*   It's very quick to prototype
*   Though we didn't end up using it, jQuery mobile is pretty neato and makes it even faster prototype
*   Lots of library options for pretty much everything you could possibly want
*   It's really cool and fun
*   If you so wanted to, you can bypass the app store by hosting the files on a server, and utilize app cache to make things speedy. Changing your app is just changing a web page and its cache manifest file
*   Managing images for multiple devices is a lot easier with CSS and media queries than it is for an iOS xcode project and an Android project with its ldpi, hdpi, xdpi, and whatever dpi.
*   Easier to create vector graphics to design spec
*   Hell, it's just easier to get things to be exactly like the design (except if you care about cross-browser compatibility)

  
**Cons**

*   There are _a lot _of mobile browsers out there (the state of browsers is worse than its ever been in terms of how many different crappy ones we have to support - it used to be just one, but guess how many people are on android 2.x and wp)
*   There are _a lot_ of mobile devices out there with varying hardware, screen sizes, and network speed
*   Some features you're used to using aren't there for all devices (position: static for instance) and since those are likely the crappy devices, using a javascript shim (like iScroll) is out of the question if you care about performance
*   There seems to be some version issues with the facebook-connect plugin for phonegap (cordova) and the latest versions of phonegap on iOS only - To get facebook connect and PhoneGap to work I had to use an older version of PhoneGap
*   Documentation for PhoneGap itself is pretty decent, but it's still new, so not a whole lot of people have reliable information on current versions (at least this was the case 5-6 months ago)
*   Since I had to use an older version of PhoneGap, I found that some of their api functions would cause javascript errors. I had to bypass the sugar they provide and call PhoneGap.exec directly on their com.phonegap.whateverFunctionality - It was ugly, but it worked
*   There are complications with linking to other apps like Google maps
*   I found that saving contacts did not work on all versions of iOS
*   jQuery Mobile + Backbone is more of a pain in the ass than you think
*   Getting neato transitions can be a pain
*   There are less facilities in javascript for modularization of large-scale applications than Objective-C or Java

  

If your app is simple, then I recommend it. I really did enjoy the process and seeing my web app as an installed app. But, just know that it is more trouble than it appears to be
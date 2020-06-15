---
title: 'The curious case of MTA Fare and birth of "MTABonus"'
date: 2014-09-28T23:28:00.002-05:00
draft: false
aliases: [ "/2014/09/the-curious-case-of-mta-fare-and-birth.html" ]
---

Finally yesterday my 11th Firefox OS App got published in the marketplace. With a salt of surprise as well. Instead of taking weeks to get approved it took only a day to get approved. But then again I am not complaining, I get lucky like this time to times (but why didn't I get this lucky for the DVLUP submission.....but that's a story for some other day) and quite a lot of time hit roadblocks too.

  

So without further ado this is finally how the "App" managed to look like

  

![](http://2.bp.blogspot.com/-lRIpR9IZML8/VCjRg2XC3nI/AAAAAAAAUSc/KTAB4OBQAsE/s1600/1.png)

![](http://3.bp.blogspot.com/-OV6pMMV-Xr8/VCjRg1u82GI/AAAAAAAAUSk/y98-NibT5Rw/s1600/2.png)

![](http://2.bp.blogspot.com/-2iMpBEIZGiE/VCjRg6_IYeI/AAAAAAAAUSg/DZqm9Wm-oHg/s1600/3.png)

![](http://4.bp.blogspot.com/-obZm0nXz8E0/VCjRhAT8rjI/AAAAAAAAUSo/P5Ji_GGWPOo/s1600/4.png)

  

_History_: When I arrived New York almost three months back apart from the amazing city what amazed and delighted me was the transportation. Unlike most cities in United States New York _City _(there is a reason for that italics) has a very comprehensive and functional Public Transport system. And one that people use extensively. The famous NYC Metro and the Buses are run by the Metro Transport Authority. The idea is you buy a "MetroCard" and refill it (or have unlimited monthly/weekly ride) with certain amount. Every rife you avail will deduct the ride amount from the card. Not much different from what I had before in DART (Dallas Area Rapid Transport). But this happens with a twist, they award certain _bonus_ (http://web.mta.info/nyct/fare/FaresatAGlance.htm). After a couple of recharges this got me thinking. And it was an easy calculation to figure out how much and how many recharges I need to get a free ride (bonsu amount equivalent to one. But then again whats the fun of doing that? So one night being high on "Pure water from Genté Springs" quickly jotted down my calculations into this app (Yeah I am too laxy hence just wen ahead and used the FxOSstub).

  

Hence it was born.

So why suddenly this blog? I never really blogged about in of my other apps, not even about V.Translator which passed a 14K download mark this week. Well you say effect of spring water and to vent out how **_easy_** it is to build openwebapp. Really, it is so easy that I sometimes get worried that quite some amount of poorly written/optimized apps will make their way into the marketplace. Just like this one, if it had more functionality.

Also a reminder to myself that I should not cut corners next time. This was different than my most other app publications, most of which were fueled by either ego(why I can't do it)/api experimentation/app porting. This time though it was different.

  

So the confession **where did I cut corners?**

*   You see the upper left menu button? That actually doesn't do anything. I disabled (read commented out) the whole menu, but out of sheer laziness left that part. _Mental Poke 1: Never do that again_
*   See how there isn't any landscape screenshots? Because I disabled it. Not because I couldn't handle it. The app template itself is perfectly responsive and suitable for all sizes, but I didn't want to deal with scroll, hence...
*   See in the second screenshot how the **Feedback** is marginally overlapping the text? Well it's just a minor css overlap which is negligible _if_ the user could scroll. But the user can't, hence and annoying ux fail which i have to fix later \*sigh\*

Finally if you want to test drive the app

  

[![](https://marketplace.cdn.mozilla.net/media/img/mkt/badges/firefox-marketplace_badge-grey_129_45.png?b=839f3aa-5421ba55)](https://marketplace.firefox.com/app/mtabonus-calculator/)
---
title: 'IoT, Analytics and Data: A day with Intel Edison,GE and OpenWeb'
date: 2016-11-09T16:25:00.001-06:00
draft: false
aliases: [ "/2016/11/iot-analytics-and-data-day-with-intel.html" ]
---

Just a few days back on 25th October, I received an invitation to attend a Internet of Things workshop by Intel and GE Digital showcasing what edison and the predix platform could do. And I realized that’s pretty good chance to see what javascript and openweb can work and do in Tandem with it.  
So on a early morning of 25th October I hopped on to an Uber to go to “Work Lodge”. A nice little co working place in the middle of Houston and discovered

![img-alternative-text](https://lh3.googleusercontent.com/-FDj38LpQNfE/WCOiX61i6XI/AAAAAAABNfs/DFgeOE3Z42U/1478728113.jpeg?imgmax=9999)

![img-alternative-text](https://lh3.googleusercontent.com/-_n1F_kb7iUI/WCOiXtRHHZI/AAAAAAABNfo/dnZ8BS-4WtU/1478728137.jpeg?imgmax=9999)

![img-alternative-text](https://lh3.googleusercontent.com/-GJZxxilGn84/WCOiXu7ug2I/AAAAAAABNfk/197J5xy4oe8/1478728151.jpeg?imgmax=9999)

When that was over we started setting up for the workshop. The most interesting thing I noticed from the organizers were how they were planning to distribute the wifi among all the 60 participants.

![img-alternative-text](https://lh3.googleusercontent.com/-cozlzNYY0j8/WCOiXq5oRmI/AAAAAAABNfg/LkZMwPw95b4/1478729251.jpeg?imgmax=9999)

Pretty clever I must say. good way to distribute wifi load in a workshop, specially in one where everyone will probably connect atleast 4-5 devices to wifi (including the IoT board).

![img-alternative-text](https://lh3.googleusercontent.com/-kAFQ-wTsVp4/WCOiXQkY5iI/AAAAAAABNfY/kk0nFz1w24Q/1478729622.jpeg?imgmax=9999)

Then we satrted builidng our prototype and projects. Mostly what was used was Intel Edision boards along with a combination of sensors. I had used a combination of temperature,light and humidity sensor. And evantually what my project became was a time series analysis based on those data. That could effectively log the changes and act on any sudden change based on those parameters. I used the predix platform to quickly get it upto running. Some nifty python scripts I cokked up running in the edison board helped to get the streaming data into predix cloud where I did the timeseries analysis. There wasnt much more time This is how essentially it looks like in the dashboard with my 3 sensors and "wind turbines"  

![img-alternative-text](https://lh3.googleusercontent.com/-Obt3Y0_wGyY/WCOiXakC_zI/AAAAAAABNfQ/pOTXuuOA6eg/1478730091.png?imgmax=9999)

And the gig  

![img-alternative-text](https://lh3.googleusercontent.com/-atbR7T8cYY0/WCOiXd_qF4I/AAAAAAABNfc/SydWnYJVt1E/1478730123.jpeg?imgmax=9999)

This was pretty fun thing to do. And i got to enjoy a lot. I also made a lot of people go through the part of how you can connect it to IBM Watson and do a lot of stuff with that. Not being bound to any platform. Alos how to actually sanitize your data and send it to the platforms for analysis and still get the same kind of results predictions (essentially how do you sanitize whil keeping data mapping). This was all lot of fun and another reminder how IoT can help us do a lot of things.

At the end a glimpse of the audience

![img-alternative-text](https://lh3.googleusercontent.com/-F14yMLidiiQ/WCOiXfgu09I/AAAAAAABNfU/3xXLnl7y-tI/1478730325.jpeg?imgmax=9999)
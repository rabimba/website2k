---
title: 'Hackrice 2017 and HarveyTrack : How social media can help in disaster management'
date: 2017-10-17T12:03:00.000-05:00
draft: false
aliases: [ "/2017/10/hackrice-2017-and-harveytrack.html" ]
tags : [hurricane, harvey, social hack, hackrice]
---

[![](https://2.bp.blogspot.com/-Q5PGkvuK_Fs/Wd08ltTM0AI/AAAAAAABcy8/5cl9zl8Ad5w46q0NOcAZk5Eg2y8w1mWqQCK4BGAYYCw/s1600/front_page.png)](http://2.bp.blogspot.com/-Q5PGkvuK_Fs/Wd08ltTM0AI/AAAAAAABcy8/5cl9zl8Ad5w46q0NOcAZk5Eg2y8w1mWqQCK4BGAYYCw/s1600/front_page.png)

  

Each year Rice University holds an annual Hackathon for everyone to participate and code away their weekend. All the students who participate trade away their sleep for a weekend to build something cool in 36 hours and showcase it. That's how hackathons are and that's the thrill of it.

  

And I _love_ that thrill. I love taking part in Hackathons. It's a way for me to work on my ideas, hobby projects which I always wanted but never could, because of the classic time crunch of being a graduate student at Rice. Classes, Research and Valhalla take away most of your time and you hardly get enough time to work on your side projects.

  

  

My affair with _HackRice_ goes back to 2014 when I first participated in HackRice from Dallas and won the Mastery Of Computer Science award by the department of computer science. That kickstarted a snowball effect which is responsible for much of what I am today. But that story is for another day and demands another blog post all by itself.

  

This year HackRice 2017 was my fourth time participating in the Hackathon. It was also probably the last time I will be taking part as a student so it was special for me. HackRice had five tracks this year. And one of those tracks was The Hurricane Harvey track which dealt with designing any application that deals with Hurricane Harvey. Being one of the many people who got affected by the flooding at Harvey and having friends who were stuck in House for days, I decided it's the perfect opportunity to do something about it in the Hackathon. On a side note, you can see what happened to our apartment during the flooding in the video.

The prize from JPMorgan and Chase for the category on best hack of Harvey Disaster management using social media also encouraged me :)  
  
Motivation  
  
The motivation behind the concept was, people post a lot of updates to facebook and twitter. This [reddit thread](https://www.reddit.com/live/zhon9xy85b55/) was my own source of information. The hack was suppsoed to make it easier to dynamically encompass all these kind of coverage and then use keywords, filters and different statistical methods to make sense out of the data to actually create alerts and help victims and early responders withreal-timee data.

  

The Team

I am by nature a very lazy person and have a very curious relationship with working in any team. I have been told (by my advisor even...) that I function better in a team. But also when I have better autonomy. In short, the team works best if I am in a team with my friends. Having realized that I started the hackathon alone and kept bugging my friend [Avisha](https://dasavisha.github.io/) until she agreed to form a team,. She also is a graduate student at the University of Houston hence commute was not a problem for us.

  

The Hack

  

What we initially envisioned was a system that will be able to monitor the social media websites in real-time based on certain parameters. This will essentially be our dashboard which will suggest us what to monitor. And then with help of different set of crafted rules, we will drill further down. While designing the system, we decided to keep the monitoring parameters and "watchers" configurable so that we can change everything from the frontend. My previous encounters with different publicly available social media crawlers made me appreciate how blissful a good UI and configurability can be for crawlers. 

  

  

And eventually, we made Harvey Track. HarveyTrack is a web application for using social media and other resources to track incidents around the world in real-time. Events such as natural disasters or elections or crime, almost anything that people are talking about can be tracked.

HarveyTrack can retrieve data from several sources:  

*   [Twitter](https://search.twitter.com/) (tweets matching a keyword search)
*   [Facebook](https://facebook.com/) (comments from publicly accessible groups and pages)
*   [RSS](http://en.wikipedia.org/wiki/RSS) (article titles and descriptions)
*   [ELMO](http://getelmo.org/) (answers to survey questions)

  

[![](https://4.bp.blogspot.com/-jwbKOLFqmZw/WeY1rq_mFVI/AAAAAAABdKs/4-g4Xn5PODssBmrO-zQBI0fdbCSkVpXYQCLcBGAs/s400/Screen%2BShot%2B2017-10-17%2Bat%2B11.52.23%2BAM.png)](https://4.bp.blogspot.com/-jwbKOLFqmZw/WeY1rq_mFVI/AAAAAAABdKs/4-g4Xn5PODssBmrO-zQBI0fdbCSkVpXYQCLcBGAs/s1600/Screen%2BShot%2B2017-10-17%2Bat%2B11.52.23%2BAM.png)Items (called reports) from all sources are streamed into the application. Monitors can quickly triage incoming reports by marking them as relevant or irrelevant. Relevant reports can be grouped into incidents for further monitoring and follow-up. Reports are fully searchable and filterable via a fast web interface. Report queries can be saved and tracked over time via a series of visual analytics. 

  

  

  

Users can be assigned to admin, manager, monitor, and viewer roles, each with appropriate permissions.

  

  

[![](https://3.bp.blogspot.com/-QYOA3gdo-Uk/WeY1j5l7kdI/AAAAAAABdKo/txqC8ZwZ8X0E9gMVGKy6alEvtskrGyxwACLcBGAs/s400/Screen%2BShot%2B2017-10-17%2Bat%2B11.52.17%2BAM.png)](https://3.bp.blogspot.com/-QYOA3gdo-Uk/WeY1j5l7kdI/AAAAAAABdKo/txqC8ZwZ8X0E9gMVGKy6alEvtskrGyxwACLcBGAs/s1600/Screen%2BShot%2B2017-10-17%2Bat%2B11.52.17%2BAM.png)And we had the perfect testbed to use it in action. All of this was happening when Hurricane Irma and Jose was just leaving us. In our live demo, we could show the judges in real-time how monitoring global tweets using geo-boundaries helped us identify victims and early responders. Using our filters and keyword based heuristics we could further drill down and categorize _priority, SOS_ tweets and also tweets _offering_ help. Pairing that information with posts in facebook and feeds helped us triangulate their position and also keep a crowdsourced tab on the status of the neighborhood. This we felt especially was important considering when we were stranded in flood, we constantly kept monitoring twitter and reddit feeds to know the status. This tool just made it more comprehensive, easy to do that and also helped us to create automated alerts. The other aspect was to pair early responders with victims and that too was a must for us. And at the end we had a nice analytics which showed all this information in a bar chart and also overlayed on Google Maps. The useful thing that we were able to pull of was to differentiate between real tweets and retweets. That helped prune a lot of false positives.

[![](https://3.bp.blogspot.com/-Ly6EX8OOvMg/WeY1dM-EXOI/AAAAAAABdKk/gH9bley8d6sK7A1EaSrqR8nsr2BObDjUwCLcBGAs/s640/Screen%2BShot%2B2017-10-17%2Bat%2B11.52.08%2BAM.png)](https://3.bp.blogspot.com/-Ly6EX8OOvMg/WeY1dM-EXOI/AAAAAAABdKk/gH9bley8d6sK7A1EaSrqR8nsr2BObDjUwCLcBGAs/s1600/Screen%2BShot%2B2017-10-17%2Bat%2B11.52.08%2BAM.png)

  
We managed to run it from my localserver and got it live using localtunnel. Which really was a pain.  
You can still have a look at it here: https://f9f984bd.ngrok.io   
And our submission in DevPost with more details: https://devpost.com/software/harveytrack  
  
_What it can do_  
  

*   _Monitor FB, Twitter, any website and SMS channel for specific events (based on Source and Incident)_
*   _Can classify "Victim" and "responders" based on tweet. So if somebody posts "My basement is full of water! What should I do!" and someone else "My basement is full of water! But I have a boat! Take that harvey". It will classify the first one as **victim** and the other one as **able to help**_
*   _Utilize IBM watson for small magick trciks like stress analysis in text to rank which are most stressed victims and which area_
*   _Have a complete tracking system with option to assign different volunteers for different incidents_
*   _Handle huge amount of data. Our "Trump" filter enabled us to analyze more than 12k tweets per minute and it didn't carsh!_
*   _Of course everything is stored (in mongodb) for later analysis_

  
  
The Result  
  
  

[![](https://2.bp.blogspot.com/-lL0CyZZcvWU/WeYy-M7di8I/AAAAAAABdKY/X65j6K7OJN0-WYQi8IzeRbdcPzYxtQ03gCLcBGAs/s1600/21950820_1616427165074622_4484565606192382410_o.jpg)](https://2.bp.blogspot.com/-lL0CyZZcvWU/WeYy-M7di8I/AAAAAAABdKY/X65j6K7OJN0-WYQi8IzeRbdcPzYxtQ03gCLcBGAs/s1600/21950820_1616427165074622_4484565606192382410_o.jpg)

The two teams who won the two challenges in Harvey Track

  

We ended up winning the "[Best Hack for Disaster Response Using Social Media Data](https://devpost.com/software/harveytrack)" award from JPMC. HarveyTrack essentially became a real-time disaster tracking and response application.   

[![](https://3.bp.blogspot.com/-oUfaVZ3kJH0/WeY24LAB4ZI/AAAAAAABdK0/fa86GcPAMucIlVgjOKULX8Gc0ZfQoMtjgCLcBGAs/s200/Screen%2BShot%2B2017-10-17%2Bat%2B11.58.23%2BAM.png)](https://3.bp.blogspot.com/-oUfaVZ3kJH0/WeY24LAB4ZI/AAAAAAABdK0/fa86GcPAMucIlVgjOKULX8Gc0ZfQoMtjgCLcBGAs/s1600/Screen%2BShot%2B2017-10-17%2Bat%2B11.58.23%2BAM.png)

Or in fact, any incident tracking that you want to monitor in social media.

  

Avisha was already back in the home by the time the results were announced and so I got back home with a Bose Soundlink 2 as a prize for the hack. And overall being happy that the allnighter paid off.

  
  

**_Also, this was an important lesson for me. If we have a natural or man-made disaster. We don't always have to be a victim. We can use our skills to actually do something about it. I will be happy if this effort can contribute even 0.1% in that effort. If anyone wants to take it up or improve it further ir use it in a similar scenario. The code is always open source and you can get in touch with me to help you set up._**
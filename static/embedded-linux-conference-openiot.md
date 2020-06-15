---
title: 'SecurityPi@Embedded Linux Conference: One Device to Monitor Them All'
date: 2017-04-08T00:46:00.000-05:00
draft: false
aliases: [ "/2017/04/embedded-linux-conference-openiot.html" ]
tags : [MozTechSpeaker, Embedded Linux, ifelc, OpenIoT, Linux Foundation]
---

![](https://lh3.googleusercontent.com/-a1P7vHRXdrE/WOh5KHKm9cI/AAAAAAABTcg/HcwPpAjTAlU/s9999/Screen-Shot-2017-04-08-at-12.05.33-AM.png)

  

Linux Foundation hosts a few very prestigious conferences throughout the year, **Embedded Linux** and **OpenIoT** conference are among them. I first had my talks accepted in OpenIoT Summit last year, and I ended up presenting two talks and one with Dietrich (yay!). You can read about it [here](http://blog.rabimba.com/2016/05/openiot-summit-two-days-with-iot-old.html).

  

  

![](https://lh3.googleusercontent.com/-Gui1GKZ8Itk/WOh5JjHNACI/AAAAAAABTcU/LlTQXF5Paiw/s9999/Screen-Shot-2017-04-08-at-12.08.04-AM.png)

  

This year again, I decided to give it a try and submitted one of my hobby projects. The project uses a Raspberry Pi and tries to take care of its security and conveniently named as…..**SecurityPi** (Brownie points to me for the Innovative nomenclature!).

There are two parts of this post.  
First, I'll explain about the background of the project - **What is SecurityPi?** **How does it work?** **What is its purpose? And, how can you use it?**  
In the latter part of the post, I will talk about the conference, how the talk was received and a little about some future ideas that I am planning to work on as well as some suggestions that I got. 

### Inception ~ How it all began:

The idea admittedly came to me on a journey through London tube, talking to Dietrich while going for Mozfest 2016. After [Mozilla All Hands](http://blog.rabimba.com/2016/07/all-hands-2016-mozlondon-recount.html) and watching all those awesome projects come out from using devices like RPI, Arduino, Particle IO made me super excited.  
It also made me a little wary about the whole scenario where people quickly develop a prototype and deploy it, the system is connected to the internet and at the same time running software that is vulnerable to cyber attacks. In certain cases, the developers had not cared changing most of the default settings of the system they are running (damn most of them are configured using only root account in them with default password)!  
Later in [Berlin](http://blog.rabimba.com/2016/11/techspeakers-ahoy-berlin-meetup.html), at a closed briefing/meeting/discussion about some of the work Mozilla IoT team was doing (this was before open innovation), I got into a little debate where everyone was advocating for innovation and encouraging new communities to try new ideas. My point of concern - the idea of everyone introducing newer devices into the internet and keeping them open without any security, vulnerable to attacks by malicious hackers waiting to gain access and compromise these devices.  
This instigated me to start to write some pieces of scripts to better configure a Pi so that with every vanilla installation, a Pi can be configured better. But then came the attack of the refrigerators and that made me realize I actually have no idea what my devices are doing, what services they are connecting to. And I realized there is no way for me to have a central Command and Control to monitor them other than their gateway i.e. my router. Hence started my journey for **SecurityPi - **_one device to monitor them all_.

### Idea ~ How is the Job done:

What SecurityPi tries to achieve is what we have in our industry and organizations all the time. It acts as the IT Department - monitoring authority for the whole organization of devices at my home, connected to the internet. Almost all my devices including my cellphones communicate with the Internet via the Wifi connection. So SecurityPi will act as a doorkeeper sitting between my ISP and my Wifi analyzing all my traffic, looking for things I _generally don’t do_. And inform me about it (it won’t immediately block them unless I tell though).

**So what does SecurityPi do?**

> It tries to understand your activity with help from various service insights and tools. It eventually creates a profile on your devices service/data usage based on the service and servers they are connecting to. It know known bad service,domain,servers (again with help form outside) and updated about it. So if any of your device connects to them you get a notification. Over the time it creates a usage profile for you and your device data usage (but the device stores this information without sending it anywhere) and shows you a pretty picture of what is going on. 

> _It does not try to do machine learning on the data, yet…..not without you knowing_

### Making my R-Pi-Wi-Fi Awesome again:

To achieve this I consolidated my previous attempts and scripts, daisy chained them so that the RPIi itself doesn't get hacked in the first place (who watches the watchman? :( ). Then I got to make this big hack achievable. I had to do the following steps:

1.  **_Get the RPi in place_:** Networks are messy. There is no _easy and_ _cheap_ way to actually get the RPi (which only had one networking card) in between my router and Wi-Fi (I did not want to use the RPI itself as a WiFi adapter). I ended up using the _**In-Line approach**_.
2.  **_Know what is going on_:** Time for me to play the spy and understand what my devices (and me!) are doing. I resorted to using **_Bro_** for this. Bro was created by Vern Paxson in 1995 while at Lawrence Berkeley National Laboratory. What’s powerful about Bro is the ability to inspect traffic at all OSI layers, as well as add additional scripting for increased attack detection. Bro conveniently gives me an insight of the packets flying between the devices and internet. But just getting them wasn't enough.
3.  **_Make Bro great again_:** _"It seems nothing is as great as it had been once.."_. So I decided to do something about it. While Bro ships with an extensive signature base to detect a number of common attacks, the signatures can be enhanced with Threat Intelligence. Here comes the lovely _**Critical Stack (CS)**_ into the scene. CS from Intel (not Counter Strike :P ) instantly gave me insight and capability to understand and gain information about spam, malicious attack and phishing domains among other things. Now I had _knowledge,_ this combined with the _information_ Bro was giving me, and finally the RPi could understand what was going on. _Critical Stack_ is a free software that aggregates threat intelligence feeds. It’s a simple point-and-click integration to pull information, such as Tor Exit node IP addresses, known malicious IPs, or known phishing domains. The Critical Stack agent pulls the threat intelligence data, formats it into the Bro scripting language, and the Bro IDS picks up the new scripts automatically.
4.  **_But I wanted to see!_** And understand what is going on. I also wanted to get notified of any _potential_ bad behaviors. I wanted to know if and when a device inside my home connects to a TOR network, or a Chinese VPN or maybe sending periodic encrypted packets to a Russian server. I also wanted an audit trail and all this in a pretty UI. I may not be able to stop _you_ bad guys, but I sure as hell want to know when I am hacked and pull the plug (that I can do). Enter **_E**_lastiserach, L_**ogstash and Kibana (ELK) _**. The whole ELK also gave me a lot of analytical capabilities (and also told me how much of my bandwitdh actually gets wasted in NetFlix).

[![](https://4.bp.blogspot.com/-WA40YdFsaoc/WOh65fERa6I/AAAAAAABTcw/HV2ZplLYqWc3NliCm-RuwEq5EgMhS9YEgCLcB/s320/Screen%2BShot%2B2017-04-08%2Bat%2B12.52.47%2BAM.png)](https://4.bp.blogspot.com/-WA40YdFsaoc/WOh65fERa6I/AAAAAAABTcw/HV2ZplLYqWc3NliCm-RuwEq5EgMhS9YEgCLcB/s1600/Screen%2BShot%2B2017-04-08%2Bat%2B12.52.47%2BAM.png)

  

  

  

And that brings us back to what we started with.

I wrapped up all these again in another daisy chained bug hacky script which will take the pain out of installing configuring all these services into your RPI and create the system for you. That **became SecurityPi**. The kinks and my pain, all gets reflected in the presentation. Which you will be able to see below with the event video.

  

> [@rabimba](https://twitter.com/rabimba) talking about Security Pi and his [@Raspberry\_Pi](https://twitter.com/Raspberry_Pi) during [#lfelc](https://twitter.com/hashtag/lfelc?src=hash) [pic.twitter.com/Ks5gfvolzl](https://t.co/Ks5gfvolzl)
> 
> — Leon Anavi (@leonanavi) [February 22, 2017](https://twitter.com/leonanavi/status/834494462516531201)

All these combined allows SecurityPi to

> It tries to understand your activity with help from various services insights and tools. It eventually creates a profile on your devices service/data usage based on the service and servers they are connecting to. It know known bad service,domain,servers (again with help form outside) and updated about it. So if any of your device connects to them you get a notification. Over the time it creates a usage profile for you and your devices data usage (but does not send it to anywhere and stores it with you) and show you a pretty picture of what is going on. _It does not try to do machine learning on the data, yet…..not without you knowing_

The talk itself went great. With a ton of questions form people who generally build automative grade linux, embedded systems and also from DIY enthusiasts. I was super surprised, excited and happy that a lot of people are concerned about security of the IoT devices and how many of them liked to check out the code. My friend Leon who had his talk in the morning snapped a picture of me in the talk with too many people trying to snap the barcode to the github link.

> [@rabimba](https://twitter.com/rabimba) shows us the code for [@Raspberry\_Pi](https://twitter.com/Raspberry_Pi) at [#lfelc](https://twitter.com/hashtag/lfelc?src=hash) [#OpenSource](https://twitter.com/hashtag/OpenSource?src=hash) :) [pic.twitter.com/TbBGXkb6MH](https://t.co/TbBGXkb6MH)
> 
> — Leon Anavi (@leonanavi) [February 22, 2017](https://twitter.com/leonanavi/status/834494844475019264)

  

I also met with one of my professors from RICE University, Lin Zhong who was there and attended my talk. There was no planned afterparty and Portland was being the classic rainy city all these three days, but surprisingly I met with a lot of people after the talk and got a ton of suggestions on how this can be improved. _One being containerizing the setup, specially the ELK stack_.

![](https://lh3.googleusercontent.com/--Z2_l-SrEAU/WOh5KSk7vEI/AAAAAAABTck/8x9hUSMQ0ck/s9999/IMG_20170222_122842.jpg)

At the very last day, I met with Leon and went out to explore the city. We ended up grabbing dinner and then walking to Voodoo Donut to taste their famous donuts. 

_Fun Fact_: They only accept cash, so if Leon wasn’t carrying cash, we probably would have had to return.

  

![](https://lh3.googleusercontent.com/-aG_h3gjL-7Q/WOh5JxTTFGI/AAAAAAABTcc/-EFnscg-fiQ/s9999/IMG_20170223_232200.jpg)

Overall it was a nice fun filled three days. I enjoyed how the conference was organized and there were a ton of very interesting session spread throughout those three days. Got a ton of feedback on the code and moreover a clear actionable feedback on the talk itself.

![](https://lh3.googleusercontent.com/-Y9odMuiagic/WOh5J5BrYuI/AAAAAAABTcY/fFxtkMCLTt0/s9999/IMG_20170223_164548.jpg)
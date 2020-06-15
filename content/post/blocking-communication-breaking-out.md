---
title: 'Blocking Communication - Breaking Out'
date: 2019-08-06T12:55:00.001-05:00
draft: false
aliases: [ "/2019/08/blocking-communication-breaking-out.html" ]
tags : [censorship, blocking]
---

  

> I disapprove of what you say, but I will defend to the death your right to say it

If you have been following my [previous post](https://blog.rabimba.com/2019/08/blocking-communication-perspective-from.html) you will realize how quickly a state actor can just disrupt any kind of communication relying on a centralized telecom authority or Internet Service providers. Anything that can be threatened technically and legally can and will be used to block access to the Internet and communication mediums. Hence we need a solution that can circumvent these hurdles.

This blog post is inspired by the recent events happening at Kashmir, India and how repeatedly state actors in different parts of globes using laws to curb access to freedom of speech.

  

I present to you today: _**NoConnect**_

  

The idea first was envisioned at a Mozilla Leadership Summit back in 2015 at Singapore along with Priyanka Nag and a few more people(whom I don't remember anymore :( ). Then it took two years for it to come out to a prototype stage. And now this is in a stable enough stage where you can use this to reliably communicate with each other.

_What is NoConnect_
-------------------

NoConnect is a real-time messaging application like WhatsApp which does not rely on any traditional GSM/CDMA network or any kind of internet service to communicate with each other unlike WhatsApp.

### Motivation:

This was primarily envisioned to be used by NGO's and rescue workers and victims in areas where cellular and telecom communications have broken down. And the only way to connect and communicate is by Satelite Phones. This app could transform every mobile device to an off the grid communication device which does not need any kind of network.

  

The idea was heavily inspired by [Gotenna Mesh](https://gotennamesh.com/) without the need for any dedicated costly hardware.

### Features

*   **off the grid:** NoConnect doesn't need any internet or mobile network to communicate. Each mobile device with the app installed acts as a node and connects with each other using wifi and Bluetooth p2p network
*   **temp users:** All the users and usernames are disposable. Since it's not stored in any server or network. It's bound only to the device
*   **encrypted:** data streams between devices are encrypted
*   **p2p network support:** if you are part of a p2p swarm. You can communicate with everyone in that swarm even if they are not within your Wifi/Bluetooth range

The swarm makes it perfect for communicating between communities. And the nature of the network makes it resilient to any kind of censorship or attacks on the interception of messages.

A short guide on how it works

  

  

  

This was later submitted to the Equal Rating Innovation challenge and listed under the Technology section.

[![](https://rabimba.blogs.rice.edu/files/2019/08/Screen-Shot-2019-08-06-at-10.24.12-PM-632x338.png)](https://rabimba.blogs.rice.edu/files/2019/08/Screen-Shot-2019-08-06-at-10.24.12-PM.png)

### **India Version:**

I have just released a prebuilt binary which you should be able to just install and use right now in any Android Device. The release note gives a few more specific features probably relevant to the present scenario. I will also list them out here:

*   Complete off the grid communication. Does not need any network (GSM/CDMA) or internet at all. Useful for situations where communication Blackdown is active
*   Supports message broadcast. Useful for quickly sharing information to everyone
*   Complete anonymous messaging. You choose your username and it doesn't have to be unique. Not tied to any phone number or any information. If you are concerned, just remove your sim card and then use it. Will work fine
*   **Censorship Resistant**: Communications are end to end encrypted and completely off the grid. No way to monitor, intercept or block communication
*   **This version is backdated. You will manually change the date to two years back (2017) and it will work. The moment your network comes back alive and if you think you are under attack. the moment the date changes the app will lock itself regardless of if you give a password or not.**

#### [Download Here](http://bit.ly/noconnect)

  

> _This post will be updated with the technical specification of the mesh network and how NoConnect works. And also some more changes that are being worked on for the India version of the app._
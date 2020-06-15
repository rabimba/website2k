---
title: 'Sony Vaio E Series Touchpad Right Click doesn''t work in Ubuntu 12.04 LTS / Elementary OS'
date: 2014-11-14T18:31:00.001-06:00
draft: false
aliases: [ "/2014/11/sony-vaio-e-series-touchpad-right-click.html" ]
---

The past six months I had barely touched my own laptop. Thanks to the awesome server I was working on and the work laptop that T J Watson was so kind to provide me. My personal laptop seemed to slow and unresponsive compared to them.

  

Well after all I had a server with 16 Xeon Processor (so yeah each with 10 core) and a little more than 26 GB RAM to go with it. The laptop was nothing to compare with that, but it was a decent T430 with a awesome keyboard and decent processor+ram. But since I was approaching the end of my internship and the end of this vanity trip I thought better to go back to my own game and polish up my Vaio(SVE15118FNB) a little bit before I go back to it.

  

So I \*_again_\* followed my standard sanitation procedure and cleaned+formatted+duel booted the whole machine. And for a change thought I'll give Elementary OS a try.

  

The whole installation process was silky smooth and went without a hitch. The first time I booted the laptop, it had problem with the graphics though. But it vanished quickly when I installed the AMD Proprietary drivers(yeah I have a graphics card). But then I faced a new/weird issue.

  

I generally never had issue with touchpad drivers and even this time I didn't notice anything at first, but then realized......the right click doesn't work. No it just simply doesn't register as a right click but registers as a left click. No matter what you do what settings you change this doesn't solve. Even getting the synaptiks package manager won't do you any good. The mouse works perfectly well though.

  

So after days of head banging I finally came up with the solution and I am packaging it with this

This is only for kernel 3.2.0-24-generic-pae so I can't promise if it will run in any other system or not.

  

1.  Download the patch form [here](http://goo.gl/Dz3h45)
2.  sudo apt-get install dkms build-essential
3.  cd Downloads (I'm assuming you kept the downloaded file here)
4.  tar jxvf psmouse-3.2.0-24-generic-pae.tar.bz2
5.  sudo mv psmouse-3.2.0-24-generic-pae /usr/build
6.  cd /usr/build
7.  sudo chmod -R a+rx psmouse-3.2.0-24-generic-pae
8.  sudo dkms add -m psmouse -v 3.2.0-24-generic-pae
9.  sudo dkms build -m psmouse -v 3.2.0-24-generic-pae
10.  sudo dkms install -m psmouse -v 3.2.0-24-generic-pae
11.  sudo modprobe -r psmouse
12.  sudo modprobe psmouse
13.  sudo dkms status

If everything goes alright then the output should be something like this

  

fglrx-updates, 13.350.1, 3.2.0-51-generic, x86\_64: installed

fglrx-updates, 13.350.1, 3.2.0-70-generic, x86\_64: installed

psmouse, 3.2.0-24-generic-pae, 3.2.0-70-generic, x86\_64: installed (original\_module exists)

  

(it will obviously be a little different for you)

  

Now you should be able to use your hardware right click buttons. Restart is not required.
---
title: 'Installing Google Chorme into Linux MInt 12 (Lisa)'
date: 2012-03-18T08:16:00.000-05:00
draft: false
aliases: [ "/2012/03/installing-google-chorme-inti-linux.html" ]
---

I'm generally a Ubuntu/OpenSUSE user.  
I love both of these for the strong points they have. Recently though I decided to give the ubuntu variant Linux Mint a try before moving to Ubuntu 12.  
  
The experience with mint till now is pleasant. I did really like how it came integrated with most of the components I used to add later to Ubuntu.  
I also liked the Gnome3 interface (to some extent).  
  
And just when everything was merry I tried installing Google Chrome in it and voila!!  
The default debian installation package we get from Google isn't working here.  
  
So after a little bit of tinkering around I found a little nifty solution.  
  
Just one round of caution. The below steps require you to use Terminal  
  
After opening a terminal, the first thing we need to do is to download google’s signing public key and add it to the apt-key database.  
  

> wget -q -O - [https://dl-ssl.google.com/linux/linux\_signing\_key.pub](https://dl-ssl.google.com/linux/linux_signing_key.pub "https://dl-ssl.google.com/linux/linux_signing_key.pub") | sudo apt-key add -

  
Next, we’ll create an apt repository file for google under /etc/apt/sources.list.d called google.list.  
  

> sudo sh -c 'echo "deb [http://dl.google.com/linux/chrome/deb/](http://dl.google.com/linux/chrome/deb/ "http://dl.google.com/linux/chrome/deb/") stable main" >> /etc/apt/sources.list.d/google.list'

 Finally, we’ll update the repository list and download the package from the source.  
  

> sudo apt-get update && sudo apt-get install google-chrome-stable
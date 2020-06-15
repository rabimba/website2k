---
title: 'Nodejs on Ubuntu with the awesome "/usr/bin/env:node: No Such file or directory"'
date: 2014-10-28T19:32:00.000-05:00
draft: false
aliases: [ "/2014/10/nodejs-on-ubuntu-with-awesome.html" ]
---

Just when you are finished installing nodejs in your fresh shiny Ubuntu box and issue your first cordova create app command you get this annoying  
  
/usr/bin/env:node: No Such file or directory  
  
Which looks like this  
  

[![](http://2.bp.blogspot.com/-decHWOdjBFE/VFA0gBHQUDI/AAAAAAAAWFk/-gZK4bPIP0w/s1600/Capture.PNG)](http://2.bp.blogspot.com/-decHWOdjBFE/VFA0gBHQUDI/AAAAAAAAWFk/-gZK4bPIP0w/s1600/Capture.PNG)

  
And you think what went wrong.  
Apparently this stupid error is because you decided to do sudo apt-get install nodejs  
  
In short Ubuntu's default code repository renames node as nodejs to avoid some weird conflict. And you just got caught in between.  
  
Fortunately a one line symlink is enough to fix it for us.  
So just issue the following and you rare good to go  
  
sudo ln -s /usr/bin/nodejs /usr/bin/node  
  

[![](http://4.bp.blogspot.com/-JscBJfu4VYE/VFA1b58m_4I/AAAAAAAAWFs/q6udCjU-rEk/s1600/Capture.PNG)](http://4.bp.blogspot.com/-JscBJfu4VYE/VFA1b58m_4I/AAAAAAAAWFs/q6udCjU-rEk/s1600/Capture.PNG)
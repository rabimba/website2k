---
title: 'Increasing Virtualbox disk size (Increasing VHD size without cloning)'
date: 2014-06-03T13:44:00.000-05:00
draft: false
aliases: [ "/2014/06/increasing-virtualbox-disk-size.html" ]
---

  
![](https://images-blogger-opensocial.googleusercontent.com/gadgets/proxy?url=http%3A%2F%2F3.bp.blogspot.com%2F-ZNkGf0PvkSI%2FU44WCePB0sI%2FAAAAAAAAOOg%2FrzhQDx5Pa8M%2Fs1600%2F18iy7ekj9af3njpg.jpg&container=blogger&gadget=a&rewriteMime=image%2F*)[![](http://2.bp.blogspot.com/-73Jy1zLPEho/U44WCdq79rI/AAAAAAAAOOU/F3-Ey7H1WTc/s1600/virtualbox-logo-290x300.jpg)](http://2.bp.blogspot.com/-73Jy1zLPEho/U44WCdq79rI/AAAAAAAAOOU/F3-Ey7H1WTc/s1600/virtualbox-logo-290x300.jpg)[![](http://3.bp.blogspot.com/-gfqYFX9-SlU/U44WCbNPBeI/AAAAAAAAOOQ/oAkq5ikvwbM/s1600/virtualbox-logo.jpg)](http://3.bp.blogspot.com/-gfqYFX9-SlU/U44WCbNPBeI/AAAAAAAAOOQ/oAkq5ikvwbM/s1600/virtualbox-logo.jpg)  
Lets just face it, I like VirtualBox. I have used it in numerous occasions, back from the days when it was offered by Innotek, to Sun and now Oracle. Yeah it always was a less powerful than Vmware in some areas, but when i don't need them this was as good (or maybe sometimes better) than Vmware for my basic sandboxing needs!  
  
But sometimes I find myself in a problem which the GUI isn't always helpful for me. One of them is when in an active Virtual Machine I run out of diskspace.  
  
There are a number of ways to increase harddisk size without destroying your data, but most of them involve cloning or copying your data to a new vdi. Though they are also relatively painless I found a much more easier solution. Or rather a one liner  
  
The following command will operate on the VirtualBox virtual disk located at “C:\\Users\\rk\\VirtualBox VMs\\Windows 7\\Windows 7.vdi”. It will resize the virtual disk to 21920 MB (20 GB).  
  

> VBoxManage modifyhd “C:\\Users\\rk\\VirtualBox VMs\\Windows 7\\Windows 7.vdi” –-resize 21920

  
Which actually will look like the following  
  

[![](http://1.bp.blogspot.com/-C4fOQO5jklM/U44slfnKLfI/AAAAAAAAOPE/7gj7BFDXiGw/s1600/Capture.PNG)](http://1.bp.blogspot.com/-C4fOQO5jklM/U44slfnKLfI/AAAAAAAAOPE/7gj7BFDXiGw/s1600/Capture.PNG)

  
  
Then boot up the Virtual Machine. You have assigned the space but you won't be able to access it right now. So we have to make it accessible within the guest os.  
  
Open up Disk Management tool and it will look like the following  
  

[![](http://3.bp.blogspot.com/-C5YrvuWlcI0/U44tNvAPIUI/AAAAAAAAOPM/ieeFdConmTE/s1600/Capture.PNG)](http://3.bp.blogspot.com/-C5YrvuWlcI0/U44tNvAPIUI/AAAAAAAAOPM/ieeFdConmTE/s1600/Capture.PNG)

  
Just select the active drive and click Extend Volume. It will automatically extend it and you will have all the space you need  
  

[![](http://1.bp.blogspot.com/-D4NxW-l649Q/U44tnLUziqI/AAAAAAAAOPU/muM11c1V7Sg/s1600/Capture.PNG)](http://1.bp.blogspot.com/-D4NxW-l649Q/U44tnLUziqI/AAAAAAAAOPU/muM11c1V7Sg/s1600/Capture.PNG)
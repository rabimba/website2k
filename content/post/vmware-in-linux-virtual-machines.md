---
title: 'VMware in Linux : The virtual machine''s operating system has attempted to enable promiscuous mode on adapter Ethernet0'
date: 2014-08-05T11:24:00.002-05:00
draft: false
aliases: [ "/2014/08/vmware-in-linux-virtual-machines.html" ]
---

I was just happy when I transported my dev virtual box to my Linux system. But immediately after starting up the system I was greeted with this error  
  

[![](http://2.bp.blogspot.com/-0xGYDMqGhZc/U-ED8XyrbXI/AAAAAAAARjI/ptpjbdBJtcI/s1600/Capture.PNG)](http://2.bp.blogspot.com/-0xGYDMqGhZc/U-ED8XyrbXI/AAAAAAAARjI/ptpjbdBJtcI/s1600/Capture.PNG)

  

> The virtual machine's operating system has attempted to enable promiscuous mode on adapter Ethernet0. This is not allowed for security reasons.

  
Apparently the solution is [this](http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=287).  
  
Which states that "VMware software does not allow the virtual Ethernet adapter to go into promiscuous mode unless the user running the VMware software has permission to make that setting. This follows the standard Linux practice that only root can put a network interface into promiscuous mode."  
  
And the solution it seems is adding a new user group and deligating permission to them. However for CentOS this didn't turn out to be the case. Apparently device nodes are created in boottime in this case and you need ownership permissions for udev to make it work.  
  
You can read a detailed description in that link. But in short the commands which will solve your problem (and conveniently _absent_in the help article) are  
  
cp -rp /dev/vmnet0 /lib/udev/devices/  
sudo chmod a+rw /dev/vmnet0  
sudo chmod a+rw /lib/udev/devices  

  

As you can see here

  

[![](http://4.bp.blogspot.com/-WeirXLSO91w/U-EFO51orRI/AAAAAAAARjQ/aOwva1wBfkk/s1600/Capture.PNG)](http://4.bp.blogspot.com/-WeirXLSO91w/U-EFO51orRI/AAAAAAAARjQ/aOwva1wBfkk/s1600/Capture.PNG)
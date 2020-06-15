---
title: 'Firefox Add ons'
date: 2009-06-16T07:37:00.000-05:00
draft: false
aliases: [ "/2009/06/firefox-add-ons.html" ]
---

**How to make Firefox addons compatible with the newest release.**  
  
Everybody likes to try out the newest version of Firefox. At the time I was writing this Firefox 3.1 beta 1 was available. When you install it you will find some of your existing Firefox add-ons may have already been updated to work with the new version. Others won’t install at all.  
  
Don’t be surprised if some of the add-ons you modify to be compatible, bring Firefox to its knees. They don’t let you install older versions for a reason. But so I’ve had no problems at all.  
**  
Step 1 – Downloading the add-on**  
  
Locate the add-on you want to install. If it’s on the official Firefox add-on page you’ll have to click “See All version” to be allowed access to the .xpi. Right click on the now clickable “Add to Firefox” button and choose save target file as.  
  
**Step 2 – Extracting the add-on.**  
  
Locate the add-on you just saved. You should be able to open the .xpi file with your favorite compression utility. I use Power Archiver and it seemed to work just fine. Other compression utilities compatibility may vary. Extract the add-on to the folder of your choosing. I usually recommend extracting it to its own folder on the desktop.  
  
**Step 3 – Modifying install.rdf**  
  
Open the folder you just extracted the xpi file to. You’ll see a file called install.rdf. By default windows will have no idea which program to use to open the file with. You can either use notepad or WordPad.  
Once you have the document opened do not get intimidated by the amount of text that you see. I find it’s easiest to just do an edit / find and look for the word max. That should take you directly too  
  
“3.0”.  
  
All you have to do is edit what is between the > <. In this case it says 3.0. Change the number to the current installed version of Firefox. In this case I have Firefox 3.1 Beta 1 installed. Which is written out as 3.1b1. So when I get done, it should say  
  
“3.1b1”.  
  
I guess you could also plan ahead so you don’t have to edit this for every new release. You could probably change it to 3.1b4 or something in that nature.  
Once you have that change made, save and exit the file.  
  
**Step 4 – Recompressing the xpi file.**  
  
The method of recompressing it into a file will vary by the software you use. If you use power archiver or winzip, I would recommend you open the folder containing the extracted contents of the xpi file and do a select all. Once all the files are selected, right click anyone of them and click “Add to zip”. When you’re done you should have a file ending in .zip. All that is left is to rename the zip file (in XP you’ll have to make sure you can see file extensions) to the name of the xpi file you downloaded earlier. Just make sure when you are done that the file ends in .xpi and not .zip.  
  
That’s it. Now just open Firefox and drag the xpi file you just created into Firefox and choose install. Once you reboot Firefox your add-on should now function properly (hopefully).
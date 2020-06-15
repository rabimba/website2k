---
title: 'HackRice 7.5: How "uFilter" was born'
date: 2018-03-08T01:59:00.000-06:00
draft: false
aliases: [ "/2018/03/hackrice-75-how-ufilter-was-born.html" ]
---

[![](https://4.bp.blogspot.com/-C4YiA2Z12CA/Wp8v5Cao-fI/AAAAAAABqgA/9HdmNUiA9xAaqhG90TEVcWNwyonYLF1EQCLcBGAs/s640/Screenshot%2Bfrom%2B2018-03-06%2B18-18-24.png)](https://4.bp.blogspot.com/-C4YiA2Z12CA/Wp8v5Cao-fI/AAAAAAABqgA/9HdmNUiA9xAaqhG90TEVcWNwyonYLF1EQCLcBGAs/s1600/Screenshot%2Bfrom%2B2018-03-06%2B18-18-24.png)

  

I have a thing for Hackathon. I am a procrastinator. A lazy _and_ procrastinator graduate student, not a nice combination to have. But still when I see hundreds of sharp minds in a room scrabbling over idea, hungry to build and prototype their idea. Bring it to life, it finally pushes me to activity, makes me productive. 

That is why I love Hackathon, that is why I love HackRice, our resident Hackathon of Rice University.  
  
**_TL;DR: if you just want to try the extension, [chrome version is here](https://chrome.google.com/webstore/detail/ufilter/fodkdomomfnijpdebiobandpijlnonig) and [Firefox version is here](https://addons.mozilla.org/en-US/firefox/addon/ufilter/)._**

  

I have been participating at HackRice since 2014, when I think for the first time it was open for non-rice students, and have been participating ever since. What a roller coaster ride it has been, but that is a story for another day.

HackRice 7.5 being the last one I will be able to attend at Rice, it was somewhat special and emotional for me.

  

[![](https://3.bp.blogspot.com/-U4Dcxwll5tI/WqDcKMG5AuI/AAAAAAABqhc/C43kYTyOvnAaAjGezM3uR9QsuNRDEYRGgCLcBGAs/s320/IMG_20180302_190644.jpg)](https://3.bp.blogspot.com/-U4Dcxwll5tI/WqDcKMG5AuI/AAAAAAABqhc/C43kYTyOvnAaAjGezM3uR9QsuNRDEYRGgCLcBGAs/s1600/IMG_20180302_190644.jpg)

Hackrice 7.5 starts now!

HackRice 7.5 was a tad different form the other iterations. For starters it was the first time it was being held in Spring semester, and hence on a smaller scale and only to Rice Students. And also instead of normal 26 hours, it was exactly 24 hours. The venue was Liu Idea Lab. I have never been to the lab before, and it seemed to be a nice place to sit and work. The event started on Friday evening and ended on Saturday evening.

The event had two tracks, with a beginner and a Data Science track. The organizers had two in depth workshop/tutorials set up for both of these tracks to help out starters. Which I though was really cool. Even though I was brainstorming and prototyping on something different, I sat through them anyway and felt they were really thorough.

  

Being a one person team, and not really knowing anybody else I decided to work on a relatively smaller project which I can finish instead of trying anything in Data Science track. The idea I initially had was of a privacy filter. After some more brainstorming realized to properly make one, taking account of all anonymizing factors it probably will take me more time than 24 hours. I decided to settle on more of a toxic/malicious/sanity/trigger word filter. 

  

_The Idea:_ Create a browser based extension that can filter out abusive posts, word, sentences paragraphs.

  

  

_Inspiration:_Lately a lot fo us have started noticing the rise of cyber bullying and abusive behaviors across the internet. Be that reddit or facebook group. Often I see it gets me rallied up just before I goto sleep. Often I wish if only I did not read that. Recent increase in cyber bullying is one of the primary reason for the tool. Mental health and online harassment are major, relevant issues today in our current society. Everyone should be able to access content in the internet without fearing for trigger words or harassment. And that goes specially for the people who have been victim of such incidents and really doesn't wish to see any such trigger words.

  

  

**_What is uFilter:_**

[![](https://3.bp.blogspot.com/-zcYMjUJBVi0/WqDiT5B5E-I/AAAAAAABqhs/mLrfetOySXUS_GWzrNxnNnjoLkgtoWB3gCLcBGAs/s320/Screen%2BShot%2B2018-03-03%2Bat%2B6.56.38%2BPM.png)](https://3.bp.blogspot.com/-zcYMjUJBVi0/WqDiT5B5E-I/AAAAAAABqhs/mLrfetOySXUS_GWzrNxnNnjoLkgtoWB3gCLcBGAs/s1600/Screen%2BShot%2B2018-03-03%2Bat%2B6.56.38%2BPM.png)uFilter is a smart web extension made to help people browse the web without seeing content they don't like to see. Bringing the power to choose what to see back to users. The user has a list of buttons as filters they can choose. Either individual or more than one at a go. The process is simple and subtle: check off the type of content you want to avoid and let us handle the rest! Questionable content is blurred out, if you wish to see it nonetheless you can click to reveal the text.

  

You can see it in action here:

  

  

_What it does in the background: _The contents are blocked at page load, so the user is still able to access the context of the site before making up their mind if they are staying or leaving. The extension has s simple UI which lets them choose what to block and what not.

  

They can also click on the covered sections to reveal as they go. The script searches through the entire DOM looking for elements wherever they may be on the page. Sentiment analysis was implemented to determine what content was malicious.

[![](https://4.bp.blogspot.com/-3e0w-gjWcwc/WqDk20DcoaI/AAAAAAABqiA/RM9Dgag_iXwVFmfiJJK3-WbOViQr82gcwCLcBGAs/s400/Screen%2BShot%2B2018-03-08%2Bat%2B1.22.07%2BAM.png)](https://4.bp.blogspot.com/-3e0w-gjWcwc/WqDk20DcoaI/AAAAAAABqiA/RM9Dgag_iXwVFmfiJJK3-WbOViQr82gcwCLcBGAs/s1600/Screen%2BShot%2B2018-03-08%2Bat%2B1.22.07%2BAM.png)

The script also observes the page so it can adaptively block content on pages like Youtube loading comments, Facebook feed as well as Twitter pages. 

uFilter is not just a dumb keyword filter. It first combs every web page you visit for questionable content based on your filter selection, once it identifies sentences containing questionable content and uses the [AFINN-165](http://www2.imm.dtu.dk/pubdb/views/publication_details.php?id=6010) wordlist and [Emoji Sentiment Ranking](http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0144296) to perform [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis). Once it determines it has abusive content. It blurs out only that portion.  

[![](https://2.bp.blogspot.com/-JwnQuQU_KYo/WqDlPk9cOMI/AAAAAAABqiE/jMWic4UJIgscGgZDPcr3pJnSrLoP2lfEwCLcBGAs/s640/Screen%2BShot%2B2018-03-03%2Bat%2B5.05.51%2BPM.png)](https://2.bp.blogspot.com/-JwnQuQU_KYo/WqDlPk9cOMI/AAAAAAABqiE/jMWic4UJIgscGgZDPcr3pJnSrLoP2lfEwCLcBGAs/s1600/Screen%2BShot%2B2018-03-03%2Bat%2B5.05.51%2BPM.png)

  

[![](https://4.bp.blogspot.com/-UVtj56_A_qA/WqDlP-pDtwI/AAAAAAABqiI/nXg3aUo8WXAA0hBicAuC41SaKPy4AVtXACLcBGAs/s640/Screen%2BShot%2B2018-03-03%2Bat%2B7.03.15%2BPM.png)](https://4.bp.blogspot.com/-UVtj56_A_qA/WqDlP-pDtwI/AAAAAAABqiI/nXg3aUo8WXAA0hBicAuC41SaKPy4AVtXACLcBGAs/s1600/Screen%2BShot%2B2018-03-03%2Bat%2B7.03.15%2BPM.png)

  

The most useful part of uFilter is, it can observe dynamic webpages and works on texts which are dynamically loaded into the webpage. Hence it works for twitter or Facebook with rolling feed and dynamic texts as well. 

[![](https://thumbs.gfycat.com/DifficultWeightyArabianhorse-size_restricted.gif)](https://thumbs.gfycat.com/DifficultWeightyArabianhorse-size_restricted.gif)

Another distinguishing feature of uFilter is, it does not remove/replace any content. If a user decides from the context of the page that s/he wants to read the content, just clicking on the blurry portion will reveal the text to the user.

  

[![](https://thumbs.gfycat.com/HandsomeNippyHornedviper-size_restricted.gif)](https://thumbs.gfycat.com/HandsomeNippyHornedviper-size_restricted.gif)All this is done in realtime so the user does not notice any difference in their normal browsing behavior. But of course properly identifying abusive content just programmatically is a hard problem. Recognizing that uFilter gives the user an option to tag/mark/categorize text as offensive. Once a user does that, the filter will learn from it. This information is stored in a firebase datastore **without any identifying information** and helps uFilter.  
  
The end result is a _uFilter_ which can intelligently sanitize any website or webpage you visit of any abusive content you do not wish to see. You can see it in action  
  

  
  

[![](https://3.bp.blogspot.com/-e2ExWOslEwQ/WqDrZYIlu0I/AAAAAAABqic/SZca6v7FKxAMZQzvaa2XZYxqMYP7XCtugCLcBGAs/s320/2018-03-08%2B01.50.40.jpg)](https://3.bp.blogspot.com/-e2ExWOslEwQ/WqDrZYIlu0I/AAAAAAABqic/SZca6v7FKxAMZQzvaa2XZYxqMYP7XCtugCLcBGAs/s1600/2018-03-08%2B01.50.40.jpg)

Got this beautiful earphone as prize

_Coming back to Hackrice._ I really did not expect much when I submitted it for judging. I had just barely made a working prototype and published it in Chrome Web Store. It was working in Firefox but it still had some security problems for which Firefox was not publishing the add-on. Surprisingly the judges including Dr. Wang was really interested in the idea and specially the implementation. When the time came for deciding winners it was announced that **uFilter won the first prize!** Imagine my delight!  
  
If you want to know more about the project, visit the submission page at [devpost](https://devpost.com/software/ufilter).  
If you want to try the add-on, I will be delighted to hear your feedback!  
  
[Chrome version download link!](https://chrome.google.com/webstore/detail/ufilter/fodkdomomfnijpdebiobandpijlnonig)  
[Firefox version download link!](https://addons.mozilla.org/en-US/firefox/addon/ufilter/?src=search)  
  

[![](https://4.bp.blogspot.com/-tOtkXcO38PM/WqD0Zc1R5OI/AAAAAAABqis/FG0WljcRyfgDgZFNwTFiBRcoKFBSDMZFQCLcBGAs/s400/MVIMG_20180303_223557.jpg)](https://4.bp.blogspot.com/-tOtkXcO38PM/WqD0Zc1R5OI/AAAAAAABqis/FG0WljcRyfgDgZFNwTFiBRcoKFBSDMZFQCLcBGAs/s1600/MVIMG_20180303_223557.jpg)

The loot :D A QC30 and Solar Backpack
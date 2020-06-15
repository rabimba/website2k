---
title: 'Story of a Drupal theme mis-configuration, Hacking and Ministry of Defense India'
date: 2018-04-06T20:57:00.000-05:00
draft: false
aliases: [ "/2018/04/story-of-drupal-theme-mis-configuration.html" ]
---

![](https://d1ah1il5j7hxtz.cloudfront.net/wp-content/uploads/2018/04/Defence-ministrys-website-hackedFEATURE-696x629.jpg)

If you have been following news or were online for past couple of hours you might have noticed this news making a tweet-storm and appearing all over your timeline regarding how India's Ministry of Defense website got hacked (allegedly by '_Chinese' _origin).

  

Almost all the big media outlets covered it. Including

  

\* [Youtube : TimesNow](https://www.youtube.com/watch?v=8KLR8k5cNvg)

\* [Times Now](http://www.timesnownews.com/india/article/the-official-website-of-the-ministry-of-defence-hacked-ministry-of-home-affairs-home-ministry-labour-ministry-chinese-hackers-cyber-attack-india/214607)

\* [Hindustan Times](https://www.hindustantimes.com/india-news/ministry-of-defence-website-hacked-leads-to-error-message/story-85ASfKmolUiDXEwrwNsAfP.html)

\* [NDTV](https://www.ndtv.com/india-news/defence-ministry-website-hacked-leads-to-an-error-page-1833811)  
\* [Business Standard](http://www.business-standard.com/article/news-ani/ministry-of-defence-official-website-hacked-118040600841_1.html)

\* [Times of India](https://timesofindia.indiatimes.com/india/defence-ministry-website-allegedly-hacked-displays-chinese-character/articleshow/63643681.cms)

An example of the coverage

  
  
Fueled by our own famous ministers chiming in with their own ideas  
  

> Action is initiated after the hacking of MoD website ( [https://t.co/7aEc779N2b](https://t.co/7aEc779N2b) ). The website shall be restored shortly. Needless to say, every possible step required to prevent any such eventuality in the future will be taken. [@DefenceMinIndia](https://twitter.com/DefenceMinIndia?ref_src=twsrc%5Etfw) [@PIB\_India](https://twitter.com/PIB_India?ref_src=twsrc%5Etfw) [@PIBHindi](https://twitter.com/PIBHindi?ref_src=twsrc%5Etfw)
> 
> — Nirmala Sitharaman (@nsitharaman) [April 6, 2018](https://twitter.com/nsitharaman/status/982223129878544384?ref_src=twsrc%5Etfw)

  
It all seemed for the fact that the homepage of the websites showed this image with a Chinese character  

[![](https://2.bp.blogspot.com/-hP35KBs0wWM/Wsgh-BeH2ZI/AAAAAAABs2o/NV_JU3-19Xch1fiTx8SVaO24ukCEozjxwCK4BGAYYCw/s320/photo_2018-04-06_20-42-02.jpg)](http://2.bp.blogspot.com/-hP35KBs0wWM/Wsgh-BeH2ZI/AAAAAAABs2o/NV_JU3-19Xch1fiTx8SVaO24ukCEozjxwCK4BGAYYCw/s1600/photo_2018-04-06_20-42-02.jpg)

And though most of india's government portals and websites aren't really what we call secure (I'll cite the references later), hilariously this time **_it really was not a hack!_**

**_I got tired of explaining everyone in social media again and again what went wrong hence this blogpost._**

It really was just a mis-configured Drupal theme :)

  

You see, most of the websites by [NIC](https://www.nic.in/) for government portals are made using a CMS called Drupal. Which is not a bad thing itself, White House's website is made in Drupal. But the hilarious thing is they were using a theme called [Zen](https://www.drupal.org/project/zen) (https://www.drupal.org/project/zen) and though they customized the theme to suit the respective government portals, they did not customize the maintenance page!

  

Any idea what is Zen Theme's logo?

  

[![](https://www.drupal.org/files/styles/grid-3/public/images/zen-logo.png)](https://www.drupal.org/files/styles/grid-3/public/images/zen-logo.png)

Now see the character on that screenshot and in the logo? 

  

And now the most awesome part is, that character is not even Chinese. It's Japanese (Kanji to be precise 禅). After reading all this if you are in need of some Zen, I won't blame you. Head over to: https://en.wikipedia.org/wiki/Zen  
  
Still don't believe me? Then look at the source code.  
The Zen theme logo is located at : [https://github.com/JohnAlbin/now/blob/master/www/sites/all/themes/zen/logo.png](https://github.com/JohnAlbin/now/blob/master/www/sites/all/themes/zen/logo.png)  
  
And it is referenced at Line 46 of the [maintenance template file](https://github.com/JohnAlbin/now/blob/master/www/sites/all/themes/zen/templates/maintenance-page.tpl.php).  

[![](https://1.bp.blogspot.com/-XLVA3iT9WAA/WshZhXJp5kI/AAAAAAABs3E/4vpHgX0RmWwOesqSPlEnIuHoHSQzNkQuQCLcBGAs/s1600/Capture.PNG)](https://1.bp.blogspot.com/-XLVA3iT9WAA/WshZhXJp5kI/AAAAAAABs3E/4vpHgX0RmWwOesqSPlEnIuHoHSQzNkQuQCLcBGAs/s1600/Capture.PNG)

  

And that logo.png file is this one 

[![](https://github.com/JohnAlbin/now/blob/master/www/sites/all/themes/zen/logo.png?raw=true)](https://github.com/JohnAlbin/now/blob/master/www/sites/all/themes/zen/logo.png?raw=true)

  

So in short, **those claims about hack are not true!**

![](https://www.tanay.co.in/sites/default/files/cdn/2018/04/07/fPtnftyLF2KBc4EuZCSk2Gap5qcUJ_AYZX7IRBlb-Fqueznw6wH-Zi7jcjWxvfDk-BJ2SR-PBVmnX_A5-enJBAOqKQB3P970OOQwvAEGTlPbrxd6j7FR9c2738T61fbAQfqEF0Oa)

  

  

![](https://www.tanay.co.in/sites/default/files/cdn/2018/04/07/Xck7f75Pvh9u4AGxfpVDW-aaEui-mnrxBhxeLPGOFCsgawYhpF3mQKcqaE7j-G2Wa4PfnpEV5Sf1Ti0ePwCO4bx_13LVr1XuoW5CwrkDgW5ETA2Ec45jdf1dXKW7eWtpctAObucb)

  

**Next time, please don't believe everything you read in the internet? Specially if it's coming from our renowned ministers....**  
**_Attribution:_**  
The last two screenshots  and the first list of links of news portals are taken from [Tanay](http://www.tanay.co.in/blog/how-drupal-themes-logo-caused-confusion-and-escalated-tension-between-two-countries.html)'s blog (linked). Here is my due attribution along with one for newsmobile.in from whom I took the first image with "hacked" logo :)  
PS: while looking for his blog I just found out a list of websites which use Drupal in Indian Govt. work by Tanay here: [https://groups.drupal.org/node/248708](https://groups.drupal.org/node/248708) so any of them using zen theme should have displayed that logo today (unless someone customized it)
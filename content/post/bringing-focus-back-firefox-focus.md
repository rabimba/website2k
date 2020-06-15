---
title: 'Bringing the Focus back : Firefox Focus (Builds) for Android'
date: 2017-05-31T16:29:00.000-05:00
draft: false
aliases: [ "/2017/06/bringing-focus-back-firefox-focus.html" ]
tags : [Firefox Focus, MozTechSpeaker, Focus, firefox, Klar, android, chrome, mozilla]
---

Firefox Focus – A Free, Fast Private Browser for....android!
------------------------------------------------------------

[![](https://blog.mozilla.org/wp-content/uploads/2017/03/firefox-focus-hero-crop.jpg)](https://blog.mozilla.org/wp-content/uploads/2017/03/firefox-focus-hero-crop.jpg)

On 17th November 2016 [Mozilla announced Firefox Focus](https://blog.mozilla.org/blog/2016/11/17/introducing-firefox-focus-a-free-fast-and-easy-to-use-private-browser-for-ios/). A free fast and easy to use [private browser for](https://itunes.apple.com/us/app/firefox-focus-the-privacy-browser/id1055677337?mt=8) _[iOS](https://itunes.apple.com/us/app/firefox-focus-the-privacy-browser/id1055677337?mt=8)._ 

[![](https://2.bp.blogspot.com/-fdeGYd9LEsE/WS4bSS8AxnI/AAAAAAABVsc/nNF1SNprCuoA3ETKPbORMlIKx2X9gmyDgCK4B/s320/Screenshot_20170530-163844.png)](http://2.bp.blogspot.com/-fdeGYd9LEsE/WS4bSS8AxnI/AAAAAAABVsc/nNF1SNprCuoA3ETKPbORMlIKx2X9gmyDgCK4B/s1600/Screenshot_20170530-163844.png)

_Focus in One Plus One_

Firefox Focus was filled with goodies. From inbuilt tracker blocking, content blockers to making privacy the first class citizen. It was all of that. Wrapped in a nice package, but only for [Apple Ecosystem](https://techcrunch.com/2016/11/17/mozilla-launches-firefox-focus-a-private-web-browser-for-iphone/). The argument for having focus was to make privacy dead simple and default experience for most people out there. An excellent read is this article "[Privacy made simple with Firefox Focus](https://blog.mozilla.org/blog/2016/11/17/privacy-made-simple-with-firefox-focus/)".

  

And while this was all fine, a lot of us were severely disappointed that we don't have an android version. That all changes now.

  

Mozilla has released a port of the Firefox Focus source code and I decided to build a port from it. And this is how it looks in my One Plus One.

  

[![](https://2.bp.blogspot.com/-zXs7J5WJqa4/WS8NrwudyOI/AAAAAAABVtc/bnArRdpF2XAO2LWdC5MyHO-OGZTB24_WgCK4B/s640/Screenshot_20170530-164031.png)](http://2.bp.blogspot.com/-zXs7J5WJqa4/WS8NrwudyOI/AAAAAAABVtc/bnArRdpF2XAO2LWdC5MyHO-OGZTB24_WgCK4B/s1600/Screenshot_20170530-164031.png)

Notice the bin in Android

If you notice it looks almost similar to its iOS counterpart. Focus blocks tracking cookies by default in its system. But there are small design cues that are different than iOS version. In iOS you have a small erase button beside the URL to erase any history of the page you have visited.

![Firefox Focus Erase Button](https://ffp4g1ylyit3jdyti1hqcvtb-wpengine.netdna-ssl.com/wp-content/uploads/2016/11/image-300x112.png)

in iOS

And in Android, you will notice the small **recycle bin** on the bottom left of the screen which does the same thing. And I think I like the bin better.

  

[![](https://4.bp.blogspot.com/-R644fKPferU/WS8Pjo3cGfI/AAAAAAABVto/tk0Ouy-swDsjFtldor51S2x4Bw8vHI1ggCK4B/s320/Screenshot_20170530-164051.png)](http://4.bp.blogspot.com/-R644fKPferU/WS8Pjo3cGfI/AAAAAAABVto/tk0Ouy-swDsjFtldor51S2x4Bw8vHI1ggCK4B/s1600/Screenshot_20170530-164051.png)  

I am using the Gecko build right now. There are ways to build using both Gecko and WebKit (and you get links of both at end of article). Mozilla's recommended build is the WebKit one, but being a mozillian I decided to test the gecko view anyway. The gecko build comes around **35mb** and the WebKit one is of **2.2 mb**. So we can clearly see that in one the whole engine gets included in the apk.

  

[![](https://3.bp.blogspot.com/-iIYZWSCW0jg/WS8QrqcXUGI/AAAAAAABVt0/yKsmOWlz27o-EDkr39ClxT7vXgptJtphQCK4B/s320/Screenshot_20170530-174100.png)](http://3.bp.blogspot.com/-iIYZWSCW0jg/WS8QrqcXUGI/AAAAAAABVt0/yKsmOWlz27o-EDkr39ClxT7vXgptJtphQCK4B/s1600/Screenshot_20170530-174100.png)I am not entirely sure which engine Focus will use in its release version. Gecko works fine for me now.

  

For me the browsing experience is very similar to Firefox for Android. Pages do load a bit faster than on Firefox, that might be because of the browser blocking ads and similar resources or just my perception. Pressing the OPO's hardware back button goes back, but the forward button can only be found in the overflow menu. 

  

You will also notice that there is a master button to toggle trackers in the overflow menu, and that also shows you if the page you are on has any trackers that Focus in blocking at the moment. Informative I must say. There are also menu items to share the current page or open it with another browser on your device.

[![](https://2.bp.blogspot.com/-JHzYsvjK4UM/WS8RcB6klLI/AAAAAAABVuI/P6eijqjvA-wGjPDQzn5p5qi8Sks4Qo1GQCK4B/s400/Screenshot_20170530-164051.png)](http://2.bp.blogspot.com/-JHzYsvjK4UM/WS8RcB6klLI/AAAAAAABVuI/P6eijqjvA-wGjPDQzn5p5qi8Sks4Qo1GQCK4B/s1600/Screenshot_20170530-164051.png)[![](https://1.bp.blogspot.com/-4LNvzSXp9_c/WS8RZp3BL-I/AAAAAAABVuA/Zu0uorxx5_cQZWpH6XuozSdLgzyH1VEngCK4B/s400/Screenshot_20170530-164058.png)](http://1.bp.blogspot.com/-4LNvzSXp9_c/WS8RZp3BL-I/AAAAAAABVuA/Zu0uorxx5_cQZWpH6XuozSdLgzyH1VEngCK4B/s1600/Screenshot_20170530-164058.png)

The settings page has options for changing your search engine, setting Focus as your default browser, and sending anonymous telemetry data. You can also enable or disable ad trackers, analytic trackers, web fonts, and social trackers separately. If you're feeling brave, there's also an option to use a more aggressive blacklist, which Focus warns "_may break some videos and Web pages_."

  

Focus by default does not let you take screenshots of a page you are in (then how did I?). The option resides in **Stealth** mode. But for the debug version I built, I have disabled that option. Afterall screenshots are very useful to write a blog post.  

#### What does not work:

[![](https://1.bp.blogspot.com/-0l4aPOY3KmM/WS83Dxn4XnI/AAAAAAABVwE/Cx8jWfPvUdYvD74DJEQ-rc7cmvzIL9elwCK4B/s320/Screenshot_1496263447.png)](http://1.bp.blogspot.com/-0l4aPOY3KmM/WS83Dxn4XnI/AAAAAAABVwE/Cx8jWfPvUdYvD74DJEQ-rc7cmvzIL9elwCK4B/s1600/Screenshot_1496263447.png)In my brief period of testing, I found out that the context menu of Pixel, does not work yet. It does show the context menu in the launcher but if you click on it it just shows the app is not installed. That might be a goof up in my part as well on how I built the apk

  

Focus get's the blocklist for its content from a modified [DisconnectMe](https://disconnect.me/) List. Do read [here](https://github.com/mozilla-mobile/focus-android/tree/master/shavar-prod-lists) to know how that works with Focus.

  

[![](https://3.bp.blogspot.com/-Xukssh_gq5Y/WS8qzZSUwqI/AAAAAAABVvg/7BIKyfMJcNogHvUpwufgkmsvS0Ad_awiQCK4B/s400/Screenshot_1496263292.png)](http://3.bp.blogspot.com/-Xukssh_gq5Y/WS8qzZSUwqI/AAAAAAABVvg/7BIKyfMJcNogHvUpwufgkmsvS0Ad_awiQCK4B/s1600/Screenshot_1496263292.png)

  

And now the binaries to install in your phone

  

Firefox Focus Gecko Debug Build: [Here](https://goo.gl/aoMpyx)

Firefox Focus WebKit Debug Build: [Here](https://goo.gl/OGj1n9) (this might not work for you depending on your mobile)

  

If you are using an MIUI based Rom and can not get past the introduction animation, use this modified apk which gets you in: [Modified for MIUI](https://goo.gl/Stpurj) (Thanks, [Sukanta Sarkar](https://www.facebook.com/sukanta.sarker.slg?fref=ufi) for being my tester)

  

#### Coverage Builds: _These builds have the screenshot protection active (you can toggle on and off)_

Firefox Focus WebKit Coverage Build: [Here](https://goo.gl/V0T2ef)

  

  

[![](https://3.bp.blogspot.com/-YQ2QCuAmUoo/WS807yLCRRI/AAAAAAABVv4/qgVN-Fzw7RA8P9ky-RknBU7K_Wv2qqf8QCK4B/s400/Screenshot_1496263722.png)](http://3.bp.blogspot.com/-YQ2QCuAmUoo/WS807yLCRRI/AAAAAAABVv4/qgVN-Fzw7RA8P9ky-RknBU7K_Wv2qqf8QCK4B/s1600/Screenshot_1496263722.png)[![](https://3.bp.blogspot.com/-klvGZXBn7KA/WS80uEZZcWI/AAAAAAABVvw/MqZKEfLuESUiGfo7mg3O5QUSvoL0xcnfACK4B/s400/Screenshot_1496263716.png)](http://3.bp.blogspot.com/-klvGZXBn7KA/WS80uEZZcWI/AAAAAAABVvw/MqZKEfLuESUiGfo7mg3O5QUSvoL0xcnfACK4B/s1600/Screenshot_1496263716.png)Also, there is a treat. **[Firefox Klar](https://itunes.apple.com/de/app/firefox-klar-der-browser-mit-privatsph%C3%A4re/id1073435754?mt=8)** or Firefox Clear is the same Firefox Focus, rebranded to be used in Germany. Here is the same rebranded build of Klar/Clear for Android.

  

  

Firefox Klar WebKit Debug: [Here](https://goo.gl/qbiUQA)

Firefox Klar WebKit Coverage: [Here](https://goo.gl/UP4f7u)
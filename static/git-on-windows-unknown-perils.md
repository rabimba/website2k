---
title: 'Git on Windows: The unknown Perils'
date: 2014-07-08T08:56:00.002-05:00
draft: false
aliases: [ "/2014/07/git-on-windows-unknown-perils.html" ]
---

  

  

  

Today when I was finally setting up a few things in my work laptop and tried to work with a few codes I pushed to my git repository I faced a new error again.

  

What I wanted to do.

Just a simple git cli call to add a repository to my local phonegap build.

  

And I ended up with

  

[![](http://2.bp.blogspot.com/-b2OTV3rHeG0/U7v4bTO1YoI/AAAAAAAAP6c/s0rqCt4QH08/s1600/Untitled+picture.png)](http://2.bp.blogspot.com/-b2OTV3rHeG0/U7v4bTO1YoI/AAAAAAAAP6c/s0rqCt4QH08/s1600/Untitled+picture.png)

  

  

Interesting. Very interesting.

As it turns out it is a platform specific bug in Windows with Git. Never noticed it before because I never used windows very much for my dirty development works.

  

Apparently

  

{ \[Error: Command failed: fatal: could not create work tree dir 'C:\\Users\\RXK132

~1\\AppData\\Local\\Temp\\plugman\\git\\1404826931375'.: No such file or directory

\] killed: false, code: 128, signal: null }

 \[error\] Command failed: fatal: could not create work tree dir 'C:\\Users\\RXK13

2~1\\AppData\\Local\\Temp\\plugman\\git\\1404826931375'.: No such file or directory

  

Is produced as windows is unable to create the directory structure. If you manually create the directory then it works just fine.

  

You can follow the issue at [https://github.com/sbt/sbt/issues/895](https://github.com/sbt/sbt/issues/895)
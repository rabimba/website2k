---
title: 'Testing With Python: The Django Way Part 1'
date: 2013-04-12T05:06:00.000-05:00
draft: false
aliases: [ "/2013/04/testing-with-python-django-way-part-1.html" ]
---

[![](http://images-onepick-opensocial.googleusercontent.com/gadgets/proxy?container=onepick&gadget=a&rewriteMime=image%2F*&url=https%3A%2F%2Fwww.djangoproject.com%2Fs%2Fimg%2Fsite%2Fhdr_logo.gif)](http://images-onepick-opensocial.googleusercontent.com/gadgets/proxy?container=onepick&gadget=a&rewriteMime=image%2F*&url=https%3A%2F%2Fwww.djangoproject.com%2Fs%2Fimg%2Fsite%2Fhdr_logo.gif)

  
One thing I really slacked on while developing AWiKi (it's on internal network hence can't show you) was testing. Maybe that's not the right way to put it. It's not like I didn't test. In fact, I did a lot of testing. A lot of painstaking manual testing. For every change. So, in a way it was really the opposite of slacking. It was working a whole lot harder than I really needed to. It was also dumb.   
Being conversant in conventional Automation methods I quickly tried my hands on automating a few scenarios using QTP and Selenium. But this soon led me to a more severe problem: I was surrounded with uncountable number of scenarios I needed to automate and soon it was eating more time than I was devoting in the development.  
Soon I realized What I did slack on, was figuring out how Django's unit testing framework worked. Well, no more! In fact, it's really easy to set up. Writing tests can also be somewhat painstaking when it comes to ensuring you've covered every possible input, but at least that pain is an investment that repays itself every time you make a change to the program and you can know right away if you've broken something that used to work.   
As usual the Django documentation is excellent. Highly recommend for learning everything about testing with Django. What I hope to do here is give a brief overview of what you need to do some basic testing. Partly as a reminder for myself on future projects, and hopefully to help out anyone in the same position I was before I started.  
  
Getting Started   
  
If your Django app is relatively new, the startapp command already created a tests.py file when you ran it to set up your app. This file includes some helpful examples, like so:  
  
"""  
This file demonstrates two different styles of tests (one doctest and one  
unittest). These will both pass when you run "manage.py test".  
  
Replace these with more appropriate tests for your application.  
"""  
  
from django.test import TestCase  
  
class SimpleTest(TestCase):  
    def test\_basic\_addition(self):  
        """  
        Tests that 1 + 1 always equals 2.  
        """  
        self.failUnlessEqual(1 + 1, 2)  
  
\_\_test\_\_ = {"doctest": """  
Another way to test that 1 + 1 is equal to 2.  
  
\>>> 1 + 1 == 2  
True  
"""}   
  
If you don't already have a tests.py file, the important things to note are that you have to import the **TestCase** class from django.test and create a new class which subclasses it. Each method defined in this class will correspond to one test, usually the test of a corresponding function in your **views.py** file. To test a particular function from **views.py**, define a method with the name **test\_functionname**.  
  
Test data   
  
Now, I'm guessing your application probably manipulates some sort of data. As a matter of fact mine does a lot. The Django test runner is kind enough to setup and destroy a complete test database for the purposes of running your tests. There's two important consequences to this. First, the database user specified in your settings.py file has to have the necessary permissions to create and destroy databases. So, make sure that's the case. Second, if you already have a test database set up on your development machine (or wherever), with data you've inserted during your manual tests, the test runner won't have access to any of it.  
To get some data for your tests, you can try exporting the data already in your test database with Django's dumpdata command. The test runner can then load it as a fixture. Honestly, I just couldn't get this to work. Some googling about the errors I was getting seemed to indicate that I wasn't the only one having problems with it. The update to natural keys announced for Django 1.2 seemed like it would help, but I've still been unsuccessful, so far. In any event, I plan on keeping an eye on future developments to see if there's any improvements in this area.  
In the meantime, I went ahead and did it the hard way. I created a separate file called **testsetup.py**. I imported all the models for my project and defined a function also called **testsetup**. All this function does is create a few instances for each model with all their various possible configurations. By defining a method called **setUp** in the new class I created in **tests.py** and calling this function there, all of the necessary data will be added to the test database before the tests are run.  
  
  
```
class ViewTest(TestCase):  
  
    def setUp(self):  
        testsetup()
``````
  

``````
  

``````
And now we will delve into the requests. But that's for another day ([Part 2](http://rkrants.blogspot.com/2013/04/testing-with-python-django-way-part-2.html))
```
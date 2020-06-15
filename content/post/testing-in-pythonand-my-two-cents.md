---
title: 'Testing In Python...and my Two cents'
date: 2012-08-02T21:19:00.001-05:00
draft: false
aliases: [ "/2012/08/testing-in-pythonand-my-two-cents.html" ]
---

The only lesson I have learned in mys past one and half of years of experience in testing is that the easier I make writing and running tests for my programs, the faster I can produce bug-free software.

  
Being a developer and also being a tester can do wonders I think. Never before this thought would have crossed my mind while coding.

  

  

That is why I start most projects nowadays with two pre-baked files: _main.py_ and _tests.py_.

With this setup and tools like [Nose](http://somethingaboutorange.com/mrl/projects/nose/1.0.0/), testing code in Python for me is nearly pain free. Recently however, I notice one aspect of the **unittest** package in Python's standard libary drives me absolutely crazy:

Why is there no simple method to run a single test case from within an interactive python shell?

As developers, this is important because if we are going to make writing tests an integral part of our development workflow, one needs some way to actually run the damn test without dropping out of our Python sessions and breaking out of our mental flow.

Being forced to run tests solely from the commandline also means we can't take advantage of features like ipython's ability to automatically [drop into a pdb debugging session](http://ipython.scipy.org/doc/manual/html/interactive/tutorial.html#debug-a-python-script) when an error occurs. This is extremely useful for when you want to introspect one or two variables to determine why a test failure occurred.

In general, it seems like the _unittest_ library's lack of a simple function to run single test cases in an interactive shell dis-incentivizes programmers from writing tests and detracts from python's whole "rapid iteration" ethos.

After googling around and failing to find any good alternatives, I've finally settled on writing my own utility function to run single test cases:  
  
```
def runtest(testCase, methodName):  
    """ Runs a test case from within interactive shell """  
  
    tc \= testCase(methodName)  
    getattr(tc, "setUp", lambda:None)()  
    try:  
        getattr(tc, methodName)()    
    finally:  
        getattr(tc, "tearDown", lambda:None)()
```

  

I add this function to every single project that I create now, and the qualitative feel of writing tests just feels so much more natural now. I also find myself writing more tests and running them more often with this function in my projects.

Give it a try, and let me know whether this has any effect for you. I'd love to hear your feedback on how it affects your development workflow.
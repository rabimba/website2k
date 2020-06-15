---
title: 'Request module: non-callable Dict Object'
date: 2013-03-24T09:51:00.000-05:00
draft: false
aliases: [ "/2013/03/request-module-non-callable-dict-object.html" ]
---

  
So, you are using the amazing requests module of Python! So checked their sample code in the website: http://docs.python-requests.org/en/latest/ and the URL you are calling returns json content. So you followed their example and came up with a code like this:  
  
import requests  
url = '' # put your url here  
r = requests.get(url)  
json\_content = r.json()  
print json\_content  
  
When you run the program, you get the following error:  
  
json\_content = r.json()  
TypeError: 'dict' object is not callable  
  
Now you are wondering what is this! An example from the home page doesn't work. So you searched Google and came here. Now you solve the problem using  
  
json\_content = r.json instead of  
json\_content = r.json()  
  
So this code will work (Python 2.7):  
  
import requests  
url = '' # put your url here  
r = requests.get(url)  
json\_content = r.json  
print json\_content  
  
If you are wondering why you got the error in the first code, let me give you a hint. Add the following lines to your Python code and see the output:  
  
print type(r)  
print type(r.json)
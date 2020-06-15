---
title: 'XML parsing and Python: the lxml way'
date: 2012-09-26T15:13:00.001-05:00
draft: false
aliases: [ "/2012/09/xml-parsing-and-python-lxml-way.html" ]
---

Today I was tinkering with an idea involving parsing a Html file by taking an XML structure and building a simple xquery engine in python.  

  

I know...most of my "World changing ideas" finally end up on my unfinished/fragile Github Project category.

But knowing how it's gonna help me in long drive I tried to give it a shot anyway.

  

And this is when I discovered [lxml](http://lxml.de/) and immediately fell in love with it.

But rather going to the intricacies I'm gonna share how simple it was for me to pars an xml file with it.

  

First, we'll make sure we have everything in place.

Things we need

*   lxml

Yeah...that's kinda only thing you'll need :) (and of course Python!!!).

If you are sing Ubuntu or Xubuntu (like me) then just goto synaptics package manager and install it. Or get it from the website if you are gonna tinker in windows.

  

Now, let's assume that we want to parse a xml file named 'file.xml' with the following content:  

  

[![](http://2.bp.blogspot.com/-6N4-zyiAfKE/UGNhGgVX7zI/AAAAAAAAFgA/DYyXwXXAac8/s1600/Untitled.png)](http://2.bp.blogspot.com/-6N4-zyiAfKE/UGNhGgVX7zI/AAAAAAAAFgA/DYyXwXXAac8/s1600/Untitled.png)

  
  

Now I want to get all the element\_id for my purpose from the file. The following python code serves the purpose:  
  
  
from lxml import etree  
  
doc = etree.parse('file.xml')  
element\_list = doc.findall('element')  
  
for store in store\_list:  
element\_id = element.findtext('element\_id')  
  
  
print element\_id  

  

Another way would be    
  
  
from lxml import etree  
  
doc = etree.parse('file.xml')  
  
for element in doc.getiterator('element'):  
element\_id = element.findtext('element\_id')  
print element\_id
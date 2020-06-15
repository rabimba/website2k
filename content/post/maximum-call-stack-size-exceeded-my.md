---
title: 'Maximum Call Stack size exceeded: My mishap with nodejs and MongoDB'
date: 2013-04-08T09:20:00.000-05:00
draft: false
aliases: [ "/2013/04/maximum-call-stack-size-exceeded-my.html" ]
---

Working with nodejs is always an adventure and mix MongoDB with it, and it becomes very interesting for a nodejs _enthusiast_ like me.  
  
While working on a pet project involving Native [MongoDb driver](https://github.com/mongodb/node-mongodb-native) and nodejs I encountered a weird problem.  
  
```
RangeError: Maximum call stack size exceeded
```

```
As usual my first thought was to Google out what I was facing and googling it out led me to the following to links.
```

*   [RangeError: Maximum call stack size exceeded](https://github.com/mongodb/node-mongodb-native/issues/715)
*   ```
    [Calling Model.collection.save() RangeError: Maximum call stack size exceeded](https://groups.google.com/d/msg/mongoose-orm/H_Yz65lezMA/4lFi7iCcBzcJ)
    ```
    

Also In some posts in MongoDB’s forum I saw that peoples said saving in \`process.nextTick\` or wrapping the call function in \`parseInt\` will also fix the problem, but it most certainly didn't work for me.So I started digging in on my own and soon enough found the reason.  
  
If you’re trying to **save a document** and saving process somehow exited with an **RangeError: Maximum call stack size exceeded** exception, it’s related to what you want to save in the database. I had this problem also, and when I checked my object, I found that the problem is related to the _big DOM Object_ that I included in the object, and when I removed that, the object saved in MongoDB correctly.  
  
My piece of buggy code:  
  

> ```
> collection.insert({ seq: nextSeq, profileIdentity: profileIdentity, sectionData: secData,  //the buggy part   
>   findDateTime:  new  Date()  
> });
> ```

 The problem occurred in \`secData\` array. In the second item of that array I had a big DOM Object and after removing that object from array (and of course, doing that job in a different way), problem solved.
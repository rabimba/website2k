---
title: 'Back To Rails: Sorting a Rails log by SQL Duration'
date: 2012-04-07T03:34:00.004-05:00
draft: false
aliases: [ "/2012/04/back-to-rails-sorting-rails-log-by-sql.html" ]
---

This is something I just stumbled upon. And here's what I did to it.  
  
  

Rails’ ActiveRecord logger writes log files like:

> `Post Load (735.8ms) SELECT ``posts`.\* FROM `posts` where post.title = 'rkship'

You may want to know the longest SQL queries for performance optimsation purposes, and general troubleshooting(my case). To list recent queries in order of duration, with longest queries shown last, I used this:

> `head -10000 development.log | grep '([0-9.]+ms)' | sed 's/._(([[:digit:].]+)ms._/\1ms &/g' | sort -n`

(The sed expression was a little more work than I’d bargained for as sed regular expressions are always lazy; even with GNU/Posix extensions, non-lazy just doesn’t exist.)
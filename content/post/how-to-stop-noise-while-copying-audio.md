---
title: 'How to Stop the Noise While Copying Audio CD'
date: 2008-12-31T01:10:00.000-06:00
draft: false
aliases: [ "/2008/12/how-to-stop-noise-while-copying-audio.html" ]
---

Whenever I try to burn an audio cd using Nero, my cd writer makes a lot of noise. Observing the process carefully for some time revealed that noise is generated only at the end of each track. Anyways, I tried to find a a fix for this, and here’s the step by step solution to the problem-

**Step 1**. Go to **System Properties>Device Manager** and select **IDE ATA/ATAPI** controllers.  
**Step 2**. Double click on the CD writer IDE channel and select advance setting.  
**Step 3**. In the advanced settings dialog, change the transfer mode to ‘PIO Only’.  
**Step 4**. Restart the computer.

That’s it. No more irritating noise now.

Enjoy!
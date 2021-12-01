---
title: 'reads to /bin will hit the disk only once every month or so'
date: 2012-05-09T19:55:00.000-07:00
draft: false
---

Blows my mind:  

> Then there is the frequency with which you reboot your computer. It's true every item must be read at least once, but, with enough RAM, it's read only once per boot - if you keep your machine on for a month at at time, **reads to /bin will hit the disk only once every month or so**. Disk writes can be trickier, since waiting for the physical write may halt the thread for a while, but, unless you specify writes to be synchronous, there is no reason not to trust the OS with the data and let it flush the cache when it's more convenient. And subsequent reads to the data you wrote won't hit the disk again until the memory is needed for something else. Reads from RAM are still orders of magnitude faster than reads from disk.

  
[Via ](http://news.ycombinator.com/item?id=3936374)
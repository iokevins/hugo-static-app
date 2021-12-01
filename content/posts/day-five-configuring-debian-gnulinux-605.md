---
title: 'Day five - Configuring Debian GNU/Linux 6.0.5 "squeeze"'
date: 2012-09-13T21:25:00.000-07:00
draft: false
tags: 
- linux
- debian
---

Re-installed Debian GNU/Linux 6.0.5 "squeeze" this evening and went through all four days of documented changes in about one hour. What a difference good documentation makes.  
  
The install process went through it's normal hiccup with detecting network hardware...I modified check-missing-hardware as [before](http://schultkl.blogspot.com/2012/09/debian-gnulinux-605-squeeze-install.html), then it seemed to get stuck again during detection of the hard drive. I switched to Ctrl + Alt + F4 to watch the system messages, and noticed the kernel time out several times in a row. Then the install started moving forward again.  
  
Investigating why my hard drive seems to continuously click when parking the head.
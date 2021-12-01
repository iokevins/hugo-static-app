---
title: 'Tree Container Library and Wubi'
date: 2008-04-27T13:09:00.000-07:00
draft: false
tags: 
- linux
- debian
---

Initial compile of the [Tree Container Library](http://www.datasoftsolutions.net/tree_container_library/overview.php) (TCL, [regrettably](http://en.wikipedia.org/wiki/Tcl), for short) fails--I'm running a version of Debian via QEMU that's a bit behind the curve, with gcc 3.3.5.  
  
I hosed my apt repository during a failed upgrade a few months ago (it wanted to upgrade the kernel, I canceled, corruption ensues). So I thought I'd upgrade--I'm testing out [Wubi](http://wubi-installer.org/), an installer that works in a similar fashion to [QEMU](http://fabrice.bellard.free.fr/qemu/), in that it allocates a block of space for an Ubuntu install (about 7GB). The nice part is that you can dual-boot into either one, and uninstall it like an app if you want.  
  
UPDATE: Never mind--while waiting for Wubi I discovered an [alternate tree data class](http://www.aei.mpg.de/%7Epeekas/tree/) (thanks Kasper Peeters, I appreciate your contribution)--and it's GPL'd.
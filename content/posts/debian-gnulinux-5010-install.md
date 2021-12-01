---
title: 'Debian GNU/Linux 5.0.10 "lenny" install'
date: 2012-09-09T14:13:00.000-07:00
draft: false
tags: 
- linux
- debian
---

Installing Debian GNU/Linux 5.0.10 "lenny" on a HP compaq nc6000, p/n DE646AV.  
  
_Even though Debian GNU/Linux 6.0.5 "squeeze" was available, I opted for the previous release, in an attempt to avoid install error #[681656](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=681656)._  
  
Downloaded the netinst CD image (generally 135-175 MB) and burned to USB using program unetbootin.  

*   Installed Unetbootin support package 7-zip
*   Formatted USB 8GB pen drive as FAT32 using Red Hat Disk Utility 3.0.2

*   Format drive > Master Boot Record > Format
*   Create partition > FAT > Create
*   Mount volume

*   Unetbootin with ISO file debian-5010-i386-netinst.iso to /dev/sdb1 > OK
*   Reboot
*   Fails to detect network hardware

I give up and try a workaround for Debian GNU/Linux 6.0.5 "squeeze": using the nightly builds.
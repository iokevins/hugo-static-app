---
title: 'Debian GNU/Linux 6.0.5 "squeeze" install'
date: 2012-09-09T17:39:00.000-07:00
draft: false
tags: 
- linux
- debian
---

After Debian GNU/Linux 5.0.10 "lenny" net install [failed](http://schultkl.blogspot.com/2012/09/debian-gnulinux-5010-lenny-install.html) to detect my network hardware, I attempted to install the latest daily image of Debian GNU/Linux 6.0.5 "squeeze".  
  
Via comment #[35](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=681656#35) of bug [681656](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=681656), some users reported success using a daily image to work around an install bug in the latest stable release.  
  
Downloaded the [mini ISO from 2012-09-09](http://d-i.debian.org/daily-images/i386/20120909-00:19/netboot/) and burned to USB using program unetbootin.  

*   Formatted USB 8GB pen drive as FAT32 using Red Hat Disk Utility 3.0.2

*   Format drive > Master Boot Record > Format
*   Create partition > FAT > Create (then wait for USB light to stop)
*   Mount volume

*   Unetbootin with ISO file mini.iso to /dev/sdb1 > OK
*   Reboot
*   Fails to detect network hardware
*   I edit /bin/check-missing-firmware, adding "exit 0" after #!/bin/sh
*   This successfully gets me past this stage
*   Installation continues
*   The installer hangs again ... I forget where

Two other options:

1.  Use alpha release
2.  Edit /bin/mountmedia 

I opt for #1, first, downloading the [mini ISO from 2012-05-20](http://d-i.debian.org/daily-images/i386/20120520-00:22/netboot/) and burning to USB as above, then rebooting.  

*   Edited /bin/check-missing-firmware, as before
*   Ran into missing kernel modules error after selecting squeeze or wheezy (no option for lenny) x\_x ... going forward, it does not seem to detect the hard disk
*   Noted Ctrl+Alt+F4 reports "Failed to load tigon /tg3\_ts05.bin"
*   Aborted

Researched and [discovered](http://wiki.debian.org/Firmware) this represents the Broadcom Tigon3 ethernet driver.

*   Per the firmware [pagipw2100e](http://wiki.debian.org/Firmware), I downloaded the squeeze current non-free [tarball](http://cdimage.debian.org/cdimage/unofficial/non-free/firmware/squeeze/current/) to the root of the reformatted squeeze 2012-09-09 Mini ISO.

Then I noticed [http://cdimage.debian.org/cdimage/unofficial/non-free/cd-including-firmware/current/i386/iso-cd/](http://cdimage.debian.org/cdimage/unofficial/non-free/cd-including-firmware/current/i386/iso-cd/) ... trying this ISO first...re-formatted, re-imaged....  

*   For good measure, also downloaded firmware.tar.gz from [http://cdimage.debian.org/cdimage/unofficial/non-free/firmware/squeeze/current/](http://cdimage.debian.org/cdimage/unofficial/non-free/firmware/squeeze/current/) to the USB /firmware folder
*   Rebooted.
*   No problem with the Tigon3...network detection goes smoothly...but error detecting ipw2100-1.3.fw, the Intel(R) PRO/Wireless 2100 Network Driver (?)

Honestly, at this point I do not remember what specifically happened; it froze again, I took down the following notes:

*   Error, "Firmware ipw2100-1.3.fw not available or load failed"
*   Edited /bin/check-missing-firmware, as before
*   Process /sbin/reopen-console /sbin/debian-installer exited...
*   Check hardware completes
*   Menu item disk-detect selected
*   "Detecting disks and all other hardware"
*   I Ctrl-C a few times, go back and forth between Ctrl+F4 (system messages), Ctrl-F3 (started a shell), and Ctrl-F1 (install screen)...
*   Next thing I know, the installer has started up the partitioner
*   And then I hit the screen which asked where to install...I took a deep breath, selected my primary drive, and went with it. It installed OK. Whole process took ~40 minutes.

Soo....

  

I'm in!
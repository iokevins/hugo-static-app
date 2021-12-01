---
title: 'Ubuntu 14.04.2 LTS (Trusty Tahr) to Dell Inspiron 15r'
date: 2015-04-04T10:25:00.000-07:00
draft: false
---

Learned from my experiences [last time](http://iokevins.blogspot.com/2013/01/installing-ubuntu-to-dell-inspiron-15r.html):  
  

*   Downloaded latest Ubuntu 14.04.2 LTS (Trusty Tahr) ISO from a mirror, using UC Santa Cruz connectivity (1.0GB in ~10 minutes)
*   Disk Utility 3.0.2 used to wipe a 16GB USB thumb drive, then reformat the drive as a bootable 2GB FAT16 partition
*   Installed unetbootin
*   Used unetbootin to write the ISO to the USB thumb drive
*   Booted the Dell Inspiron 15r from the USB thumb drive (F12 to select boot device)

From there, I followed the prompts, no problems--wiped the entire drive of Microsoft Windows and the previous Ubuntu install. No need to re-install GRUB. Configured encrypted hard drive and home directory, connected to Wi-Fi, connected to network printer, and so forth.

  

Success!
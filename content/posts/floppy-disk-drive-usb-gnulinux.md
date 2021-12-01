---
title: 'Floppy disk drive (USB) + GNU/Linux'
date: 2015-04-12T17:37:00.000-07:00
draft: false
tags: 
- linux
---

Today I used a floppy diskette drive (USB) for the first time in years, to migrate some media I had in long-term storage.  
  
NOTES  
  

*   [Noises](https://www.youtube.com/watch?v=7Qz9a8kYYkA) of floppy drive brought a smile -- though I seem to recall if the floppy sounds that bad, it most likely will not last much longer (?)
*   Purchased the FDD for ~$15
*   For GNU/Linux, I ended up mounting the USB floppy as follows:

*   Connect the drive and USB
*   sudo blkid -c /dev/null

*   This will list your device (for me, it was /dev/sdb)
*   Alternatively: 

*   udisks --mount /dev/sdb
*   Nautilus then displayed the drive
*   To unmount, I used Nautilus

Not pretty, but we got there--now I can ditch this old media! Next weekend, I will tackle some old ZIP disks.
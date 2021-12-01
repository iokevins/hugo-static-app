---
title: 'Steam Game Migration: Laptop A, Hard Drive, to Laptop B, USB 3.0 external storage drive'
date: 2015-03-27T00:06:00.000-07:00
draft: false
---

Recently moved a Steam installation of "Sid Meier's Civilization: Beyond Earth", per the subject of this post.  
  
A few hiccups, but we got there. Laptop B had an existing installation of Steam on the C:\\ (an internal SSD). However, due to space limitations on the primary internal SSD, we wanted to install the downloadable content on an external USB SSD (in this case, a Samsung T1 Portable 250GB USB 3.0 External SSD).  
  

*   Uninstalled Steam on Laptop B C:\\
*   Re-installed Steam on Laptop B external USB SSD (D:\\Steam) (note: in retrospect, probably could have left Steam on the C:\\ and configured Steam to look in D:\\Steam as a library location, instead...however, this may not represent much of an issue, moving forward)
*   Connect external USB SSD to Laptop A
*   Copy Laptop A Steam subfolder "Steamapps" to external USB SSD (note: **need to ensure manifest file(s) gets copied**...for example, Steam\\Steamapps\\appmanifest\_65980.acf)
*   Connect external USB SSD to Laptop B
*   Start Steam on Laptop B
*   [Verify integrity of the game cache](https://support.steampowered.com/kb_article.php?ref=2037-QEUH-3335) on Laptop B

Once verified, proceed with playing the game.

  

At this point, we need to test whether running the game from the USB 3.0 flash drive will work, performance-wise.  
  
UPDATE: Performance seems quite acceptable.
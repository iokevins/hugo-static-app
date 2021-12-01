---
title: 'Steam Folder Migration: USB 3.0 external storage drive, to internal SSD'
date: 2015-08-02T10:43:00.000-07:00
draft: false
---

We recently complete updating storage on Dawn's laptop, [adding additional capacity and modifying partition sizes](http://iokevins.blogspot.com/2015/06/cloning-increasing-ssd-partitions-of.html).  
  
Today, we moved the Steam folder, from a Samsung T1 Portable 250GB USB 3.0 External SSD, to her newly expanded laptop internal SSD, loosely following the instructions on the [Steam web site](https://support.steampowered.com/kb_article.php?ref=7418-YUBN-8129):  

*   Exit the Steam client application
*   Browse to the Steam installation folder for the Steam installation you would like to move (D:\\Steam, for us)
*   Copy the folder to the new location; for example: C:\\Program Files\\Steam
*   Delete all of the files and folders, in C:\\Program Files\\Steam, except the SteamApps folder and Steam.exe
*   Rename D:\\Steam to D:\\SteamBackup
*   For the first time only, launch Steam via "Run as Administrator", then log into your account

*   Running as non-Administrator, Steam produced an error which said (paraphrasing): "Could not connect; please connect to a network and try again
*   Running as Administrator did not produce the error

*   [Verify integrity of game cache(s)](https://support.steampowered.com/kb_article.php?ref=2037-QEUH-3335):

*   From the Library section, right-click on the game and select Properties from the menu
*   Select the Local files tab and click the Verify integrity of game cache... button
*   Steam will verify the game's files - this process may take several minutes
*   Once the process is completed, the Check Window will automatically exit

*   Manually update the Start Menu shortcut, for Steam: right-click on the icon, select Properties, then change the location the shortcut points to, so it points to the new folder (for us, we changed it from D:\\Steam\\Steam.exe, to C:\\Program Files\\Steam\\Steam.exe)

Done. 

  

NOTES  

*   After you have some confidence that Steam works as expected, you can either keep D:\\Steam as a backup, or delete it
*   OK to start Steam as non-administrator, for all future uses...that first time, above, Steam needs administrator rights to repair itself

[Previously](http://iokevins.blogspot.com/2015/03/steam-game-migration-larptop-hard-drive.html), [previously](http://iokevins.blogspot.com/2015/06/lenovo-thinkpad-x1-carbon-2nd.html), [previously](http://iokevins.blogspot.com/2015/06/cloning-increasing-ssd-partitions-of.html).
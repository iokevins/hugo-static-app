---
title: 'CloneZilla LiveCD + Samba + Windows XP = Disk Image Happiness'
date: 2009-06-21T16:04:00.000-07:00
draft: false
---

[![](http://2.bp.blogspot.com/_xmqk7LpXiyY/Sj7HcB_lw3I/AAAAAAAAAiE/8JMhREtJWeo/s320/clonezilla_logo_transparent.gif)](http://2.bp.blogspot.com/_xmqk7LpXiyY/Sj7HcB_lw3I/AAAAAAAAAiE/8JMhREtJWeo/s1600-h/clonezilla_logo_transparent.gif)  
Situation: I want to clone a laptop hard drive (30GB of 40GB used) to a destination laptop hard drive (also 40GB, identical hardware) using CloneZilla. I am out of DVDs, unfortunately, and burning tens of CDs does not sound pleasant.  
  
CloneZilla ([http://clonezilla.org/](http://clonezilla.org/)) and Samba ([http://en.wikipedia.org/wiki/Samba\_(software)](http://en.wikipedia.org/wiki/Samba_%28software%29)) to the rescue! I have a desktop running Windows XP with 200GB storage, so I installed Samba on it and connected using CloneZilla Live to save/restore the image.  

1.  Get CloneZilla Live ([http://clonezilla.org/clonezilla-live/](http://clonezilla.org/clonezilla-live/)) and burn the ISO to a CD  
      
    
2.  Install Samba on Windows XP via instructions at [http://smithii.com/samba  
      
    ](http://smithii.com/samba)Note: my Windows XP desktop has storage on a separate physical drive (namely, "P:\\"). By default, the Samba setup for Windows creates a share point on C:\\windows\\temp. To setup a share point on a separate drive: (1) create a registry entry for the destination folder in "HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Cygnus Solutions\\Cygwin\\mounts v2", in similar fashion to the keys already there. For example, my destination drive is P:\\, so I created new key "/p" with REG\_DWORD "flags" set to 'a' and REG\_SZ "native" set to "P:\\SAMBA". Ensure folder P:\\SAMBA exists--I also shared folder P:\\SAMBA on the local network, but I am not sure if this was necessary; (2) Edit file "C:\\Program Files\\samba\\lib\\smb.conf" to have another entry similar to "tmp" but pointing to the new share. For example, I created new share point "p" with attributes "comment = /cygdrive/p/samba", "path = /cygdrive/p/samba", "writable = yes", and "public = yes"; (3) Restart the Samba daemons. Namely, kill all existing processess named "nmbd.exe" and "smbd.exe", then run "cd /d C:\\Progra~1\\samba" and "start\_daemons.cmd"; (4) Verify everything looks correct by running "smbclient -L localhost -U guest%password"  
      
    
3.  Boot source laptop with CloneZilla Live CD. Go through the normal steps (if using [http://clonezilla.org/clonezilla-live/doc/](http://clonezilla.org/clonezilla-live/doc/), steps "Save Disk Image, 1-7") until you reach "Mount CloneZilla Image Directory". Select "samba\_server". The Windows XP desktop was on local IP 192.168.1.100. Domain was given by running command "smbclient -L localhost -U guest%password" on the Windows XP desktop. For mount point I used "/p". I used user "administrator" with appropriate password (I had changed using command "smbpasswd administrator" on the Windows XP desktop). After that everything went smooth!  
    

Notes:  

*   Takes a while. Currently projected to take around six hours. Would run faster if the desktop computer was not on wireless. No hurry to get it done though. Averaging around 80-100 Mb/s transfer rate.  
      
    
*   I am sure there is a better way to do this that people will tell me.

  
UPDATE:  
  

*   The first attempt over wireless failed. It said it finished transferring all the data, but in my haste I rebooted before it had completed all the steps.
*   For the second attempt, I plugged the destination directly into the router, so everything went over wired network. The speedup was tremendous (factor of 5x). Instead of 6.5 hours, it took ~1.25 hours.
*   The second attempt failed. It completed successfully, but a reboot showed only a blinking cursor.
*   The third attempt worked. It completed successfully, and a reboot loaded Windows XP.

Unfortunately, the laptop I loaded the image onto only has 512 MB RAM and no wireless card--so it is unusable for now until I get more RAM. :)  
  
Mission accomplished!
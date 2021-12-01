---
title: 'Amazon EC2 Ubuntu 12.04 LTS Remote Desktop via NoMachine 4'
date: 2013-10-25T00:00:00.000-07:00
draft: false
tags: 
- linux
---

[http://cloud.ubuntu.com/ami/](http://cloud.ubuntu.com/ami/)  
  
This was the link which assisted me with getting everything working, using Ubuntu 12.04 LTS and NoMachine 4:  
[http://www.crouse.cc/blog/of-on-ec2.html](http://www.crouse.cc/blog/of-on-ec2.html)  
  
Then:  
  
[https://help.ubuntu.com/community/CitrixICAClientHowTo#Citrix\_ICA\_Client\_12\_on\_Ubuntu\_12.04\_64-bit](https://help.ubuntu.com/community/CitrixICAClientHowTo#Citrix_ICA_Client_12_on_Ubuntu_12.04_64-bit)  
  
Fixing wcamgr:  
[http://ubuntuforums.org/showthread.php?t=1913988](http://ubuntuforums.org/showthread.php?t=1913988)  
  
Using rdesktop:  
[http://dcook.org/gobet/using\_amazon\_ec2.html](http://dcook.org/gobet/using_amazon_ec2.html)  
  
Some other links:  
  

*   http://activeintelligence.org/blog/archive/remote-graphical-linux-desktop-on-ec2/
*   https://help.ubuntu.com/community/FreeNX

Notes

*   I tried 13.x Ubuntu images but failed to get them working 
*   Added user ec2usr as admin to the image
*
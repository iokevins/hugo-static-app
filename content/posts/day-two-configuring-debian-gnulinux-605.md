---
title: 'Day two - Configuring Debian GNU/Linux 6.0.5 "squeeze"'
date: 2012-09-10T21:19:00.000-07:00
draft: false
tags: 
- linux
- debian
---

_Add image of Carl Sagan to Cosmos screensaver_  
  

*   cd /usr/share/backgrounds/cosmos && sudo wget http://apod.nasa.gov/apod/image/9612/sagan\_uc\_big.jpg
*   Because...Carl Sagan...Cosmos

_Investigate clicking when hard drive parks head_

*   Via this [post](http://www.thinkwiki.org/wiki/Problem_with_hard_drive_clicking), I hear a clicking when the hard drive parks it's head.
*   Quiet, but noticeable
*   sudo hdparm -B 254 /dev/sda
*   Still hearing the hard drive parking it's head

*   ATA FUJITSU MHT2040A 006C PQ : 0 ANSI: 5
*   Install smartmontools package via Software Center
*   Ran sudo smartctl -A /dev/sda ... not sure how to parse the results
*   Edited /etc/hdparm.conf 

*   sudo vim /etc/hdparm.conf 
*   apm = 255
*   apm\_battery = 255
*   sudo update-rc.d hdparm defaults

*   ?

  

_Configure printing_

*   System > Administration > Printing
*   Add > Printer
*   Expand "Network Printer"
*   Select "HP LaserJet CP1525nw"...popup "Searching for drivers" appears
*   Select "Select printer from database", then "HP", then button "Forward"
*   Select model "Color LaserJet cp1518ni" and Drivers "HP Color LaserJet cp1518ni hpijs pcl3, 3.10.6 \[en\] (recommended), then select button "Forward"
*   Set Printer Name = HP-Color-LaserJet-cp1525nw, Description = HP Color LaserJet cp1525nw, then select button "Apply"
*   Authenticate to complete the test, if necessary
*   Print test page...prints successfully in color
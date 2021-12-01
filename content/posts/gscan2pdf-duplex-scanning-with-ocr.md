---
title: 'gscan2pdf - Duplex scanning, with OCR'
date: 2015-08-24T21:21:00.000-07:00
draft: false
tags: 
- linux
- debian
---

After [setting up my Fujitsu ScanSnap S1300i on Debian Jessie (stable)](http://iokevins.blogspot.com/2015/08/debian-linux-and-fujitsu-scansnap-s1300i.html), I began scanning duplex pages:  
  

*   sudo gscan2pdf
*   Place pages into scanner, face down
*   File > Scan

*   Select device (in my case, "FUJITSU ScanSnap S1300i")
*   Page Options Tab

*   \# Pages: All
*   Source Document: Single sided (note: we select duplex, later)
*   Select button "Options", for line "Clean up images"

*   Select tab "Filters"

*   White threshold: 0.90
*   Black threshold: 0.48 (note: this currently does not save, for me!)

*   Scan Mode Tab

*   Scan Source: ADF Duplex (note: this scans both sides at once!)
*   Scan mode: Lineart (note: best for scanning text)
*   Scan resolution: 300

*   Geometry Tab: accept defaults
*   Enhancement Tab:

*   Threshold: 50 (note: this helps cleans up artifacts)

*   Sensors Tab: accept defaults

*   Page options > Scan button
*   Close the popup window
*   File > Save

If you like, save the Scan Profile.

  

LINKS

[http://ubuntuforums.org/showthread.php?t=1681579](http://ubuntuforums.org/showthread.php?t=1681579)
---
title: 'Cloning, Increasing SSD Partitions of Lenovo ThinkPad X1 Carbon, 2nd Generation (Rel 2)'
date: 2015-06-27T22:03:00.000-07:00
draft: false
---

Used a Transcend 512 GB SATA III SSD, in the following enclosure, to clone the existing 128GiB SSD: "ZTC Thunder Enclosure NGFF M.2 SSD to USB 3.0 Adapter. Support UASP SuperSpeed 6Gb/s 520MB/s Black Model ZTC-EN004-BK"  

*   Really tough to insert the Transcend SSD drive into the ZTC M.2 SSD to USB 3.0 Adapter board (the adapter board and SSD then gets inserted into the enclosure)
*   The adapter's USB 3.0 Micro-B [receptacle](https://en.wikipedia.org/wiki/USB#Host_and_device_interface_receptacles) seemed poorly soldered, most likely a factory defect

*   After inserting the USB 3.0 Micro-B plug, Microsoft Windows recognized the adapter, then, after a few seconds, lost connection to it
*   The adapter's blue LEDs turned on/off in the same way
*   Physically bumping the adapter seemed to produce the same effect
*   After some experimentation, I discovered flexing the USB 3.0 Micro-B receptacle, at a downward angle, allowed for a reliable connection

*   After finding the workaround mentioned above, I sat for nearly 18 minutes, holding the adapter board perfectly still, at this angle, to complete the clone of the existing disk
*   We did not use the aluminum enclosure, just the M.2 SSD to USB 3.0 Adapter...due to the faulty soldering...having the adapter in the enclosure did not allow for the workaround
*   We used software [Macrium Reflect Free](http://www.macrium.com/reflectfree.aspx), version 6.0.685 (17 June 2015); it worked perfectly--love it!

After cloning the internal disk, we replaced the 128GiB X1 Carbon internal SSD with the new 512GiB SSD:

*   This went smoothly
*   We needed to apply a non-trivial amount of force to unscrew the screw holding down the SSD
*   Insertion of the Transcend 512 GB SATA III drive was no problem

Rebooting showed everything as expected!

  

Due to dual-OS configuration, on one disk, enlarging partitions had a few wrinkles:

*   The original 128GB SSD had a hidden, 7GiB [Intel Rapid Start Technology (IRST)](http://download.intel.com/support/motherboards/desktop/sb/rapid_start_technology_user_guide_for_uefi1.pdf) partition, as the last partition
*   We found no partition editors which would allow us to move this partition 
*   After disabling BIOS IRST support and doing some research, we deleted this partition, with no ill effect
*   The vendor seems to have labeled this partition "OEM", which caused a bit of confusion, initially...many posts advised, rightfully so, to not delete the OEM partition
*   After deleting the IRST partition, we successfully moved the Ubuntu swap partition, allowing room to expand the main Ubuntu partition size
*   After a reboot, we increased the partition size of the Microsoft Windows 8 C:\\ partition (after taking a risk and deleting a 1.0 MiB partition which seemed unused)
*   We also created a new IRST partition:

*   Type = Unformatted
*   Drive Letter = None
*   Use diskpart to [set the ID](http://download.intel.com/support/motherboards/desktop/sb/rapid_start_technology_user_guide_for_uefi1.pdf) to D3BFE2DE-3DAF-11DF-BA40-E3A556D89593

*   After creating the IRST partition, we re-enabled IRST in BIOS
*   Hibernation works, as expected, with the system going into Microsoft Windows [S4 sleep mode](https://en.wikipedia.org/wiki/Hibernation_(computing)#Microsoft_Windows)

So far, all seems well. Ubuntu and Microsoft Windows work, as expected. 

  

Cleanup tasks:

*   Migrate files from external USB 3.0 SSD to internal USB 3.0 SSD
*   Update Ubuntu
*   (?)

[Previously](http://iokevins.blogspot.com/2015/06/lenovo-thinkpad-x1-carbon-2nd.html)
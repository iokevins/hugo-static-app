---
title: 'GNOME: Turning off notifications when charging device via usb'
date: 2017-05-06T15:03:00.000-07:00
draft: false
---

gsettings set org.gnome.desktop.media-handling autorun-never true  
  
Due to a slightly wonky USB cable, GNOME kept displaying notification popups identifying my device as newly available.  
  
To re-enable:  
  
gsettings set org.gnome.desktop.media-handling autorun-never false  

  

Note: this disables the GNOME popups, but not necessarily the Deny/Allow popups on the phone itself. One way of suppressing this seems to involve enabling USB Debugging mode:  
  

1.  From a Home screen, tap Apps Apps icon (located in the lower-right).
2.  Tap Settings.
3.  Tap About device.
4.  Tap the Build number field 7 times. Note This unlocks Developer options.
5.  Tap the Back arrow (located in the upper left).
6.  Tap Developer options (note: bottom).
7.  Ensure the Developer options switch is enabled Switch On icon.
8.  Tap the USB debugging switch to enable Switch On icon.
9.  If presented with "Allow USB debugging", tap OK.

Via:

[https://askubuntu.com/questions/88051/how-can-i-stop-gnome-shells-drive-pop-up-notifications](https://askubuntu.com/questions/88051/how-can-i-stop-gnome-shells-drive-pop-up-notifications)  
[https://www.verizonwireless.com/support/knowledge-base-203783/](https://www.verizonwireless.com/support/knowledge-base-203783/)
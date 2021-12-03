---
title: 'Debian Wheezy + Logitech Mini Boombox'
date: 2014-12-11T18:33:00.000-08:00
draft: false
tags: 
- linux
- debian
---

[![](/images/mini-boombox.png)](/images/mini-boombox.png)

A friend recently gifted me a [Logitech Mini Boombox](http://support.logitech.com/en_us/product/8725) (Model F-00003, p/n 880-000243). Logitech introduced this product in the United States market in 2011 at a price point of about $100.  
  
This product supports Bluetooth 2.1 and can play music up to 33 feet away. It supports four [Bluetooth profiles](http://en.wikipedia.org/wiki/List_of_Bluetooth_profiles):  

1.  Advanced Audio Distribution Profile ([A2DP](http://en.wikipedia.org/wiki/List_of_Bluetooth_profiles#Advanced_Audio_Distribution_Profile_.28A2DP.29))
2.  Audio/Video Remote Control Profile ([AVRCP](http://en.wikipedia.org/wiki/List_of_Bluetooth_profiles#Audio.2FVideo_Remote_Control_Profile_.28AVRCP.29))
3.  Hands-Free Profile ([HFP](http://en.wikipedia.org/wiki/List_of_Bluetooth_profiles#Hands-Free_Profile_.28HFP.29))
4.  Headset Profile ([HSP](http://en.wikipedia.org/wiki/List_of_Bluetooth_profiles#Headset_Profile_.28HSP.29))

GNU/LINUX DEBIAN WHEEZY CONFIGURATION  
  
Initially, I successfully paired the device to my IBM Lenovo X201 laptop...no problems. However, the device did not appear under "Sound Settings" tab "Hardware" (that is, GNOME control center - Sound)  
  
After a bunch of web searches and unsuccessful configurations of /etc/bluetooth/audio.conf (note: I eventually reverted it to default and it was fine), it turned out installing pulseaudio-module-bluetooth seemed to allow the device to appear:  
  
**sudo apt-get install pulseaudio-module-bluetooth**  

**pacmd load-module module-bluetooth-discover**

  

Note: I may have ran "pulseaudio -k" to restart audio...and the sound comes through with static...some fine-tuning still needs to occur.  
  
UPDATE: to improve audio quality, access control panel "GNOME control center - Sound" (that is, "Sound Settings"), select tab "Hardware," then select device "Mini Boombox", then, under section "Settings for the selected device," select profile "High Fidelity Playback (A2DP)" from the pull-down list. ([Via](http://milianw.de/blog/logitech-mini-boombox-on-linux))  
  
UPDATE: after a reboot, ran pulseaudio -k again before I could get it to work  
  
UPDATE, 2015-05-03: Fresh install of Debian Jessie and everything works after installing pulseaudio-module-bluetooth and running pacmd.  
  
UPDATE: 2015-10-25:  
Bluetooth pairing stopped about a week ago. At first, I suspected recent system updates to my Debian Jessie install. This weekend, I noticed my mobile Android device also did not pair. Solution: turn off the Mini Boombox and unplug from the power source. The light on the front of the Mini Boombox will turn dark. Now, after unpairing the Mini Boombox from within Bluetooth settings, reboot the device. After reboot, plug in the Mini Boombox and turn it on. Pairing now seems to work as expected. However, the paired device did not appear in the Sound Options screen. To fix:  
sudo apt-get install --reinstall pulseaudio pulseaudio-utils pulseaudio-module-bluetooth

sudo apt-get install --reinstall bluez bluez-alsa bluez-audio bluez-gstreamer bluez-hcidump bluez-tools bluez-utils  
Note: not all packages will install.

([via](http://askubuntu.com/questions/370254/how-can-i-get-the-a2dp-output-option-and-the-input-working-again))  
  
UPDATE: 2015-10-26  
Learning about Bluetooth, PulseAudio, ALSA, and so forth. Opening Bluetooth Settings and removing the Mini Boombox device activates my headphones, if jacked in. After pairing the Mini Boombox again, I can now control sound to Output devices "Headset - Mini Boombox" and "Speakers - Built-in Audio", via Sound applet. When I jack in my headphones, music plays to Output "Headphones - Built-in Audio". When I remove my headphones, output goes to device "Headset - Mini Boombox". If I am playing sound via Output "Headset - Mini Boombox" and I plug-in my headphones to the headset jack, nothing happens; music continues to play to Output "Headset - Mini Boombox". So, much better than before, but still not quite dialed-in the way I want.
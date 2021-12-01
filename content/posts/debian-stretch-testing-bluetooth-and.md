---
title: 'Debian Stretch (Testing): Bluetooth and PulseAudio'
date: 2015-11-25T23:06:00.001-08:00
draft: false
tags: 
- audio
- gdm
- testing
- bluetooth
- stretch
- a2dp
- gnome
- manager
- pulseaudio
- debian
- display
---

Debian Stretch (Testing) seems to ship with the following software, as of this writing:  

*   PulseAudio 7.1-2
*   GDM (GNOME Display Manager) 3.18.0-2

GDM seems to capture the A2DP sink, on session start, resulting in two PulseAudio processes.

#### WORKAROUND #1: GDM

The Debian Wiki A2DP page details a workaround, to disable GDM pulseaudio use:

*   echo -e "autospawn = no\\ndaemon-binary = /bin/true" | sudo tee /var/lib/gdm3/.config/pulse/client.conf
*   sudo chown Debian-gdm:Debian-gdm /var/lib/gdm3/.config/pulse/client.conf
*   Fix 

*   sudo vim /etc/pulse/default.pa
*   add string: load-module module-switch-on-connect
*   Note: I added after command ""

This seems to successfully stop my Debian Stretch system from having user Debian-gdm (note: in ps and top, Debian lists this user as "Debian-+", which represents the first seven letters, and the plus sign, as an indicator that the name extends past eight characters).  
  
Why does GDM start PulseAudio? [Michael Biebl](https://qa.debian.org/developer.php?login=biebl%40debian.org) writes, in Debian bug #[805414](https://www.mail-archive.com/debian-bugs-dist@lists.debian.org/msg1372708.html):  

> "We need pulseaudio in the gdm session for accessibility, e.g. the screen reader requires it."

That...makes sense.  

#### WORKAROUND #2: CLEANUP

When I first installed Debian Stretch, I successfully paired to a Logitech Mini Boombox. I installed package pulseaudio-module-bluetooth, restarted pulseaudio, paired the device, and everything worked. Brilliant.

  

Now, even after removing GDM from the picture, I can't connect via Bluetooth.

  

So, I decided to start over. However, when I try to remove the Mini Boombox profile, I get an error:

*   bt-device -l
*   Note: shows device "Mini Boombox (10:B7:F6:00:B5:D2)"
*   bt-device -r "10:B7:F6:00:B5:D2"
*   Error: GDBus.Error:org.bluez.Error.NotReady: Resource Not Ready

Manually running GNOME Control Center in verbose mode shows more detail:  
  

*   gnome-control-center -v bluetooth

*   Note: terminal displays a status line and an error line: 

*   (gnome-control-center:8526): Bluetooth-DEBUG: Saving device type Headset for 10:B7:F6:00:B5:D2
*   (gnome-control-center:8526): Bluetooth-DEBUG: Call to Set Powered failed /org/bluez/hci0: GDBus.Error:org.bluez.Error.Blocked: Blocked through rfkill

*   On screen "Bluetooth", I select Device "Mini Boombox"

*   Note: No new output to the terminal

*   On screen "Mini Boombox":

*   Field "Connection" displays the slider in position "Off"
*   I attempt to slide the Connection slider to position "On", but this fails
*   Note: terminal displays two new lines:

1.  (gnome-control-center:8603): Bluetooth-DEBUG: Connect failed for /org/bluez/hci0/dev\_10\_B7\_F6\_00\_B5\_D2: GDBus.Error:org.bluez.Error.NotReady: Resource Not Ready
2.  (gnome-control-center:8603): Bluetooth-DEBUG: Connection failed to 10:B7:F6:00:B5:D2: GDBus.Error:org.bluez.Error.NotReady: Resource Not Ready

*   Close out all windows to exit; no new terminal output

The first error, "Blocked through rfkill" may indicate the result of earlier testing. I unblocked it, via:

*   sudo rfkill list all

*   7: hci0: Bluetooth
*   Soft blocked: yes
*   Hard blocked: no

*   sudo rfkill unblock bluetooth
*   sudo rfkill list all

*   7: hci0: Bluetooth
*   Soft blocked: no
*   Hard blocked: no

Manually running GNOME Control Center, in verbose mode, now shows new detail:

*   gnome-control-center -v bluetooth
*   Note: terminal shows no error after line, "(gnome-control-center:9772): Bluetooth-DEBUG: Saving device type Headset for 10:B7:F6:00:B5:D2", as before
*   Terminal shows three lines, in a loop, while GNOME Control Center screen "Bluetooth" displays a spinning wait icon:

1.  (gnome-control-center:9772): Bluetooth-DEBUG: authorize\_service\_callback (/org/bluez/hci0/dev\_10\_B7\_F6\_00\_B5\_D2, 0000110d-0000-1000-8000-00805f9b34fb)
2.  (gnome-control-center:9772): Bluetooth-DEBUG: Unhandled UUID 0000110d-0000-1000-8000-00805f9b34fb (0x110d)
3.  (gnome-control-center:9772): Bluetooth-DEBUG: authorize\_service\_callback (/org/bluez/hci0/dev\_10\_B7\_F6\_00\_B5\_D2, 00001112-0000-1000-8000-00805f9b34fb)

*   Note: The second line, above, seems to have an error, "Unhandled UUID 0000110d-0000-1000-8000-00805f9b34fb (0x110d)"

Restarting GNOME Control Center, it does let me remove it this time.

  

Restarting GNOME Control Center and attempting to setup the device:

*   gnome-control-center -v bluetooth
*   ...
*   First sequence:

*   (gnome-control-center:11341): Bluetooth-DEBUG: New Device interface added.

*   (gnome-control-center:11341): Bluetooth-DEBUG: Adding device Mini Boombox (/org/bluez/hci0/dev\_10\_B7\_F6\_00\_B5\_D2)
*   (gnome-control-center:11341): Bluetooth-DEBUG: Saving device type Headset for 10:B7:F6:00:B5:D2
*   (gnome-control-center:11341): Bluetooth-DEBUG: Unhandled property: RSSI
*   (gnome-control-center:11341): Bluetooth-DEBUG: Unhandled UUID 0000110d-0000-1000-8000-00805f9b34fb (0x110d)
*   (gnome-control-center:11341): Bluetooth-DEBUG: Removing device 'Mini Boombox'

*   Second sequence:

*   (gnome-control-center:11341): Bluetooth-DEBUG: New Device interface added.
*   (gnome-control-center:11341): Bluetooth-DEBUG: Unhandled UUID 0000110d-0000-1000-8000-00805f9b34fb (0x110d)
*   (gnome-control-center:11341): Bluetooth-DEBUG: Adding device Mini Boombox (/org/bluez/hci0/dev\_10\_B7\_F6\_00\_B5\_D2)
*   (gnome-control-center:11341): Bluetooth-DEBUG: Removing device 'Mini Boombox'

*   The second sequence continues, looping, until the Mini Boombox stops attempting to pair
*   Third sequence:

*   (gnome-control-center:11341): Bluetooth-DEBUG: New Device interface added.
*   (gnome-control-center:11341): Bluetooth-DEBUG: Adding device Mini Boombox (/org/bluez/hci0/dev\_10\_B7\_F6\_00\_B5\_D2)
*   (gnome-control-center:11341): Bluetooth-DEBUG: Removing device 'Mini Boombox'

*   This continues....

Noticed my fingerprint scanner was wonky. Rebooted.  
  
Upon reboot, started GNOME Control Center and noticed the output mentioned "Blocked through rfkill", so I ran "sudo rfkill unblock bluetooth" again.  
  
Rerunning GNOME Control Center, I noticed new results:  
  

*   (gnome-control-center:2101): Bluetooth-DEBUG: Saving device type All types for 10:B7:F6:00:B5:D2
*   (gnome-control-center:2101): Bluetooth-DEBUG: pincode\_callback (/org/bluez/hci0/dev\_10\_B7\_F6\_00\_B5\_D2)
*   (gnome-control-center:2101): Bluetooth-DEBUG: Getting pincode for device 'Mini Boombox' (type: All types address: 10:B7:F6:00:B5:D2)
*   (gnome-control-center:2101): Bluetooth-DEBUG: Got pin '(null)' (max digits: 0, confirm: 1) for device 'Mini Boombox' (type: All types address: 10:B7:F6:00:B5:D2, vendor: plastoform industries ltd.)
*   (gnome-control-center:2101): Bluetooth-DEBUG: cancel\_callback ()
*   (gnome-control-center:2101): Bluetooth-DEBUG: Removing device 'Mini Boombox'
*   (gnome-control-center:2101): Bluetooth-DEBUG: New Device interface added.
*   (gnome-control-center:2101): Bluetooth-DEBUG: Adding device Mini Boombox (/org/bluez/hci0/dev\_10\_B7\_F6\_00\_B5\_D2)
*   (gnome-control-center:2101): Bluetooth-DEBUG: Saving device type Headset for 10:B7:F6:00:B5:D2
*   (gnome-control-center:2101): Bluetooth-DEBUG: pincode\_callback (/org/bluez/hci0/dev\_10\_B7\_F6\_00\_B5\_D2)
*   (gnome-control-center:2101): Bluetooth-DEBUG: Getting pincode for device 'Mini Boombox' (type: Headset address: 10:B7:F6:00:B5:D2)
*   (gnome-control-center:2101): Bluetooth-DEBUG: Got pin '0000' (max digits: 0, confirm: 1) for device 'Mini Boombox' (type: Headset address: 10:B7:F6:00:B5:D2, vendor: plastoform industries ltd.)
*   (gnome-control-center:2101): Bluetooth-DEBUG: authorize\_service\_callback (/org/bluez/hci0/dev\_10\_B7\_F6\_00\_B5\_D2, 0000110d-0000-1000-8000-00805f9b34fb)
*   (gnome-control-center:2101): Bluetooth-DEBUG: Unhandled UUID 0000110d-0000-1000-8000-00805f9b34fb (0x110d)
*   (gnome-control-center:2101): Bluetooth-DEBUG: authorize\_service\_callback (/org/bluez/hci0/dev\_10\_B7\_F6\_00\_B5\_D2, 00001112-0000-1000-8000-00805f9b34fb)

  

On screen "Bluetooth", a popup displayed with the PIN. I think I selected OK. The terminal kept reporting the above messages. But, no success.

  
Google-fu for phrase "Unhandled UUID 0000110d-0000-1000-8000-00805f9b34fb (0x110d)" leads to [this post](https://bbs.archlinux.org/viewtopic.php?id=197826), which leads to this post, which leads me to try the following:  
  

*   modprobe

without success. Continuing to [the next post](https://bugzilla.redhat.com/show_bug.cgi?id=1186062), which hints at the following troubleshooting tools:

*   hciconfig
*   sudo journalctl -u bluetooth --since="2015-11-25"
*   Note: at this point, I notice new error from bluetoothd, "Failed to obtain handles for "Service Changed" characteristic"

Googling for [this](https://www.google.com/search?q=bluetoothd+Failed+to+obtain+handles+for+%22Service+Changed%22+characteristic) results in a link to Ubuntu but #[1499858](https://bugs.launchpad.net/ubuntu/+source/bluez/+bug/1499858), which hints at a dup of Ubuntu bug #[1490349](https://bugs.launchpad.net/ubuntu/+source/bluez/+bug/1490349), which leads me to a [first working workaround solution](https://bugs.launchpad.net/ubuntu/+source/bluez/+bug/1490349/comments/4):

*   sudo vim /etc/pulse/system.pa
*   Append the following:

*   \### Automatically load driver modules for Bluetooth hardware
*   .ifexists module-bluetooth-policy.so
*   load-module module-bluetooth-policy
*   .endif
*     
    
*   .ifexists module-bluetooth-discover.so
*   load-module module-bluetooth-discover
*   .endif

*   pulseaudio -k

  
And...when I go back into GNOME Control Center, I can connect. o\_O

#### BLUETOOTH HARDWARE

On my Lenovo Thinkpad X201, I see the following Bluetooth hardware:

*   hcitool dev

*   hci0  78:DD:08:A4:16:A3

*   hciconfig

*   hci0:  Type: BR/EDR  Bus: USB
*   BD Address: 78:DD:08:A4:16:A3  ACL MTU: 1021:8  SCO MTU: 64:1
*   UP RUNNING PSCAN ISCAN 
*   RX bytes:18982 acl:438 sco:0 events:681 errors:0
*   TX bytes:11170 acl:456 sco:0 commands:214 errors:0

*   lsusb -v | grep -E '\\<(Bus|iProduct|bDeviceClass|bDeviceProtocol)' 2>/dev/null

*   Bus 001 Device 010: ID 0a5c:217f Broadcom Corp. BCM2045B (BDC-2.1)
*     bDeviceClass          224 Wireless
*     bDeviceProtocol         1 Bluetooth
*     iProduct                2 

*   Note: [via](https://wiki.debian.org/HowToIdentifyADevice/USB)
*   dmesg reports:

*   \[ 4636.805229\] usb 1-1.4: new full-speed USB device number 10 using ehci-pci
*   \[ 4636.901666\] usb 1-1.4: New USB device found, idVendor=0a5c, idProduct=217f
*   \[ 4636.901674\] usb 1-1.4: New USB device strings: Mfr=1, Product=2, SerialNumber=3
*   \[ 4636.901681\] usb 1-1.4: Product: Broadcom Bluetooth Device
*   \[ 4636.901685\] usb 1-1.4: Manufacturer: Broadcom Corp
*   \[ 4636.901688\] usb 1-1.4: SerialNumber: 78DD08A416A3

*   217f = BCM2045B (BDC-2.1) ([via](http://www.linux-usb.org/usb.ids))
*   BDC = Bluetooth Daughter Card
*   2.1 = Bluetooth 2.1
*   [Details - ThinkWiki](http://www.thinkwiki.org/wiki/Bluetooth_Daughter_Card_(14_pins)):

*   USB ids

*   0A5C:2145
*   0A5C:217F

*   Broadcom BCM92070MD
*   HCI/LMP version 2.1
*   Firmware 104.66 / 3
*   (information from hciconfig hciX features/version/revision)

#### NOTES

  

#### RESOURCES

Debian

*   [Debian Wiki - A2DP](https://wiki.debian.org/BluetoothUser/a2dp)
*   [Logging PulseAudio Errors](https://wiki.ubuntu.com/PulseAudio/Log)

PulseAudio

*   [Wikipedia - PulseAudio](https://en.wikipedia.org/wiki/PulseAudio)
*   Steve Litt's [Troubleshooting Linux Sound](http://www.troubleshooters.com/linux/sound/sound_troubleshooting.htm) (note: useful as background info)

Bluetooth
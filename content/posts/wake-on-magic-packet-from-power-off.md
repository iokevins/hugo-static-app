---
title: 'Wake on Magic Packet from power off state'
date: 2015-12-14T19:19:00.001-08:00
draft: false
tags: 
- adapter
- intel
- dual boot
- wake on lan
- card
- driver
- e1000e
- ethernet
- windows
- linux
- gnu
- magic packet
- i1217-lm
- network
---

Recent Dell OptiPlex 9020 Mid Tower shipments include Gigabit Ethernet (GbE). Ours had an integrated [Intel Ethernet Connection i217-LM](http://www.intel.com/content/www/us/en/embedded/products/networking/ethernet-connection-i217-family.html) network adapter, which Intel markets as "Corporate LAN product with support for [Intel vPro](https://en.wikipedia.org/wiki/Intel_vPro) technology, [Intel AMT2](https://en.wikipedia.org/wiki/Intel_AMT_versions), [Energy Efficient Ethernet](https://en.wikipedia.org/wiki/Energy-Efficient_Ethernet) (802.3AZ), [Intel SIPP](http://www.intel.com/content/www/us/en/computer-upgrades/pc-upgrades/sipp-intel-stable-image-platform-program.html), [iSCSI Boot](https://en.wikipedia.org/wiki/ISCSI#Network_booting), Server OS support". Intel also markets a consumer-class model, the i217-V.

  

The i217-LM network adapter seems to work flawlessly, in Microsoft Windows. However, in a dual boot operating system configuration, Microsoft Windows network adapter driver setting "**Power Management > Wake on Magic Packet from power off state**", if enabled, seems to prevent network connectivity after soft restarting into GNU/Linux, from Microsoft Windows. Note: a hard reboot (power off), or removing/inserting the power cable (wait until NIC blinkies disappear), enables GNU/Linux network connectivity.

  

This root cause seems to present as other problems:  

*   DHCP fails

*   Utility dhclient, in verbose mode, reports sending DHCPDISCOVER, but no receipt of DHCPOFFER
*   Network sniffer analysis reveals the DHCPDISCOVER requests don't seem to get sent onto the wire
*   Strangely, DHCP also failed under Microsoft Windows 7, which may indicate a DHCP server issue did temporarily exist (note: this was late Friday afternoon, after finals week, on what seems like a less-used subnet)

*   Network adapter reports "network unreachable", via ping requests
*   GNU/Linux seems to indicate a functional e1000e network adapter, via lspci, ifconfig, ethtool, and so forth

(Some comments posit this may only occur when interacting with Gigabit switches, even if 100Mbps or less rates negotiated.)

  

The root cause seems to indicate an issue with the Intel Linux e1000e driver, when dealing with Power Management settings, upon soft restart.  
  

### SPECIFICS (SORT OF)

*   Microsoft Windows 7

*   Network adapter driver:

*   As shipped: 12.something (?)
*   Updated: Intel PROSet Version: 20.4.1 (Latest, as of this writing), Date: 10/2/2015

*   Ubuntu 15.04

*   Network adapter driver: 

*   e1000e, version 2.3.2-k, firmware version 0.13-4
*   e1000e, version 3.2.4.2-NAPI (note: "New API")

*   Network connectivity still failed, for us, after modprobe -r e1000e && modprobe e1000e (note: we verified the 3.2.4.2-NAPI driver was loaded)
*   We did \*not\* successfully test this driver, upon boot...we successfully did a make install, but we must have missed a step, as, after a reboot, the system had loaded the 2.3.2-k driver
*   We did not pursue it, for science, due to finding the workaround

*   Kernel: 3.19.0-39-generic

### DISABLING SETTING "WAKE ON MAGIC PACKET FROM POWER OFF STATE"

*   In Microsoft Windows, open Device Manager

*   Start > Control Panel
*   Select "System and Security"
*   Under System, select Device Manager
*   Note: Administrator permission required--if you're prompted for an administrator password or confirmation, type the password or provide confirmation

*   In Device Manager, expand "Network Adapters", right-click the adapter, and select Properties
*   In the Properties window, select tab "Power Management"
*   Under section "Wake on LAN", find setting "Wake on Magic Packet from power off state" and uncheck it
*   Select button "OK" to save and exit

Note: we first installed the latest drivers, from intel.com, at [https://downloadcenter.intel.com/product/60019/Intel-Ethernet-Connection-I217-LM](https://downloadcenter.intel.com/product/60019/Intel-Ethernet-Connection-I217-LM) . Namely, as of this writing: Network Adapter Driver for Windows 7\*, Version: 20.4.1 (Latest), Date: 10/2/2015 . You may or may not need to do this, to clear the setting listed above.

### RESOURCES

\[SOLVED\] Ethernet issues after booting Windows (Intel I217-V (e1000e))

[https://bbs.archlinux.org/viewtopic.php?id=191981](https://bbs.archlinux.org/viewtopic.php?id=191981)

  

Intermittent Ethernet on Optiplex 9020 under Xubuntu 15.04

[http://en.community.dell.com/support-forums/software-os/f/3525/t/19649388](http://en.community.dell.com/support-forums/software-os/f/3525/t/19649388)

  

Enabling NIC under Ubuntu 15.04 on Dell Optiplex 9020

[http://askubuntu.com/questions/647624/enabling-nic-under-ubuntu-15-04-on-dell-optiplex-9020/708997#708997](http://askubuntu.com/questions/647624/enabling-nic-under-ubuntu-15-04-on-dell-optiplex-9020/708997#708997)

  

Windows 10 Breaks Debian Ethernet

[https://m.reddit.com/r/debian/comments/3ho7k5/windows\_10\_breaks\_debian\_ethernet/](https://m.reddit.com/r/debian/comments/3ho7k5/windows_10_breaks_debian_ethernet/)

  

Bug#780631: e1000e: Intel I217-V non-functional after booting Windows

[https://lists.debian.org/debian-kernel/2015/03/msg00249.html](https://lists.debian.org/debian-kernel/2015/03/msg00249.html)

  

\[SOLVED\] Intel I217-V wired ethernet not working

[http://ubuntuforums.org/archive/index.php/t-2280968.html](http://ubuntuforums.org/archive/index.php/t-2280968.html)

  

Trying to get Ethernet working in Linux

[http://unix.stackexchange.com/questions/229414/trying-to-get-ethernet-working-in-linux](http://unix.stackexchange.com/questions/229414/trying-to-get-ethernet-working-in-linux)

  

dhcpcd in ArchLinux does not get lease from EdgeRouter Lite

[https://community.ubnt.com/t5/EdgeMAX/dhcpcd-in-ArchLinux-does-not-get-lease-from-EdgeRouter-Lite/td-p/1301442](https://community.ubnt.com/t5/EdgeMAX/dhcpcd-in-ArchLinux-does-not-get-lease-from-EdgeRouter-Lite/td-p/1301442)
---
title: 'Upgrading to Debian GNU/Linux 7 "wheezy" + XFCE'
date: 2013-04-21T10:15:00.000-07:00
draft: false
tags: 
- linux
- debian
---

Last night I took the plunge and upgraded my Debian GNU/Linux 6 "squeeze" install to "wheezy"...here's my running log of updates.  
  
2013-04-20  
  
Referencing [http://www.debian.org/releases/testing/i386/release-notes/ch-upgrading.en.html](http://www.debian.org/releases/testing/i386/release-notes/ch-upgrading.en.html):  
  
sudo dpkg --audit  
grep -q '^flags.\*\\bpae\\b' /proc/cpuinfo && echo yes || echo no    
(returned "no"...old hw without pae : o ( )  
  
sudo vim /etc/apt/sources.list  
\--changed all my sources from squeeze to wheezy. Note: commented out backports for wheezy  
sudo apt-get update  
\--updated sources...this took a few minutes  
sudo apt-get -o APT::Get::Trivial-Only=true dist-upgrade  
\-- this told me whether or not I had enough space for the upgrade (yes)  
sudo apt-get upgrade  
\-- this upgraded a bunch of stuff...took about 45 minutes  
  
sudo apt-get dist-upgrade -o APT::Immediate-Configure=0 APT::Force-LoopBreak=1  

\-- the main upgrade...I received errors when I just ran "sudo apt-get dist-upgrade": "E: Could not perform immediate configuration on 'package'.  Please see man 5 apt.conf under APT::Immediate-Configure for details." I also got an conflict/pre-depend error for xml-core and docbook-xml...ugh. So, I started uninstalling things:

sudo apt-get autoremove

sudo apt-get remove default-jre

  

sudo apt-get remove xml-core

sudo apt-get remove gnome

sudo apt-get remove kde

sudo apt-get remove libreoffice

sudo apt-get remove openoffice.org

sudo apt-get remove gcc

sudo apt-get remove openjdk-6-jre

  

finally: 

sudo apt-get dist-upgrade

  

This ran overnight.

  

2013-04-21

  

In the morning, I awoke to a screen warning about the 686 kernel. After the dist-upgrade completed, I installed the 486 kernel, as suggested:

  

sudo apt-get install linux-image-486

sudo apt-get remove linux-image-686

sudo apt-get remove linux-image-2.6-686

sudo apt-get install gnome

sudo apt-get install default-jre

sudo apt-get install xml-core

sudo apt-get install kde

sudo apt-get install libreoffice

sudo apt-get install openoffice.org

sudo apt-get install gcc

sudo apt-get install openjdk-7-jre

  

sudo apt-get autoremove

\-- a sanity check

sudo apt-get check

sudo apt-get update

sudo apt-get upgrade

sudo apt-get dist-upgrade

sudo apt-get install google-chrome-unstable

sudo dpkg --audit

  

sudo apt-get remove adobereader-enu

sudo apt-get remove dhcp3-client dhcp3-common 

sudo apt-get remove gcj-jre-headless

sudo apt-get install gcj-jre-headless

sudo apt-get remove bogofilter doc-debian

sudo apt-get install bogofilter doc-debian

  

Done. : o )

  

At this point I attempted to fix my sudoers file, as per instructions. I moved /etc/sudoers to /etc/sudoers.d/mychanges ... this was a mistake, because as soon as I did, I lost the ability to sudo things. x\_x After a few reboots into recovery mode I successfully copied back /etc/sudoers.d/mychanges to /etc/sudoers and removed /etc/sudoers.d/mychanges.

  

Next, I ran the following to remove the unneeded grub menu entries:

  

sudo aptitude search linux-image

sudo aptitude remove linux-image-2.6.32-5-686 linux-image-3.2.0-4-686-pae linux-image-686-pae

  

I installed bootlogd to record the Radeon error messages I receive during boot:

  

sudo apt-get install bootlogd

sudo apt-get install firmware-linux-nonfree

  

This solved getting Gnome3 to load with all the bells and whistles.  
  
However, this ended up being too slow, given my hardware. So I uninstalled it, per [instructions](http://wiki.debian.org/Xfce):  

*   sudo aptitude purge \`dpkg --get-selections | grep gnome | cut -f 1\`
*   sudo aptitude -f install
*   sudo aptitude purge \`dpkg --get-selections | grep deinstall | cut -f 1\`
*   sudo aptitude -f install

Unfortunately, this sequence of commands led to two undesirable side-effects:  

1.  Network no longer worked

*   sudo vim /etc/network/interfaces
*   sudo dhclient eth0
*   ifconfig eth1 up
*   sudo iwconfig eth1 up
*   sudo iwconfig eth1 essid {ESSID}
*   sudo dhclient eth1

3.  GDM - gone...booted into tty prompt

*   Added to ~/.xinitrc: exec ck-launch-session startxfce4
*   sudo apt-get install gdm3

At this point, everything looks like it´s pretty stable...moving on to configuration.  
  
Other things installed:  
  

*   wicd
*   p7zip-full
*   p7zip
*   mtools
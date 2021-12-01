---
title: 'My Touchpad Won''t Vertical Scroll: Interactions of GNOME 3.20, libinput, Debian Stretch (Testing), and Synaptics functionality'
date: 2016-05-29T23:03:00.005-07:00
draft: false
tags: 
- libinput
- testing
- synaptics
- stretch
- linux
- touchpad
- debian
---

Within the last two weeks, I noticed something unexpected: My Lenovo Thinkpad x201, which has a SynPS/2 Synaptics TouchPad, still moved the mouse cursor, but no scrolling occurred when using the right vertical scroll area.  

> Note: I want to acknowledge and recognize everyone who contributes their time and energy to developing and maintaining these projects--this post represents a way for me to document my troubleshooting and expand my own awareness of the various project details. Thank you.

TL;DR:  
  

*   GNOME 3.20 prioritizes driver libinput, deprecating the unsupported Synaptics touchpad driver
*   Driver libinput breaks my use case, for touchpad vertical edge scrolling (note: as of xserver-xorg-input-libinput 0.19.0-1) 
*   As a workaround, two finger scrolling works, for now
*   The end.

  
  
TIMELINE OF EVENTS  
  
March 23, 2016: [The GNOME Project](https://en.wikipedia.org/wiki/The_GNOME_Project) staff \[note: upstream, from Debian\] released GNOME 3.20. In this version, GNOME developers committed changes to simplify Wayland compositor mouse input device handling. Specifically, they removed "...support for detecting and configuring input devices driven by the Synaptics X driver...because the \[S\]ynaptics X driver isn't developed anymore." The GNOME changeset comment reads, "mouse: Remove support for non-libinput mouse configurations.... As we want to move input device handling into the compositor, so there's only one code path for all their configuration, remove support for evdev/synaptics settings."  
[https://bugzilla.gnome.org/show\_bug.cgi?id=764257#c12](https://bugzilla.gnome.org/show_bug.cgi?id=764257#c12)  
[https://git.gnome.org/browse/gnome-settings-daemon/commit/?id=66c211ff24bec6a938d6a6a0dd8730f4689ef383](https://git.gnome.org/browse/gnome-settings-daemon/commit/?id=66c211ff24bec6a938d6a6a0dd8730f4689ef383)  
  
April 17, 2016: Debian GNOME maintainers released GNOME 3.20, to Debian sid (Unstable).  
[https://lists.alioth.debian.org/pipermail/pkg-gnome-maintainers/2016-April/126108.html](https://lists.alioth.debian.org/pipermail/pkg-gnome-maintainers/2016-April/126108.html)  
  
April 19, 2016: Noticing the GNOME 3.20+ libinput driver dependency, for mouse input configurations, a Debian GNOME maintainer created bug #821760, suggesting Debian X maintainers modify metapackage xserver-xorg-input-all, to force install libinput driver package xserver-xorg-input-libinput.  
https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=821760#15  

  
April 23, 2016: Debian X maintainers released package xorg-server 1:7.7+15, to Debian sid (Unstable), with changeset comment, "Make x-x-input-all depend on x-x-input-libinput. Closes: #821760". This change triggered the installation of then-current libinput driver package xserver-xorg-input-libinput 0.18.0-1,which maintainers had previously released, on April 7, 2016.  
[https://lists.debian.org/debian-x/2016/04/msg00221.html](https://lists.debian.org/debian-x/2016/04/msg00221.html)  

> Note: libinput driver package xserver-xorg-input-libinput 0.18.0-1 installed configuration file /usr/share/X11/xorg.conf.d/90-libinput.conf. Restarting X server subsequently prioritized use of the libinput driver package (note: priority 90), over then-current Synaptics driver package xserver-xorg-input-synaptics:amd64 1.8.3-1+b1, which installed configuration file /usr/share/X11/xorg.conf.d/50-synaptics.conf (note: priority 50).

April 23, 2016: After five days, per Debian automated processes, Debian Stretch (Testing) automatically received the updated GNOME 3.20 package gnome-desktop3 3.20.1-1. As mentioned earlier, GNOME 3.20 required libinput driver package xserver-xorg-input-libinput, to perform certain mouse configurations. \[Note: I upgraded to GNOME 3.20 two days later, on April 25, 2016.\]  
[https://lists.alioth.debian.org/pipermail/pkg-gnome-maintainers/2016-April/126431.html](https://lists.alioth.debian.org/pipermail/pkg-gnome-maintainers/2016-April/126431.html)  

> Note: This seems to imply a five day delay, between release of GNOME 3.20 and libinput driver package xserver-xorg-input-libinput 0.18.0-1

April 24, 2016: Users of Debian Sid (Unstable) began reporting issues related to Synaptic input devices, after upgrading to xorg-server 1:7.7+15, which prioritized using libinput driver package xserver-xorg-input-libinput 0.18.0-1:  
[https://lists.debian.org/debian-x/2016/04/msg00246.html](https://lists.debian.org/debian-x/2016/04/msg00246.html)  
  
April 28, 2016: After five days, per Debian automated processes, Debian Stretch (Testing) automatically received the updated package xorg-server 1:7.7+15, which installed libinput driver package xserver-xorg-input-libinput 0.18.0-1.  

> Note: While I installed the libinput driver package xserver-xorg-input-libinput 0.18.0-1, on April 28, 2016, I don't remember immediately noticing Synaptic touchpad vertical scrolling issues, possibly because I didn't restart my X server, until May 15, 2016

May 10, 2016: As a libinput maintenance release, this seems to address similar issues, for Wacom input devices. As the first of two steps, Debian maintainers updated libinput driver package xserver-xorg-input-libinput, in Debian sid (Unstable), from version 0.18.0.1, to version 0.19.0-1. As a workaround, for Wacom devices, this update renamed and deprioritized the libinput driver configuration file, from /usr/share/X11/xorg.conf.d/90-libinput.conf, to /usr/share/X11/xorg.conf.d/60-libinput.conf. Note: as of this writing, Debian X maintainers have yet to perform the second step (possibly due to waiting on upstream maintenance): renaming and prioritizing the configuration file, for Wacom driver packge xserver-xorg-input-wacom, from /usr/share/X11/xorg.conf.d/50-wacom.conf, to /usr/share/X11/xorg.conf.d/70-wacom.conf.  
[https://lists.debian.org/debian-x/2016/05/msg00073.html](https://lists.debian.org/debian-x/2016/05/msg00073.html)  
[https://lists.debian.org/debian-x/2016/05/msg00075.html](https://lists.debian.org/debian-x/2016/05/msg00075.html)  
[https://lists.debian.org/debian-x/2016/05/msg00189.html](https://lists.debian.org/debian-x/2016/05/msg00189.html)  
  
May 15, 2016: Updated libinput driver package xserver-xorg-input-libinput 0.19.0-1 reached Debian Stretch (Testing), and I installed it.  

> Note: Due to reboot, per separate issue, this most likely represents the point where I began noticing the lack of touchpad vertical scrolling.

> k@bucket:/var/log$ last -50 reboot shutdown -f /var/log/wtmp.1  
> reboot system boot 4.4.0-1-amd64 Sun Apr 10 17:22 still running  
> reboot system boot 4.4.0-1-amd64 Sat Apr 9 14:59 - 17:20 (1+02:21)  
> reboot system boot 4.4.0-1-amd64 Sat Apr 9 14:06 - 14:20 (00:14)  
> reboot system boot 4.4.0-1-amd64 Sat Apr 2 10:00 - 14:06 (7+04:06)  
> wtmp.1 begins Sat Apr 2 10:00:08 2016 

> k@bucket:/var/log$ last -50 reboot shutdown -f /var/log/wtmp  
> reboot system boot 4.5.0-2-amd64 Sun May 29 19:29 still running  
> reboot system boot 4.5.0-2-amd64 Sat May 28 20:11 still running  
> reboot system boot 4.5.0-2-amd64 Sun May 15 21:32 still running  
> reboot system boot 4.5.0-2-amd64 Sun May 15 20:53 still running  
> reboot system boot 4.5.0-2-amd64 Sun May 15 17:24 still running  
> reboot system boot 4.5.0-2-amd64 Sun May 15 12:51 - 16:09 (03:18)  
> reboot system boot 4.5.0-2-amd64 Sun May 15 12:44 - 12:50 (00:06)  
> wtmp begins Sat May 7 15:16:51 2016

May 21, 2016: Debian X maintainers release libinput package libinput10 1.3.0-2, a maintenance release, closing bug 822872.  
[https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=822872](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=822872)  
  
May 26, 2016: Debian X maintainers updated Synaptics driver package xserver-xorg-input-synaptics, from 1.8.3-1+b1, to 1.8.3-2, with changeset comment "renames 50-synaptics.conf to 70-synaptics.conf. This means the synaptic driver will be used instead of the libinput driver when both are installed."  
[https://lists.debian.org/debian-x/2016/05/msg00193.html](https://lists.debian.org/debian-x/2016/05/msg00193.html)  

> Note: This means, after five days--on Tuesday, May 31, or Wednesday, June 1, Debian Stretch (Testing) should receive Synaptics driver package xserver-xorg-input-synaptics 1.8.3-2, which, after restarting X, should prioritize using synaptic driver and allow scrolling again.

  
  
BACKGROUND  
Via: [https://www.freedesktop.org/wiki/Software/libinput/](https://www.freedesktop.org/wiki/Software/libinput/)  

> **libinput** is a library to handle input devices in [Wayland](http://wayland.freedesktop.org/) compositors and to provide a generic [X.Org](http://x.org/) input driver. It provides device detection, device handling, input device event processing and abstraction so minimize the amount of custom input code compositors need to provide the common set of functionality that users expect.

MY INSTALLATION HISTORY  
  
My Debian Stretch (Testing) package xserver-xorg-input-synaptics installation history:  

> k@bucket:/usr/share/X11/xorg.conf.d$ zgrep " installed"  /var/log/dpkg.log\* | grep "xserver-xorg-input-synaptics" | cut -d':' -f2- | sort -r 

> 2016-02-04 20:35:08 status installed xserver-xorg-input-synaptics:amd64 1.8.3-1+b1  
> 2015-11-16 19:10:50 status installed xserver-xorg-input-synaptics:amd64 1.8.2-1  
> k@bucket:/usr/share/X11/xorg.conf.d$ 

My Debian Stretch (Testing) package xserver-xorg-input-libinput installation history:

> k@bucket:/usr/share/X11/xorg.conf.d$ zgrep " installed"  /var/log/dpkg.log\* | grep "xserver-xorg-input-libinput" | cut -d':' -f2- | sort -r 

> 2016-05-15 22:51:06 status installed xserver-xorg-input-libinput:amd64 0.19.0-1  
> 2016-04-28 21:47:32 status installed xserver-xorg-input-libinput:amd64 0.18.0-1  
> k@bucket:/usr/share/X11/xorg.conf.d$ 

My Debian Stretch (Testing) package libinput10 installation history:

> k@bucket:/usr/share/X11/xorg.conf.d$ zgrep " installed"  /var/log/dpkg.log\* | grep "libinput10" | cut -d':' -f2- | sort -r 

> 2016-05-21 16:50:39 status installed libinput10:amd64 1.3.0-2  
> 2016-05-15 22:51:06 status installed libinput10:amd64 1.3.0-1  
> 2016-04-25 19:14:22 status installed libinput10:amd64 1.2.4-1  
> 2016-04-18 21:09:35 status installed libinput10:amd64 1.2.3-1  
> 2016-03-23 17:58:54 status installed libinput10:amd64 1.2.2-1  
> 2016-03-01 18:09:44 status installed libinput10:amd64 1.2.0-1  
> 2016-02-17 05:52:09 status installed libinput10:amd64 1.1.7-1  
> 2016-01-20 17:41:42 status installed libinput10:amd64 1.1.4-1  
> 2015-12-23 04:55:43 status installed libinput10:amd64 1.1.3-1  
> 2015-12-17 05:26:07 status installed libinput10:amd64 1.1.2-1  
> 2015-11-16 19:09:50 status installed libinput10:amd64 1.1.0-1  
> k@bucket:/usr/share/X11/xorg.conf.d$ 

My Debian Stretch (Testing) package xserver-xorg installation history:

> k@bucket:/usr/share/X11/xorg.conf.d$ zgrep " installed"  /var/log/dpkg.log\* | grep "xserver-xorg:" | cut -d':' -f2- | sort -r 

> 2016-04-28 21:47:32 status installed xserver-xorg:amd64 1:7.7+15  
> 2016-03-14 08:48:08 status installed xserver-xorg:amd64 1:7.7+14  
> 2016-02-01 18:42:59 status installed xserver-xorg:amd64 1:7.7+13  
> 2015-11-16 19:10:50 status installed xserver-xorg:amd64 1:7.7+12  
> k@bucket:/usr/share/X11/xorg.conf.d$ 

My Debian Stretch (Testing) package xserver-xorg-input-all installation history:

> k@bucket:/usr/share/X11/xorg.conf.d$ zgrep " installed"  /var/log/dpkg.log\* | grep "xserver-xorg-input-all" | cut -d':' -f2- | sort -r 

> 2016-04-28 21:47:32 status installed xserver-xorg-input-all:amd64 1:7.7+15  
> 2016-03-14 08:48:08 status installed xserver-xorg-input-all:amd64 1:7.7+14  
> 2016-02-01 18:42:59 status installed xserver-xorg-input-all:amd64 1:7.7+13  
> 2015-11-16 19:10:50 status installed xserver-xorg-input-all:amd64 1:7.7+12  
> k@bucket:/usr/share/X11/xorg.conf.d$ 

  

  

My Debian Stretch (Testing) package gnome-desktop3-data installation history (note: this package provides file /usr/share/gnome/gnome-version.xml, which seems to represent the authoritative version file [referenced by GNOME developers](http://unix.stackexchange.com/a/73225/11726))

> k@bucket:~/Documents/schultkl@gmail.com$ zgrep " installed"  /var/log/dpkg.log\* | grep "gnome-desktop3-data" | cut -d':' -f2- | sort -r  
> 2016-05-17 05:58:57 status installed gnome-desktop3-data:all 3.20.2-1  
> 2016-04-25 19:14:21 status installed gnome-desktop3-data:all 3.20.1-1  
> 2015-11-16 19:09:55 status installed gnome-desktop3-data:all 3.18.2-1

**UPDATE, 2016-06-01**  
Right on schedule  

> The following packages will be upgraded:  
>   cpp g++ gcc google-chrome-stable libtheora0 python-requests python-urllib3  
>   python3-requests python3-urllib3 vorbis-tools xserver-xorg-input-synaptics  
> 11 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.  
> Need to get 50.0 MB of archives.  
> After this operation, 71.7 kB of additional disk space will be used.  
> Do you want to continue? \[Y/n\] 

> Get:11 http://ftp.us.debian.org/debian stretch/main amd64 xserver-xorg-input-synaptics amd64 1.8.3-2 \[216 kB\]  
> Fetched 50.0 MB in 24s (2,064 kB/s)                                            
> Reading changelogs... Done  
> (Reading database ... 178566 files and directories currently installed.)  
> Preparing to unpack .../xserver-xorg-input-synaptics\_1.8.3-2\_amd64.deb ...  
> Unpacking xserver-xorg-input-synaptics (1.8.3-2) over (1.8.3-1+b1) ...  
> Setting up xserver-xorg-input-synaptics (1.8.3-2) ...

I now have these versions installed:

> k@bucket:~/Music$ zgrep " installed"  /var/log/dpkg.log\* | grep "xserver-xorg-input-synaptics" | cut -d':' -f2- | sort -r  
> 2016-06-01 17:26:00 status installed xserver-xorg-input-synaptics:amd64 1.8.3-2  
> 2016-02-04 20:35:08 status installed xserver-xorg-input-synaptics:amd64 1.8.3-1+b1  
> 2015-11-16 19:10:50 status installed xserver-xorg-input-synaptics:amd64 1.8.2-1

And /usr/share/X11/xorg.conf.d/ looks like this:

> k@bucket:~/Music$ ls /usr/share/X11/xorg.conf.d/  
> 10-amdgpu.conf  10-quirks.conf   50-wacom.conf     70-synaptics.conf  
> 10-evdev.conf   50-vmmouse.conf  60-libinput.conf

Unfortunately, when I restarted my X server, I still do not get the Synaptics vertical scroll functionality back.

  
So--goodbye Synaptics, for good. I uninstalled it, leaving libinput as the driver:  

> k@bucket:~$ ls /usr/share/X11/xorg.conf.d/  
> 10-amdgpu.conf  10-quirks.conf   50-wacom.conf  
> 10-evdev.conf   50-vmmouse.conf  60-libinput.conf

And doh. Just discovered I have to use two fingers side-by-side, to scroll. Sigh. That's it.

  

  

RESOURCES

  
Debian Package xserver-xorg-input-libinput, and so forth  
[https://www.freedesktop.org/wiki/Software/libinput/](https://www.freedesktop.org/wiki/Software/libinput/)  
[https://wayland.freedesktop.org/libinput/doc/latest/index.html](https://wayland.freedesktop.org/libinput/doc/latest/index.html)  
[https://wiki.archlinux.org/index.php/Libinput](https://wiki.archlinux.org/index.php/Libinput)  
[http://forum.siduction.org/index.php?topic=6180.msg50908#msg50908](http://forum.siduction.org/index.php?topic=6180.msg50908#msg50908)  
[https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=821760](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=821760)  
[http://metadata.ftp-master.debian.org/changelogs//main/x/xserver-xorg-input-libinput/](http://metadata.ftp-master.debian.org/changelogs//main/x/xserver-xorg-input-libinput/)  
[https://packages.debian.org/stretch/xserver-xorg-input-libinput](https://packages.debian.org/stretch/xserver-xorg-input-libinput)  
[https://sources.debian.net/src/xserver-xorg-input-libinput/0.19.0-1/ChangeLog/](https://sources.debian.net/src/xserver-xorg-input-libinput/0.19.0-1/ChangeLog/)  
[http://snapshot.debian.org/package/xserver-xorg-input-libinput/](http://snapshot.debian.org/package/xserver-xorg-input-libinput/)  
  
Debian Package xserver-xorg-input-synaptics, and so forth  
[https://wiki.debian.org/SynapticsTouchpad#Change\_to\_libinput\_Xorg\_driver\_in\_Debian\_9\_.22Stretch.22](https://wiki.debian.org/SynapticsTouchpad#Change_to_libinput_Xorg_driver_in_Debian_9_.22Stretch.22)  
[https://packages.debian.org/xserver-xorg-input-synaptics](https://packages.debian.org/xserver-xorg-input-synaptics)  
[https://packages.debian.org/xserver-xorg-input-libinput](https://packages.debian.org/xserver-xorg-input-libinput)  
[https://en.wikipedia.org/wiki/Synaptics](https://en.wikipedia.org/wiki/Synaptics)  
[http://metadata.ftp-master.debian.org/changelogs//main/x/xserver-xorg-input-synaptics/](http://metadata.ftp-master.debian.org/changelogs//main/x/xserver-xorg-input-synaptics/)  
[http://snapshot.debian.org/package/xserver-xorg-input-synaptics/](http://snapshot.debian.org/package/xserver-xorg-input-synaptics/)  
  
Debian Package xserver-xorg  
[https://packages.debian.org/sid/xserver-xorg](https://packages.debian.org/sid/xserver-xorg)  
[http://metadata.ftp-master.debian.org/changelogs//main/x/xorg/?C=M;O=D](http://metadata.ftp-master.debian.org/changelogs//main/x/xorg/?C=M;O=D)  
[https://lists.debian.org/debian-x/2016/04/msg00225.html](https://lists.debian.org/debian-x/2016/04/msg00225.html)  
  
Debian Stretch (Testing)  
[https://lists.debian.org/debian-testing/](https://lists.debian.org/debian-testing/)  
[https://wiki.debian.org/DebianTesting](https://wiki.debian.org/DebianTesting)  
[https://www.debian.org/devel/testing](https://www.debian.org/devel/testing)  
  
GNOME  
[https://git.gnome.org/browse/gnome-settings-daemon/commit/?id=66c211ff24bec6a938d6a6a0dd8730f4689ef383](https://git.gnome.org/browse/gnome-settings-daemon/commit/?id=66c211ff24bec6a938d6a6a0dd8730f4689ef383)  
[https://lists.alioth.debian.org/pipermail/pkg-gnome-maintainers/](https://lists.alioth.debian.org/pipermail/pkg-gnome-maintainers/)  
[https://lists.debian.org/debian-gtk-gnome/](https://lists.debian.org/debian-gtk-gnome/) \[Note: unused (?)\]
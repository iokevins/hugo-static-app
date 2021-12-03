---
title: 'GNOME-Software, PackageKit: Button "Restart & Install", Offline OS Updates'
date: 2015-11-24T11:16:00.002-08:00
draft: false
tags: 
- gnome-software
- update
- package
- gnome
- debian
- packagekit
---

[![](/images/Screenshot%2Bfrom%2B2015-11-24%2B11-07-17.png)](/images/Screenshot%2Bfrom%2B2015-11-24%2B11-07-17.png)

_Screenshot of GNOME-Software tab "Update", showing option "OS Updates" and button "Restart & Install", at upper-right_

  
Noticed gnome-software, after upgrading to Debian Stretch (Testing), showing button "Restart & Install".  

#### OVERVIEW

[PackageKit](https://en.wikipedia.org/wiki/PackageKit) represents a common frontend, for a number of different backend package management systems. For example, apt, yum, and ZYpp. PackageKit runs, in the background, as operating system process packagekitd. To my knowledge, it is \*not\* part of GNOME.  
  
[GNOME-Software](https://en.wikipedia.org/wiki/GNOME_Software) represents one, of several\*, frontend user interfaces, to PackageKit. It runs as user process gnome-software. \*Note: KDE, for example, uses alternative frontend user interface [Apper](https://en.wikipedia.org/wiki/Apper).  

#### HISTORY OF PACKAGEKIT, GNOME-SOFTWARE

Richard Hughes created PackageKit, in 2007. Fedora 9 seems to represent the first distribution to include it, in May, 2008.  
  
PackageKit began supporting feature "Offline OS Updates", in July 2012, with version 0.8.1. Fedora 18 seems to represent the first distribution to include this PackageKit functionality.  
  
Richard Hughes created package GNOME-Software in September 2013, as initial version number 3.9.1. Fedora 20 seems to represent the first distribution to include GNOME-Software, as part of GNOME 3.10.  
  
Other distributions, such as Debian, have now adopted PackageKit and GNOME-Software, with different timelines (see below).  

#### CONTROVERSY

The PackageKit changes seem to have sparked a lot of discussion, on the [Fedora devel list](https://lists.fedoraproject.org/pipermail/devel/2013-November/191197.html), and elsewhere.  
  
"Offline OS Updates" represents a complicated topic, with ties to historical \*NIX pride over uptimes and comparisons to Microsoft Windows. I don't claim expert knowledge in the theory or practice, so, per [Bertrand Russell](https://philebersole.wordpress.com/2010/12/19/bertrand-russells-rules-for-skeptics/), I am refraining from comment.  

#### DEBIAN TIMELINE: PACKAGEKIT, GNOME-SOFTWARE

Debian released Etch, in April 2007, Lenny, in February 2009, and Squeeze, in February 2011. None of these releases seem to have contained PackageKit or gnome-software. This seems reasonable, given the development and release cycles.  
  
Debian Wheezy (OldStable), initially released in May, 2013, currently supports the following package versions:  

1.  GNOME 3.4
2.  PackageKit 0.7.6-3 (that is, no support for feature "Offline OS Updates")
3.  gnome-software: not in this release

Debian Jessie (Stable), initially released in April, 2015, currently supports the following package versions:  
  

1.  GNOME 3.14
2.  PackageKit 1.0.1-2 (that is, support for feature "Offline OS Updates")
3.  gnome-software: not in this release

  
Debian Stretch (Testing), as of this writing, supports the following package versions:  
  

1.  GNOME 3.18.2 (via Activities > Details)
2.  PackageKit 1.0.10-1 (that is, support for feature "Offline OS Updates")
3.  gnome-software 3.18.3-1

  
The above lists help explain why I did not notice this functionality until I upgraded, from Debian Jessie (Stable), to Debian Stretch (Testing).  

#### WORKAROUNDS

In most cases, to avoid restarting, I use apt (Advanced Package Tool), so I use that and ignore suggestions from gnome-software.  
  
GNOME-Software makes a guess as to whether to suggest a restart. Specifically, "\[i\]f the package has a .desktop file (which are normally used to populate the \[desktop environment's\] menus) it is considered an user application and can be updated without a reboot. Without this file, it is considered a OS or System update and a 'Update and Restart' is offered." ([via](http://unix.stackexchange.com/a/152361)).  

#### RESOURCES

PackageKit  

*   [PackageKit](https://en.wikipedia.org/wiki/PackageKit) (note: frontend, to various backend package managers; for example, apt, yum)
*   [Offline OS Updates – Looking forward to GNOME 3.6](https://blogs.gnome.org/hughsie/2012/06/04/offline-os-updates-looking-forward-to-gnome-3-6/) (note: this seems to indicate the rough time of introduction, via PackageKit; namely, June 4, 2012, with GNOME 3.6)
*   [Richard Hughes](http://www.hughsie.com/) (note: gnome-software maintainer; Red Hat employee, in the desktop group)

GNOME-Software  

*   [GNOME-Software](https://en.wikipedia.org/wiki/GNOME_Software) (note: frontend, to PackageKit)
*   GitHub gnome-software release tags

Debian-specific resources  

*   [](https://wiki.debian.org/Gnome)[GNOME in Debian](https://wiki.debian.org/Gnome) (note: shows specific versions shipped with major releases)
*   [Debian Package Search](https://www.debian.org/distrib/packages#search_packages)
*   [PackageKit Debian metadata](http://metadata.ftp-master.debian.org/changelogs/main/p/packagekit/)
*   Debian developer [Matthias Klumpp](https://portfolio.debian.net/result?username=mak&nonddemail=matthias%40tenstral.net&aliothusername=&gpgfp=D33A3F0CA16B0ACC51A60738494C8A5FBF4DECEB&forumsid=&wikihomepage=&email=matthias%40tenstral.net&name=Matthias+Klumpp) released the following statements, on his blog, regarding Debian support for package GNOME-Software:

*   [The state of AppStream/GNOME-Software in Debian Jessie](http://blog.tenstral.net/2014/11/the-state-of-appstreamgnome-software-in-debian-jessie.html) (note: explains why GNOME-Software did not get released with Debian Jessie; circa November, 2014) 
*   [Update notifications in Debian Jessie](http://blog.tenstral.net/2015/09/update-notifications-in-debian-jessie.html) (note: from September, 2015)
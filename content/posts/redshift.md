---
title: 'Redshift'
date: 2015-11-03T05:11:00.001-08:00
draft: false
tags: 
- linux
- gnome
- redshift
- debian
- f.lux
- display
---

I like [f.lux](https://justgetflux.com/) when in a Microsoft Windows environment, and [redshift](http://jonls.dk/redshift/) represents an equivalent, on Debian Jessie (stable). I also installed redshift-gtk, which runs under GNOME, in the system tray.  
  
NOTES  
  

*   F.lux seems to maintain packages, for Ubuntu, but does not seem to have Debian repositories
*   Required me to create a configuration file, in ~/.config/redshift.conf...after creation, it runs fine

*   I started from the version published on the redshift web site
*   I manually configured my latitude and longitude (note: as mentioned in the configuration file comments, the Americas have a negative longitude)
*   I also manually modifited the lines "screen=1", as I received the following errors, otherwise:

*   user@host:~/.config$ redshift

*   Screen 1 could not be found.
*   Failed to start adjustment method randr

*   Fix: change line to "screen=0"
*   Runs fine, after
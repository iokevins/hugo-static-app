---
title: 'gnome-screensaver'
date: 2013-04-21T21:49:00.000-07:00
draft: false
tags: 
- linux
- debian
---

Reading up on gnome-screensaver this evening, as I upgrade from Debian Squeeze to Wheezy:  
[http://en.wikipedia.org/wiki/Gnome-screensaver](http://en.wikipedia.org/wiki/Gnome-screensaver)  
  
Tag 2.91.91 removed the cosmos images on 2011-03-08:  
[https://git.gnome.org/browse/gnome-screensaver/commit/?id=2.91.91](https://git.gnome.org/browse/gnome-screensaver/commit/?id=2.91.91)  
  
The commit to remove the Cosmos screensaver images, from 2011-03-06:  
[https://git.gnome.org/browse/gnome-screensaver/commit/?id=897dc79ba04b3cfb49b93f6bd03fa2ce59a274b7](https://git.gnome.org/browse/gnome-screensaver/commit/?id=897dc79ba04b3cfb49b93f6bd03fa2ce59a274b7)  
  
Squeeze: gnome-screensaver 2.30.0-2squeeze1  
[http://packages.debian.org/squeeze/i386/gnome-screensaver/filelist](http://packages.debian.org/squeeze/i386/gnome-screensaver/filelist)  
  
Wheezy: gnome-screensaver 3.4.1-1  
[http://packages.debian.org/wheezy/i386/gnome-screensaver/filelist](http://packages.debian.org/wheezy/i386/gnome-screensaver/filelist)  
  
I had **an** **"ah ha" moment** while reading the [description](https://live.gnome.org/GnomeScreensaver/FrequentlyAskedQuestions#Why_doesn.27t_the_screensaver_preferences_tool_allow_me_to_change_the_settings_for_the_theme.3F) of why the gnome-screensavers chose the route they did to remove the Cosmos screensaver. At first, I think I reacted as many did--with surprise and indignation. However, their argument seems reasonable and they seem very open to explaining their actions.  
  
I must say, however--playing with all the xscreensaver options brought some nostalgic joy to my heart this evening. : o ) I'm going to go ahead and [salvage](https://git.gnome.org/browse/gnome-screensaver/tree/data/images/cosmos?id=2.91.90) the old Cosmos screen saver images for xscreensaver, instead:  
  

1.  [https://git.gnome.org/browse/gnome-screensaver/plain/data/images/cosmos/blue-marble-west.jpg?id=2.91.90](https://git.gnome.org/browse/gnome-screensaver/plain/data/images/cosmos/blue-marble-west.jpg?id=2.91.90)
2.  [https://git.gnome.org/browse/gnome-screensaver/plain/data/images/cosmos/cloud.jpg?id=2.91.90](https://git.gnome.org/browse/gnome-screensaver/plain/data/images/cosmos/cloud.jpg?id=2.91.90)
3.  [https://git.gnome.org/browse/gnome-screensaver/plain/data/images/cosmos/comet.jpg?id=2.91.90](https://git.gnome.org/browse/gnome-screensaver/plain/data/images/cosmos/comet.jpg?id=2.91.90)
4.  [https://git.gnome.org/browse/gnome-screensaver/plain/data/images/cosmos/earth-horizon.jpg?id=2.91.90](https://git.gnome.org/browse/gnome-screensaver/plain/data/images/cosmos/earth-horizon.jpg?id=2.91.90)
5.  [https://git.gnome.org/browse/gnome-screensaver/plain/data/images/cosmos/galaxy-ngc3370.jpg?id=2.91.90](https://git.gnome.org/browse/gnome-screensaver/plain/data/images/cosmos/galaxy-ngc3370.jpg?id=2.91.90)
6.  [https://git.gnome.org/browse/gnome-screensaver/plain/data/images/cosmos/helix-nebula.jpg?id=2.91.90](https://git.gnome.org/browse/gnome-screensaver/plain/data/images/cosmos/helix-nebula.jpg?id=2.91.90)
7.  [https://git.gnome.org/browse/gnome-screensaver/plain/data/images/cosmos/jupiter.jpg?id=2.91.90](https://git.gnome.org/browse/gnome-screensaver/plain/data/images/cosmos/jupiter.jpg?id=2.91.90)
8.  [https://git.gnome.org/browse/gnome-screensaver/plain/data/images/cosmos/sombrero.jpg?id=2.91.90](https://git.gnome.org/browse/gnome-screensaver/plain/data/images/cosmos/sombrero.jpg?id=2.91.90)
9.  [https://git.gnome.org/browse/gnome-screensaver/plain/data/images/cosmos/whirlpool.jpg?id=2.91.90](https://git.gnome.org/browse/gnome-screensaver/plain/data/images/cosmos/whirlpool.jpg?id=2.91.90)
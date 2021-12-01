---
title: 'Day one - Configuring Debian GNU/Linux 7 "wheezy"'
date: 2013-04-21T23:25:00.000-07:00
draft: false
tags: 
- linux
- debian
---

2013-04-21  
  
_Reviewing previous customizations_  
I´m going through many of the previous customizations from the previous stable release:  

*   [Day two - Configuring Debian GNU/Linux 6.0.5 "squeeze"](http://schultkl.blogspot.com/2012/09/day-two-configuring-debian-gnulinux-605.html)
*   [Day three - Configuring Debian GNU/Linux 6.0.5 "squeeze"](http://schultkl.blogspot.com/2012/09/day-three-configuring-debian-gnulinux.html)
*   [Day five - Configuring Debian GNU/Linux 6.0.5 "squeeze"](http://schultkl.blogspot.com/2012/09/day-five-configuring-debian-gnulinux.html)
*   [Errata - Configuring Debian GNU/Linux 6.0.5 "squeeze"](http://schultkl.blogspot.com/2012/09/errata-configuring-debian-gnulinux-605.html)

_Cosmos screensaver_  
Looks like XFCE ships without the cosmos screensaver...  
  

*   Unfortunately, gnome-screensaver, which has the cosmos screensaver, requires gnome-session
*   Just for fun, I installed all the xscreensaver options: 

*   sudo apt-get install xscreensaver-data xscreensaver-data-extra xscreensaver-gl xscreensaver-gl-extra rss-glx

*   To configure xscreensaver to display a [slideshow](http://www.jwz.org/xscreensaver/faq.html#slideshow) of images:

*   Applications Menu > Settings > Screensaver
*   Mode = Only One Screen Saver
*   Screen Saver = GLSlideshow
*   Blank After = 30 minutes
*   Cycle After = 3 minutes
*   Select button ¨Settings¨

*   Select button "Advanced"
*   Command Line =  
    glslideshow -root -delay 84615 -duration 17 -zoom 100 -pan 17 -fade 3 -fps
*   Letterbox = Checked, everything else unchecked
*   Select button ¨OK¨ to return to the main window

*   Select tab ¨Advanced¨

*   Select checkbox ¨Choose Random Image¨ and set to  
    /usr/share/backgrounds/cosmos
*   Uncheck ¨Grab Desktop Images¨

*   It appears all my old cosmos images got [deleted](http://schultkl.blogspot.com/2013/04/gnome-screensaver.html) though...so I chose to get them back manually:

*   cd /usr/share/backgrounds/cosmos
*   sudo wget https://git.gnome.org/browse/gnome-screensaver/plain/data/images/cosmos/blue-marble-west.jpg?id=2.91.90 -O blue-marble-west.jpg
*   sudo wget https://git.gnome.org/browse/gnome-screensaver/plain/data/images/cosmos/cloud.jpg?id=2.91.90 -O cloud.jpg
*   sudo wget https://git.gnome.org/browse/gnome-screensaver/plain/data/images/cosmos/comet.jpg?id=2.91.90 -O comet.jpg
*   sudo wget https://git.gnome.org/browse/gnome-screensaver/plain/data/images/cosmos/earth-horizon.jpg?id=2.91.90 -O earth-horizon.jpg
*   sudo wget https://git.gnome.org/browse/gnome-screensaver/plain/data/images/cosmos/galaxy-ngc3370.jpg?id=2.91.90 -O galaxy-ngc3370.jpg
*   sudo wget https://git.gnome.org/browse/gnome-screensaver/plain/data/images/cosmos/helix-nebula.jpg?id=2.91.90 -O helix-nebula.jpg
*   sudo wget https://git.gnome.org/browse/gnome-screensaver/plain/data/images/cosmos/jupiter.jpg?id=2.91.90 -O jupiter.jpg
*   sudo wget https://git.gnome.org/browse/gnome-screensaver/plain/data/images/cosmos/sombrero.jpg?id=2.91.90 -O sombrero.jpg
*   sudo wget https://git.gnome.org/browse/gnome-screensaver/plain/data/images/cosmos/whirlpool.jpg?id=2.91.90 -O whirlpool.jpg

*   All that work, because, as I said before, ...Carl Sagan...Cosmos

_Printing_

It appears I lost all my UI printer configuration utilities, so, [via](http://xfce.10915.n7.nabble.com/Printer-configuration-tp15882p15883.html):

sudo apt-get install system-config-printer

  

This opens up Applications Menu > System > Printing

  

_Vim colors_

sudo cp /usr/share/vim/vim73/colors/koehler.vim /usr/share/vim/vim73/colors/koehler.vim.bak

  

_Configure vim  .vimrc_

  

_Configure XFCE4 Terminal 0.4.8 colors_

Via my 2008 [post](http://schultkl.blogspot.com/2008/01/putty-settings.html):

*   Font: Monospace Regular 10 pt.
*   Text Color="0,255,0"
*   Background Color="0,55,0"
*   Default Bold Background="85,85,85"
*   Lines of scrollback: 9999

To set the preferred geometry ([via](http://gnubyexample.blogspot.com/2010/06/opening-terminal-with-preset-size-fixed.html)):

*   vim ~/.config/Terminal/terminalrc
*   MiscDefaultGeometry=100x100+150+0

_Eclipse_

_Geany_

_Citrix Receiver _

_Filezilla_

_Amarok 2.5-GIT_

Loads OK

  

_Headphone jack sensing _

Not tested

  
_Java plugin_  
sudo apt-get install icedtea-plugin  
Restart browser  

_VLC_

Seems unable to play YouTube files

  

To-Do:

Ghostview

Install Adobe Reader 9.5.3

Volume control sound theme

Java
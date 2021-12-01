---
title: 'Debian Jessie Stable '
date: 2015-04-26T15:18:00.000-07:00
draft: false
tags: 
- linux
- debian
---

Upgrading to Debian Jessie stable soon. Have downloaded the ISOs for KDE and GNOME...need to decide which to go with.  
  
INSTALLATION LOG  
  
Backed up home directory  
Wiped disk during install (/home in separate partition)  
Had to use a separate USB to retrieve nonfree [wifi](https://packages.debian.org/jessie/all/firmware-iwlwifi/filelist) for my Lenovo ThinkPad x201:  

*   Package: firmware-iwlwifi
*   File: /lib/firmware/iwlwifi-6000-4.ucode

Put the USB in when prompted and the install proceeded without interruption.

  

Rebooted and all came up smoothly

  

CUSTOMIZATIONS

  

_Google Chrome_

Use Iceweasel to download 64-bit Google Chrome deb to Downloads folder

sudo dpkg -i ~/Downloads/google-chrome-stable\_current\_amd64.deb

This throws errors about missing packages libappindicator1 and libcurl3

sudo apt-get install libappindicator1 libcurl3

This throws errors

sudo apt-get -f install

This closes out the install and gets everything working

Add Google Chrome to Favorites

  

_Geany_

sudo apt-get install geany

sudo apt-get install geany-plugins

  

_GCC_

sudo apt-get install gcc

Note: already the latest version

  

_Filezilla_

sudo apt-get install filezilla

  

_Configure vim  .vimrc_

sudo apt-get install vim

From my 2009 [post](http://schultkl.blogspot.com/2009/03/vimrc.html), copied and pasted into ~k/.vimrc .

Historical note: the "rc" in ".vimrc" derives from "runcom", from the MIT CTSS system, ca. 1965.

  

_git_

sudo apt-get install git  
  
_subversion_  
sudo apt-get install subversion

  

_gimp extras_

[Via](http://zachariasblog.wordpress.com/2013/05/07/debian-wheezy-a-humble-post-install-guide/):

sudo apt-get install gimp-plugin-registry gimp-data-extras

  

_Enabling NTP Support_

sudo apt-get install ntp

Activities > Search for Date and Time

Automatic Date & Time: On

Automatic Time Zone: On

  

_Set default editor to vim_

vim ~k/.bashrc

Append line: export EDITOR="vim"

  

_Default applications_

[Via](http://verahill.blogspot.com/2013/03/367-some-post-install-steps-on-debian.html):

Activities, Search for Details

Default Applications

Web: Chromium Web Browser

Mali: Chromium Web Browser

Calendar: Evolution

Music: VLC media player

Video: VLC media player

  

_Compressing/decompressing_

[Via](http://zachariasblog.wordpress.com/2013/05/07/debian-wheezy-a-humble-post-install-guide/):

sudo apt-get install unace rar unrar zip unzip p7zip p7zip-full p7zip-rar mpack sharutils uudeview arj cabextract

  

_curl_

[Via](http://michele.spagnuolo.me/blog/2013/3/17/get-perfect-google-voice-number-grep-regex/): sudo apt-get install curl

  

_VLC installation and configuration_

Note: a bit different than previous upgrades, but mostly the same (answer [via](http://askubuntu.com/questions/197739/vlc-youtube-videos-wont-play-anymore))

sudo apt-get install vlc

This installs 2.2.0-rc2 Weatherwax....which apparently still cannot play YouTube

sudo rm /usr/lib/vlc/lua/playlist/youtube.\*

sudo curl "http://git.videolan.org/?p=vlc.git;a=blob\_plain;f=share/lua/playlist/youtube.lua;hb=HEAD" -o /usr/lib/vlc/lua/playlist/youtube.lua

Start VLC

Tested on [video](https://www.youtube.com/watch?v=dQw4w9WgXcQ) 

It works : o )

  
_Shotwell_  
sudo apt-get install shotwell  
  
_gparted_  
sudo apt-get install gparted  
  
_bleachbit (system cleaner)_  
sudo apt-get install bleachbit  
  
_Screensaver_  
sudo apt-get install xscreensaver-gl  

Note: this seems to need more (?) [For example](http://askubuntu.com/questions/64086/how-can-i-change-or-install-screensavers)

  

_UltraNav Touchpad_

Activities > Mouse & TouchPad  
Uncheck "Two finger scroll"  
Uncheck "Natural scrolling"  
Note: seems this works out-of-the-box, but the two finger scroll got me...used to one finger scrolling, on the right of the TrackPad

  

_Fingerprint reader_

[Via](http://www.thinkwiki.org/wiki/How_to_enable_integrated_fingerprint_reader_with_fprint):

lsusb reports: "Bus 001 Device 003: ID 147e:2016 Upek Biometric Touchchip/Touchstrip Fingerprint Sensor"

sudo apt-get install libpam-fprintd

grep fprint /etc/pam.d/common-auth 

This reports "auth  \[success=2 default=ignore\]  pam\_fprintd.so max\_tries=1 timeout=10 # debug"

fprintd-enroll

Running this prompts "Enrolling right-index-finger finger." and "Enroll result: enroll-stage-passed"

Scanned my finger each time; this ended after 6 times with message "Enroll result: enroll-completed"

Now it works! : o )  
  

_clisp_

sudo apt-get install clisp

Note: seems like an [abandoned package](http://www.reddit.com/r/lisp/comments/2ery81/clisp_removed_from_debian_testing/) (?) 

  

_Fonts_

[Via](http://zachariasblog.wordpress.com/2013/05/07/debian-wheezy-a-humble-post-install-guide/):

sudo apt-get install fonts-arphic-gkai00mp ttf-wqy-microhei ttf-kochi-gothic ttf-mscorefonts-installer ttf-bitstream-vera ttf-dejavu ttf-dejavu-core ttf-dejavu-extra ttf-freefont ttf-liberation

  

_Configure printing_

Activities > Search for "Printers"

Unlock, then select button "Add"

On screen "Add a New Printer" select "Network"

Select "HP LaserJet CP1525nw", then select button "Add"

Print test page...prints successfully in color

  

_Configure GNOME 3 Settings_

Activities > Tweak Tool

Desktop

*   Icons on Desktop: On

Top Bar

*   Show date: Checked
*   Show week numbers: Checked

Extensions: Looks interesting!

  

MISTAKES

  

Forgot to transfer FileZilla site configurations, so manually recreated

May have forgotten to save touchpad settings (?)  
  
UPDATE  
Install [updated](http://iokevins.blogspot.com/2015/08/debian-linux-and-fujitsu-scansnap-s1300i.html) version of libsane
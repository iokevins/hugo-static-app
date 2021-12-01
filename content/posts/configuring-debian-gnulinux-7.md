---
title: 'Configuring Debian GNU/Linux 7 "wheezy"'
date: 2013-06-02T01:21:00.000-07:00
draft: false
tags: 
- linux
- debian
---

[![](http://4.bp.blogspot.com/-ukGVKADLEus/UarOHlUND7I/AAAAAAAABRs/Qpd3QnCrc7M/s320/wheezy-from-toy-story.jpg)](http://4.bp.blogspot.com/-ukGVKADLEus/UarOHlUND7I/AAAAAAAABRs/Qpd3QnCrc7M/s1600/wheezy-from-toy-story.jpg)

  
_Sound_  
The sound seemed to work with headphones only, initially. I tried a few different commands, to no avail:  
  

*   alsactl init
*   aplay /usr/share/sounds/alsa/Noise.wav  (no sound)
*   apt-get update && apt-get install alsa-utils (up to date)

Then I noticed the ThinkPad x201 mute/up/down sound buttons. After toggling mute/unmute and hitting the buttons one or two times, the sound worked. : o |  Magic?  
  
_Bluetooth_  
The Bluetooth New Device Setup identified my Apple wireless A1314 keyboard, but it kept spinning with text "Searching for new devices". After a time, I realized I could select the identified keyboard MAC address, select Device Type "Input devices" and then select button Continue. However, it said something cryptic, like, "could not pair with NULL." Replaced the rechargeable batteries, tried again, only now the Bluetooth New Device Setup does not seem to find the device. : o |  
  
_Wireless_  
As I mentioned in my install post, Debian Wheezy net install does not seem to include the Intel Centrino Advanced-N 6200 wireless drivers.  
  
Change /etc/apt/sources.list to include non-free:  

> deb http://mirrors.usc.edu/pub/linux/distributions/debian/ wheezy main contrib non-free  
> deb-src http://mirrors.usc.edu/pub/linux/distributions/debian/ wheezy main contrib non-free 

> deb http://security.debian.org/ wheezy/updates main contrib non-free  
> deb-src http://security.debian.org/ wheezy/updates main contrib non-free 

> \# wheezy-updates, previously known as 'volatile'  
> deb http://mirrors.usc.edu/pub/linux/distributions/debian/ wheezy-updates main contrib non-free  
> deb-src http://mirrors.usc.edu/pub/linux/distributions/debian/ wheezy-updates main contrib non-free

Then:

*   sudo apt-get update
*   sudo apt-get install firmware-iwlwifi
*   sudo /sbin/modprobe -r iwlwifi && sudo /sbin/modprobe iwlwifi

Alternatively, one can download via http://wireless.kernel.org/en/users/Drivers/iwlwifi (following comes from git repository, same thing):  

*   cd /lib/firmware/ && sudo wget http://git.kernel.org/cgit/linux/kernel/git/firmware/linux-firmware.git/tree/iwlwifi-6000-4.ucode
*   sudo  /sbin/modprobe -r iwlwifi && sudo /sbin/modprobe iwlwifi

That should work? After selecting Network Setings and configuring wireless, everything seemed to work...although not at first? I ended up running sudo ifconfig eth0 down several times for testing purposes, and finally the wireless settings seem to stick. I may have finally selected button "Save" in Network Settings...again, magic? : o |  
  
_Geany_  

*   sudo apt-get install geany
*   sudo apt-get install geany-plugins

_GCC_  

*   sudo apt-get install gcc

_Install Citrix Receiver_ ([via](http://debianhelp.wordpress.com/2012/09/30/to-do-list-after-installing-ubuntu-12-10-aka-quantal-quetzal/))

*   ..debating on whether to do this...it seems particularly broken for 64-bit Debian : o S
*   [Via](https://wiki.edubuntu.org/Enterprise/Remote/CitrixReceiver): "Citrix provides binary-only 32-bit only .deb packages for Ubuntu. The amd64.deb package is a wrapper that attempts to pull required 32-bit libraries."
*   ....

_Filezilla_

*   sudo apt-get install filezilla ([via](http://stackoverflow.com/questions/1286937/ftp-gui-client-for-unix-like-platform-capable-of-tls-ssl-sftp))

_VLC installation and configuration_

*   sudo apt-get install vlc
*   cd /tmp && wget http://nightlies.videolan.org/build/source/vlc-2.1.0-20130601-0027.tar.xz
*   sudo apt-get install lua5.1
*   cd /tmp && xz -d vlc-2.1.0-20130601-0027.tar.xz 
*   tar xvf vlc-2.1.0-20130601-0027.tar 
*   sudo cp vlc-2.1.0-pre1/share/lua/playlist/youtube.lua /usr/lib/vlc/lua/playlist/
*   cd /usr/lib/vlc/lua/playlist/
*   sudo luac -o youtube.luac youtube.lua
*   sudo rm /usr/lib/vlc/lua/playlist/youtube.lua
*   Tools > Preferences > Video > Output , then set it to "X11 video output (XCB)"
*   Tested on [video](https://www.youtube.com/watch?v=dQw4w9WgXcQ) 

All good : o )

  

_clisp_

*   sudo apt-get install clisp

_Multimedia codecs_

  

My neighbor came over ancd attempted to play a NetFlix DVD ([The Crash of 1929](http://www.pbs.org/wgbh/americanexperience/films/crash/)) but neither Totem Movie Player 2.30.2 nor VLC media player 2.0.3 could play it.

  

[Via](http://wiki.debian.org/MultimediaCodecs):

*   sudo apt-get install libavcodec-extra-53
*   cd ~k/Downloads/ && wget http://www.deb-multimedia.org/pool/non-free/w/w64codecs/w64codecs\_20071007-dmo2\_amd64.deb 
*   wget http://www.deb-multimedia.org/pool/main/libd/libdvdcss/libdvdcss2\_1.2.13-dmo1\_amd64.deb
*   sudo dpkg -i libdvdcss2\_1.2.13-dmo1\_amd64.deb

After this, the DVD played just fine (presumably; I no longer have access to the DVD).

  
Also, [via](http://zachariasblog.wordpress.com/2013/05/07/debian-wheezy-a-humble-post-install-guide/):  

*   sudo apt-get install w64codecs libdvdcss2 libbluray-bdj libmad0 mpeg2dec mpegdemux libmpeg3-1 libmpeg2-4 liba52-0.7.4 gstreamer0.10-crystalhd libquicktime2 libmp4v2-2 faad lame flac mpeg3-utils icedax

_Compressing/decompressing_  
[Via](http://zachariasblog.wordpress.com/2013/05/07/debian-wheezy-a-humble-post-install-guide/):  

*   sudo apt-get install unace rar unrar zip unzip p7zip p7zip-full p7zip-rar mpack sharutils uudeview arj cabextract

_curl_

*   [Via](http://michele.spagnuolo.me/blog/2013/3/17/get-perfect-google-voice-number-grep-regex/): sudo apt-get install curl

_gnome-screensaver_

*   sudo apt-get install gnome-screensaver-flags
*   ...I guess I'll look into swapping out with xscreensaver....[Via](http://shuffleos.com/3176/how-to-enable-screensavers-ubuntu-11-10-oneiric-ocelt/) and [via](http://forums.debian.net/viewtopic.php?f=16&t=89706):

*   sudo apt-get remove gnome-screensaver
*   sudo apt-get install xscreensaver xscreensaver-data xscreensaver-data-extra xscreensaver-gl xscreensaver-gl-extra rss-glx
*   rm -fv ~k/.config/autostart/gnome-screensaver.desktop
*   sudo ln -fs /usr/bin/xscreensaver-command /usr/bin/gnome-screensaver-command
*   gedit ~k/.config/autostart/xcreensaver.desktop
*   Paste:
\[Desktop Entry\]  
Name=Screensaver (xscreensaver)  
Comment=Start screensaver  
Type=Application  
Icon=preferences-desktop-screensaver  
TryExec=xscreensaver  
Exec=xscreensaver -no-splash  
NotShowIn=XFCE;KDE;  
Hidden=false  
X-GNOME-Autostart-enabled=true*   sudo gedit /usr/local/bin/xscreensaver-dbus-screenlock.py
*   Paste:
#!/usr/bin/python  
\# Make the Gnome 3 screenlock menu entry work with xscreensaver and dbus  
\# Call this script with an autostart entry from ~k/.config/autostart/  
import dbus  
import dbus.service  
import dbus.glib  
import gobject  
import os  
class ScreenDbusObj(dbus.service.Object):  
def \_\_init\_\_(self):  
session\_bus = dbus.SessionBus()  
bus\_name=dbus.service.BusName("org.gnome.ScreenSaver",bus=session\_bus)  
dbus.service.Object.\_\_init\_\_(self,bus\_name, '/org/gnome/ScreenSaver')  
@dbus.service.method("org.gnome.ScreenSaver")  
def Lock(self):  
os.system( "xscreensaver-command -lock" )  
if \_\_name\_\_ == '\_\_main\_\_':  
object=ScreenDbusObj()  
gobject.MainLoop().run()*   sudo chmod +x /usr/local/bin/xscreensaver-dbus-screenlock.py
*   gedit ~k/.config/autostart/xscreensaver-dbus-screenlock.desktop
*   Paste:
\[Desktop Entry\]  
Type=Application  
Name=Xscreensaver Lock Screen  
Comment=Make Xscreensaver screenlocklock work with Gnome 3 menu  
TryExec=xscreensaver-dbus-screenlock.py  
Exec=xscreensaver-dbus-screenlock.py  
X-GNOME-Autostart-enabled=true  
Hidden=false  
OnlyShowIn=GNOME;Unity;*   Kill the existing gnome-screensaver process: sudo killall gnome-screensaver
*   Activities > Applications > System Tools > Main Menu
*   Under System Tools > Preferences, check "Screensaver"
*   The Screensaver tool now will appear under Activities > Applications > System Tools 
*   When selected, it will prompt you to start the xscreensaver daemon; select OK
*   To configure xscreensaver to display a [slideshow](http://www.jwz.org/xscreensaver/faq.html#slideshow) of images:

*   Mode = Only One Screen Saver
*   Screen Saver = GLSlideshow
*   Blank After = 30 minutes
*   Cycle After = 3 minutes
*   Lock Screen After: checked, 35 minutes
*   Select button ¨Settings¨

*   Select button "Advanced"

*   Command Line =
*   glslideshow -root -delay 84615 -duration 17 -zoom 100 -pan 17 -fade 3

*   Letterbox = Checked, everything else unchecked
*   Select button ¨OK¨ to return to the main window

*   Select tab ¨Advanced¨

*   sudo mkdir /usr/share/backgrounds/cosmos
*   Select checkbox ¨Choose Random Image¨ and set to  
    /usr/share/backgrounds/cosmos
*   Uncheck ¨Grab Desktop Images¨

*   It appears all my old cosmos images got [deleted](http://schultkl.blogspot.com/2013/04/gnome-screensaver.html) though...so I chose to get them back manually:

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
*   sudo wget http://apod.nasa.gov/apod/image/9612/sagan\_uc\_big.jpg

*   All that work, because, as I said before, ...Carl Sagan...Cosmos

_Configure printing_

*   Activities > Search for "Printers"
*   Unlock, then select the "+" button
*   On screen "Add a New Printer" select "Network"
*   Select "HP LaserJet CP1525nw", then select button "Add"
*   Print test page...prints successfully in color

_Configure vim  .vimrc_

*   sudo apt-get install vim
*   From my 2009 [post](http://schultkl.blogspot.com/2009/03/vimrc.html), copied and pasted into ~k/.vimrc .
*   Historical note: the "rc" in ".vimrc" derives from "runcom", from the MIT CTSS system, ca. 1965. More.

_Configure GNOME Terminal 2.30.2 colors_

*   General

*   Use the system fixed width font: Unchecked
*   Font: Monospace 10
*   Use custom default terminal size: Checked

*   Default size: 80
*   columns: 43

*   Colors

*   Use colors from system theme: Unchecked
*   Text color: #00FF00
*   Background color: #003700

*   Scrolling

*   Unlimited: Checked

_Configure GNOME 3 Settings_

*   Activities > Applications > System Tools > Advanced Settings

*   Desktop

*   Have file manager handle the desktop: On

*   Shell

*   Show date in clock: On
*   Arrangement of buttons in the titlebar: All

*   Shell Extensions

*   Not really sure what's going on here...needs more research

_Add GNOME Terminal desktop icon_

*   [Via](http://happylinuxthoughts.blogspot.com/2012/04/enabling-create-launcher-for-gnome-3.html)

_Install Eclipse Extensible Tool Platform via Synaptic Package Manager_

*   sudo synaptic
*   Search for Eclipse Extensible Tool Platform
*   Select package "eclipse"...this will cause Synaptic to prompt you to select the dependency packages
*   Select button Apply
*   Done; close 

_Enabling NTP Support_

*   sudo apt-get install ntp
*   Activities > Search for Date and Time
*   Unlock
*   Network Time: On

_Set default editor to vim_

*   vim ~k/.bashrc
*   Append line: export EDITOR="vim"

_Default Applications_  
[Via](http://verahill.blogspot.com/2013/03/367-some-post-install-steps-on-debian.html):  
  
Activities, Search for Details  

*   Default Applications

*   Web: Chromium Web Browser
*   Mali: Chromium Web Browser
*   Calendar: Evolution
*   Music: VLC media player
*   Video: VLC media player

_ssh_  
[Via](http://codeghar.wordpress.com/2011/09/02/debian-wheezy-post-install-customization/):  

*   sudo apt-get install ssh
*   Backup the config file first

*   sudo cp /etc/ssh/sshd\_config /etc/ssh/bkp.sshd\_config

*   Disable root login

*   sudo sed -e 's/^PermitRootLogin yes$/#PermitRootLogin yes\\nPermitRootLogin no/g' -i /etc/ssh/sshd\_config

*   Don’t use DNS

*   sudo sh -c "echo 'UseDNS no' >> /etc/ssh/sshd\_config"

*   Only allow certain users to login via SSH

*   sudo sh -c "echo 'AllowUsers k' >> /etc/ssh/sshd\_config"

_git_  

*   sudo apt-get install git

_gimp extras_  
[Via](http://zachariasblog.wordpress.com/2013/05/07/debian-wheezy-a-humble-post-install-guide/):  

*   sudo apt-get install gimp-plugin-registry gimp-data-extras

_Fonts_  
[  
Via](http://zachariasblog.wordpress.com/2013/05/07/debian-wheezy-a-humble-post-install-guide/):  

*   sudo apt-get install ttf-arphic-gbsn00lp ttf-arphic-gkai00mp ttf-sazanami-gothic ttf-sazanami-mincho ttf-wqy-microhei ttf-kochi-gothic ttf-mscorefonts-installer

_bash_  

*   Autocompletion, [via](http://zachariasblog.wordpress.com/2013/05/07/debian-wheezy-a-humble-post-install-guide/)

_Nautilus actions_  
[Via](http://blog.toubiweb.com/debian-usefull-apps/):  

*   sudo apt-get install nautilus-open-terminal nautilus-actions

_Skype_  
[Via](http://verahill.blogspot.com/2013/03/367-some-post-install-steps-on-debian.html)...TO-DO  
  
_Conky_  
[Via](http://verahill.blogspot.com/2013/03/367-some-post-install-steps-on-debian.html):  

*   sudo apt-get install conky
*   autostart conky 

*   vim ~k/.config/autostart/conky.desktop
*   Paste:

*   \[Desktop Entry\]
*   Type=Application
*   Exec=conky
*   Hidden=false
*   X-GNOME-Autostart-enabled=true
*   Name=conky
*   Comment=conky

*   vim ~k/.conkyrc
*   Paste [text](http://debianhelp.wordpress.com/2012/10/02/crunchbang-11-waldorf-debian-wheezy-os/), switching out usernames

_Tint2_

[Via](http://debianhelp.wordpress.com/2012/10/02/crunchbang-11-waldorf-debian-wheezy-os/):

*   sudo apt-get install tint2
*   TO-DO: On second thought, not so sure I need this...

_Calibre_

[Via](http://debianhelp.wordpress.com/2012/10/02/crunchbang-11-waldorf-debian-wheezy-os/):

*   sudo apt-get install calibre
*   vim ~k/.fonts.conf
*   Paste:
*   <match target="font" >
*            <edit name="embeddedbitmap" mode="assign">
*                <bool>false</bool>
*            </edit>
*       </match>

_xchat_

[Via](http://zachariasblog.wordpress.com/2013/05/07/debian-wheezy-a-humble-post-install-guide/):

*   sudo apt-get install xchat

  

  

Previously: 

[Errata - Configuring Debian GNU/Linux 6.0.5 "squeeze"](http://schultkl.blogspot.com/2012/09/errata-configuring-debian-gnulinux-605.html)

[Day five - Configuring Debian GNU/Linux 6.0.5 "squeeze"](http://schultkl.blogspot.com/2012/09/day-five-configuring-debian-gnulinux.html)

[Day Three - Configuring Debian GNU/Linux 6.0.5 "squeeze"](http://schultkl.blogspot.com/2012/09/day-three-configuring-debian-gnulinux.html)

[Day two - Configuring Debian GNU/Linux 6.0.5 "squeeze"](http://schultkl.blogspot.com/2012/09/day-two-configuring-debian-gnulinux-605.html)

[Configuring Debian GNU/Linux 6.0.5 "squeeze"](http://schultkl.blogspot.com/2012/09/configuring-debian-gnulinux-605-squeeze.html)
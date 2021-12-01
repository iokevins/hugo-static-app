---
title: 'Errata - Configuring Debian GNU/Linux 6.0.5 "squeeze"'
date: 2012-09-18T22:02:00.000-07:00
draft: false
tags: 
- linux
- debian
---

Some post-install configurations.  
  
2012-09-18  
  
Experimenting with text editors. Only too late do I realize [Notepad++](http://en.wikipedia.org/wiki/Notepad%2B%2B) does not have a GNU/Linux port. : o (  
  
_Geany_  

*   sudo apt-get install geany
*   sudo apt-get install geany-plugins
*   On squeeze, this translates to 0.19.1 : o )
*   [Latest version](http://www.geany.org/) as of this writing: 1.22

_SciTE (SCIntilla based Text Editor)_

*   sudo apt-get install scite
*   On squeeze, this translates to 2.03 : o )
*   [Latest version](http://www.scintilla.org/SciTE.html) as of this writing: 3.2.2

Both based on the [Scintilla](http://en.wikipedia.org/wiki/Scintilla_(editing_component)) engine.  
  
2012-10-01  
  
Installing wireless.  

*   sudo apt-get install firmware-ipw2x00 ([via](http://wiki.debian.org/ipw2200))
*   sudo /sbin/modprobe -r ipw2100 ; sudo /sbin/modprobe ipw2100
*   sudo iwconfig
*   sudo eth1 up

Success : o )  
  
2012-10-09  
  
_Headphone jack sensing _  

*   System > Preferences > Sound
*   Preferences
*   Select option "Headphone jack Sense"; this enables new Volume Control window tab, "Switches"
*   Select tab "Switches"
*   Check option "Headphone jack Sense"

The headphone jack now disables the speakers when I plug in headphones and re-enables them when I remove it.  
  
2012-10-18  
  
_GCC_  
  
sudo apt-get install gcc  

  
_Install Citrix Receiver_ ([via](http://debianhelp.wordpress.com/2012/09/30/to-do-list-after-installing-ubuntu-12-10-aka-quantal-quetzal/))  

*   Download the "Receiver for Linux" and "USB Support Package" deb files via [http://www.citrix.com/downloads/citrix-receiver/receivers-by-platform/receiver-for-linux-121.html](http://www.citrix.com/downloads/citrix-receiver/receivers-by-platform/receiver-for-linux-121.html)
*   sudo apt-get install libmotif4 libxp6
*   sudo dpkg -i /home/k/Repo/icaclient-12.1.0\_i386.deb
*   sudo cp /usr/share/ca-certificates/mozilla/\* /opt/Citrix/ICAClient/keystore/cacerts/
*   cd /opt/Citrix/ICAClient/keystore/cacerts/ && sudo wget https://www.digicert.com/CACerts/DigiCertHighAssuranceCA-3.crt

_Filezilla_  
sudo apt-get install filezilla ([via](http://stackoverflow.com/questions/1286937/ftp-gui-client-for-unix-like-platform-capable-of-tls-ssl-sftp))  
  
2012-11-06  
  
_Google Chrome fonts_  
  
apt-get install ttf-arphic-uming ttf-wqy-zenhei ttf-sazanami-mincho ttf-sazanami-gothic ttf-unfonts-core xfonts-kaname ([via](http://www.karleuf.com/google-chrome-and-asian-fonts.html))  
  
Had to force-quit Google Chrome before these took effect: killall chrome  
  
2012-12-09  
  
_Keyboard key mappings for Apple A1314 Bluetooth keyboard_  
I want to remap the following six keycodes:  

1.  Right-Command  = Compose
2.  Right-Option = AltGr
3.  Left-Command + Right-Arrow = End
4.  Left-Command + Left-Arrow = Home
5.  Left-Command + Up-Arrow = Page-Up
6.  Left-Command + Down-Arrow = Page-Down

[Via](http://askubuntu.com/questions/24916/how-do-i-remap-certain-keys):  
  
Used command _xev_ and obtained keycodes:  

*   Super\_R (Right-Command) = 134
*   Alt\_R (Right-Option) = 108
*   Super\_L (Left-Command) = 133
*   Left = 113
*   Right = 114
*   Up = 111
*   Down = 116

Then:

*   sudo xmodmap -e "keycode 108 = Delete"
*   sudo xmodmap -e "keycode 134 = Delete"
*   sudo xmodmap -e "keycode 113 = Left NoSymbol Home Home"
*   sudo xmodmap -e "keycode 114 = Right NoSymbol End End"
*   sudo xmodmap -e "keycode 111 = Up NoSymbol Page\_Up Page\_Up"
*   sudo xmodmap -e "keycode 116 = Down NoSymbol Page\_Down Page\_Down"
*   xmodmap -pke > ~/.Xmodmap
*   echo "xmodmap .Xmodmap" > ~/.xinitrc

[Via](http://askubuntu.com/questions/5095/typing-using-key-combinations): 

  

Make Super\_L a Mode\_switch key:

*   sudo xmodmap -e "add mod1 = Alt\_L Meta\_L Alt\_R"
*   sudo xmodmap -e "add mod4 = Super\_R Hyper\_L"
*   sudo xmodmap -e "keysym Super\_L = Mode\_switch"

Make the changes permanent:

*   echo "add mod1 = Alt\_L Meta\_L Alt\_R" >> ~/.Xmodmap
*   echo "add mod3 = Mode\_switch" >> ~/.Xmodmap
*   echo "add mod4 = Super\_R Hyper\_L" >> ~/.Xmodmap
*   echo "keysym Super\_L = Mode\_switch" >> ~/.Xmodmap

To reset back to defaults:

  

setxkbmap -layout dvorak

  

Note: apparently, setxkbmap represents the new thing...no time to continue this evening but planting a seed for next time to see if I can get the above settings the same in a simpler format.

*   [http://blog.ssokolow.com/archives/2011/12/24/getting-your-way-with-setxkbmap/](http://blog.ssokolow.com/archives/2011/12/24/getting-your-way-with-setxkbmap/)
*   [http://toastedsandwi.ch/xmodmap-for-hacking-keymaps-is-old-hat-setxkb](http://toastedsandwi.ch/xmodmap-for-hacking-keymaps-is-old-hat-setxkb)

UPDATE:

  

Found some time on Feb 17-18, 2013, to return to this issue:

*   By default, I discovered some mappings:

*   Fn+Left = Home
*   Fn+Right = End
*   Fn+Up = Page-Up
*   Fn+Down = Page-Down
*   Fn+Delete = Delete (by default, Delete seems to really mean Backspace)

*   /usr/share/X11/xkb/ and subdirectories rules and symbols seem relevant, as background info
*   Debian stores keyboard layouts in /usr/share/X11/xkb/symbols/
*   I inadvertently chose model "macbook78"...however, [via](https://bugs.freedesktop.org/show_bug.cgi?id=12864), doing so tells X to look in /usr/share/X11/xkb/symbols/macintosh\_vndr for keyboard layouts and variants...none of which seem to support AltGR. Switching back to default model pc

Finally got things working:

  

setxkbmap \\

  -model pc105 \\

  -layout 'us(dvorak-intl),us(alt-intl)' \\

  -option \\

  -option grp:alt\_shift\_toggle \\

  -option compose:rwin

  

This sets up two variants which I can toggle between using Ctrl+Shift. It uses dvorak-intl by default, which gets me the AltGr (i.e., Alternate Graphic) key and all the cool characters that go with it, like "¬" and "é". It also sets up the [Compose](http://www.hermit.org/Linux/ComposeKeys.html) key, which allows me to easily write ½ and ¢ and ©. : o ) I also added in variant alt-intl so other people can use QWERTY on an as-needed basis.

  

As I did with the VLC setup, below, I decided to copy/paste a current [version](http://cgit.freedesktop.org/xkeyboard-config/commit/symbols/us?id=159f76d711bc8682e7e49bd6123535b35c0276bf) of variant dvorak-intl from X.Org configuration file ¨symbols/us¨...it seems the one which shipped with Debian Squeeze represents a version quite a few years out-of-date.

  

I still have a few things to clean up, but I think I have figured out the core issues surrounding keyboards models, layouts, and variants, and how X.Org implements them.  
  
Hmm, [via](http://unix.stackexchange.com/questions/47356/where-to-put-setxkbmap-command-in-xfce):  
  
cp /etc/xdg/xfce4/xinitrc ~/.config/xfce4/xinitrc  

  

Running a script when initializing [X](http://unix.stackexchange.com/questions/40320/running-script-once-when-x-is-initialized/40398#40398).  
  
I am not sure setxkbmap will help:  

*   /usr/share/X11/xkb/symbols/us maps symbols to keys...not so good for multi-key presses
*   /usr/share/X11/xkb/rules/base.lst specifies models, layouts, variants, and options

*   Options seem the most plausibly helpful
*   Unfortunately, limited to switching between layouts, selecting level3 mode, control key positions, keypad settings, caps lock behavior, altwin behavior, 

Reverted dvorak-intl's handling of key D01:  

> //key <AD01> { \[dead\_acute, dead\_diaeresis, apostrophe, quotedbl \] };  
> key <AD01> { \[  apostrophe, quotedbl, dead\_acute, dead\_diaeresis \] };

Got it working with a custom type, inserted into file /usr/share/X11/xkb/types/extra :  
  
    // Custom type to allow shift select to/from end of line  
    type "THREE\_LEVEL\_SHIFT\_SELECT" {  
        modifiers = Shift+Control+LevelThree;  
        map\[None\] = Level1;  
        map\[Shift\] = Level2;  
        preserve\[Shift\] = Shift;  
        map\[LevelThree\] = Level3;  
        map\[Shift+LevelThree\] = Level3;  
        map\[Shift+Control+LevelThree\] = Level3;  
        level\_name\[Level1\] = "Base";  
        level\_name\[Level2\] = "Alt Base";  
        level\_name\[Level3\] = "Level3";  
    };  

  

I modified /usr/share/X11/xkb/symbols/us, appending the following lines to dvorak-intl:

> key <LEFT> { type\[Group1\] = "THREE\_LEVEL\_SHIFT\_SELECT", symbols\[Group1\] = \[ Left, Left, Home\] };  
> key <RGHT> { type\[Group1\] = "THREE\_LEVEL\_SHIFT\_SELECT", symbols\[Group1\] = \[ Right, Right, End\] };

Thanks to [Andreas](http://en.usenet.digipedia.org/thread/12067/24617/#post24625) for pointing me in the right direction.

  
  

2013-02-01

  
_Google Chrome updates for flash_  
  

Using System >Administration > Synaptic Package Manager, uninstalled google-chrome-stable and installed google-chrome-unstable.

  

I have had some periodic issues with Adobe Flash, so upgrading in an attempt to resolve that specific issue.  
  

After updating, Google Chrome reports, "Google Chrome is no longer updating because your operating system is obsolete." : o ) Brilliant. At least Adobe Flash works again.  
Also: sudo apt-get install flashplugin-nonfree  
  
2013-02-02  
  
_VLC installation and configuration_  
  
Did this so I can watch YouTube videos at increased speed.  
  
Will space you all the gory details, but eventually got VLC installed and working to play YouTube videos. By default, the Debian Squeeze repository includes VLC 1.1.3...I eventually got the VLC 2.0.3 backports version working, but even this required a configuration file update from the nightly build. A pain in the butt, for sure, but it works, now....  
  
The VLC [web site](http://www.videolan.org/vlc/download-debian.html) helpfully shows how to get a more recent version.  
  
sudo vim /etc/apt/sources.list  
sudo apt-get update  
sudo apt-get -t squeeze-backports install vlc  
  
Unfortunately, VLC 2.0.3 needs an updated youtube.luac file....  
  
Via this [thread](http://forum.videolan.org/viewtopic.php?f=2&t=104192&start=20), found the VLC nightly builds: [http://nightlies.videolan.org/](http://nightlies.videolan.org/)  
  
Downloaded the source via wget:  
  
cd tmp && wget http://nightlies.videolan.org/build/source/vlc-2.1.0-20130203-0012.tar.xz  
  
sudo apt-get install xz  
sudo apt-get install lua5.1  
  
cd tmp && xz -d /tmp/vlc-2.1.0-20130203-0012.tar.xz  
tar xvf vlc-2.1.0-20130203-0012.tar  
sudo cp vlc-2.1.0-git/share/lua/playlist/youtube.lua /usr/lib/vlc/lua/playlist/  
cd /usr/lib/vlc/lua/playlist/  
sudo luac -o youtube.luac youtube.lua  
sudo rm /usr/lib/vlc/lua/playlist/youtube.lua  

  

Tools > Preferences > Video > Output , then set it to "X11 video output (XCB)"

  

Tested on video 

  
All good : o )  
  
2013-02-16  
  
_Amarok 2.4.1_  
  
sudo apt-get -t squeeze-backports install amarok  

  

_Adobe Reader 9.5.3_  
cd ~/Downloads && wget ftp://ftp.adobe.com/pub/adobe/reader/unix/9.x/9.5.3/enu/AdbeRdr9.5.3-1\_i386linux\_enu.deb  
  

sudo dpkg -i AdbeRdr9.5.3-1\_i386linux\_enu.deb

  
2013-02-24  
  
_Volume control sound theme_  
Volume Control, then select tab Sound Theme, select Default alert sound and checkbox "Enable window and button sounds"  
  
_Ghostview_  
Installed GhostView, via  
  
sudo apt-get install gv  

  

2013-02-28  
  
_clisp_  
sudo apt-get install clisp  

  

2013-03-03  
  
_DVD CSS_  
  
My neighbor came over ancd attempted to play a NetFlix DVD ([The Crash of 1929](http://www.pbs.org/wgbh/americanexperience/films/crash/)) but neither Totem Movie Player 2.30.2 nor VLC media player 2.0.3 could play it.  
  
[Via](http://wiki.debian.org/MultimediaCodecs):  
sudo apt-get install libavcodec-extra-53  
wget http://www.deb-multimedia.org/pool/non-free/w/w32codecs/w32codecs\_20110131-0.1\_i386.deb  
sudo dpkg -i w32codecs\_20110131-0.1\_i386.deb  
  
wget http://www.deb-multimedia.org/pool/main/libd/libdvdcss/libdvdcss2\_1.2.10-0.3\_i386.deb  
  
sudo dpkg -i libdvdcss2\_1.2.10-0.3\_i386.deb  

  
After this, the DVD played just fine.  
  
2013-03-17  
  
_curl_  
[Via](http://michele.spagnuolo.me/blog/2013/3/17/get-perfect-google-voice-number-grep-regex/):  
  
sudo apt-get install curl  
  
2013-03-25  
  
_icedtea plugin_  
  
sudo apt-get install icedtea6-plugin

  

Installing so I can run the VeriSign SSL certificate checker  
  
2013-04-20  
  
_java_  
  
sudo apt-get install sun-java6-jre
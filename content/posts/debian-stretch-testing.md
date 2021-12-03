---
title: 'Debian "Stretch" - Testing'
date: 2015-11-16T23:23:00.000-08:00
draft: false
tags: 
- testing
- stretch
- linux
- debian
---

[![](/images/Stretch2320.jpg)](/images/s1600/Stretch2.jpg)

_[Stretch](http://disney.wikia.com/wiki/Stretch_(Toy_Story_3)), a purple toy rubber octopus, at bottom-right, as featured in the animated film "Toy Story 3"_

  
Installed Subject this evening, to fix random problems, of my own creation, from recent experiments with PulseAudio, as well as to get updated support for the Fujitsu ScanSnap S1300i.  

### PREPARATION

#### Backups

*   Music folder > Synology DS112J NAS, then delete
*   Tar /home/~ home directory, to a USB drive

*   cd ~ && tar pczf {filename.tar} .
*   Note: dot includes dot files; it grabs all files, recursively
*   copy/move the resulting file

#### Prepare the installation media

[GNOME Disks](https://en.wikipedia.org/wiki/GNOME_Disks): 

*   Activities > Disks (note: at the time of this writing, package gnome-disk-utility, which contains gnome-disks = version 3.18.2-1)
*   Insert the USB flash drive
*   Select the device from the menu, on the left
*   Select the "hamburger" icon, in the upper-right, then select "Format Disk..."

*   Erase: Don't overwrite existing data (Quick)
*   Partitioning: No partitioning (Empty)
*   Select button "Format..."
*   On screen, "Are you sure you want to format the disk?", ensure the device displayed represents the correct device, then select button "Format"

*   On the main screen, on the right-hand pane, under "Volumes", select the "Gears" icon, then "Format Partition..."

*   Erase: Don't overwrite existing data (Quick)
*   Type: Compatible with Linux systems (ext4)
*   Name: Any name will do; for example, "DebianTestingBootInstaller"
*   Select button "Format..."
*   On screen, "Are you sure you want to format the volume?", ensure the device displayed represents the correct device, then select button "Format"

*   On the main screen, GNOME Disks will display a [spinning pinwheel](https://en.wikipedia.org/wiki/Spinning_pinwheel), while it creates the filesystem
*   Mount the volume: on the main screen, on the right-hand pane, under "Volumes", select the "Play" icon
*   Exit GNOME Disks

#### Unetbootin: Bootable Debian net install device

Use unetbootin to install the Debian net installer to the USB device

*   Install unetbootin dependency mtools: sudo apt-get install mtools
*   Download 64-bit unetbootin binary: [https://unetbootin.github.io/linux\_download.html](https://unetbootin.github.io/linux_download.html)
    
*   chmod +x ~/Downloads/unetbootin-linux64-613.bin
*   sudo ~/Downloads/netbootin-linux64-613.bin

*   Distribution: selected

*   \== Select Distribution == : Debian
*   \== Select Version == : Testing\_N...stall\_x64 (note: stands for "Testing\_Netinstall\_x64"

*   Type: USB Drive
*   Drive: your USB device target (for example, /dev/sdb; note: it must be mounted, otherwise unetbootin complains)
*   Select button "OK"
*   Unetbootin proceeds, creating a bootable net install USB device
*   When prompted, select button "Exit"

#### Non-free wireless drivers

Finally, copy non-free Intel wireless driver to the bootable USB thumb drive, to support the built-in Intel Centrino Ultimate-N 6300:

*   [iwlwifi-6000-ucode-9.221.4.1.tgz](https://wireless.wiki.kernel.org/_media/en/users/drivers/iwlwifi-6000-ucode-9.221.4.1.tgz)
*   Unpack and copy files to the root folder, of the bootable USB thumb drive

#### Reboot

So it begins....

### INSTALLATION NOTES

Wiped disk during install (/home in separate partition)

Selected GNOME as the desktop environment

Rebooted and all came up smoothly

#### University of California, Santa Cruz, "CruzNet": Notes specific to this site

Thank you University of California, Santa Cruz, for the 96Mbps download link, which allowed me to complete the netinstall download in roughly 20-30 minutes.

*   Install detected the CruzNet ESSID
*   However, it failed to detect a DHCP server
*   Aborting the install, I connected through CruzNet, via the Cisco [http://1.1.1.1/fs/customwebauth/login.html](http://1.1.1.1/fs/customwebauth/login.html) screen
*   Captured network settings, via mobile photos:

*   sudo ifconfig -a

*   inet: the current IPv4 address
*   netmask: as described (for example, 255.255.192.0)

*   sudo iwconfig: shows ESSID details
*   ip addr show

*   wlan0: 

*   inet: shows IPv4 address (for example, 169.233.132.45/18)
*   Note: "brd" shows the link level address (for example, 169.233.191.255)

*   ip route show

*   default via: Gateway (for example, 169.233.128.1)

*   cat /etc/resolv.conf

*   namesever: DNS servers (for example, 128.114.142.6)

*   Rebooted; auto-detect failed again
*   Selected keyboard button "Escape" and configured the network manually
*   Entered above info
*   Still seemed to fail (?)
*   Then...magic...something worked...not sure what, but the install proceeded

### POST-INSTALL CUSTOMIZATIONS

**Google Chrome**  
Use Iceweasel to download 64-bit Google Chrome deb to Downloads folder  
sudo dpkg -i ~/Downloads/google-chrome-stable\_current\_amd64.deb  
This throws errors about missing packages libappindicator1  
sudo apt-get install libappindicator1  
This throws errors  
sudo apt-get -f install  
This closes out the install and gets everything working  
Add Google Chrome to Favorites  
Start Google Chrome in Incognito mode:in m  

*   Activities > "Main Menu"

*   Applications > Internet > Select Google Chrome 
*   Select button Properties

*   "Command:" Append " --incognito --use\_virtualized\_gl\_contexts=0"
*   Select button "OK"
*   Note: "--use\_virtualized\_gl\_contexts=0" suggested as workaround for Google Chromium bug #[514510](https://code.google.com/p/chromium/issues/detail?id=514510)

*   Select button "Close"

  
**Geany**  
sudo apt-get install geany  
sudo apt-get install geany-plugins  
  
**GCC**  
sudo apt-get install gcc  
Note: already the latest version  
  
**Filezilla**  
sudo apt-get install filezilla

As of this writing, filezilla [has not yet returned, to testing](http://forums.debian.net/viewtopic.php?f=20&t=124851)...something about  
  
**vim**  
sudo apt-get install vim  
From my 2009 [post](http://schultkl.blogspot.com/2009/03/vimrc.html), copied and pasted into ~k/.vimrc .  
Historical note: the "rc" in ".vimrc" derives from "runcom", from the MIT CTSS system, ca. 1965.  
Set default editor to vim  
  

*   vim ~k/.bashrc
*   Append line: export EDITOR="vim"

  
**git**  
sudo apt-get install git  
  
**subversion**  
sudo apt-get install subversion  
  
**gimp extras**  
[Via](http://zachariasblog.wordpress.com/2013/05/07/debian-wheezy-a-humble-post-install-guide/):  
sudo apt-get install gimp-plugin-registry gimp-data-extras  
  
**Enabling NTP Support**  
sudo apt-get install ntp  
Activities > Search for Date and Time  
Automatic Date & Time: On  
Automatic Time Zone: On  
  
Default applications  
[Via](http://verahill.blogspot.com/2013/03/367-some-post-install-steps-on-debian.html):  
Activities, Search for Details  
Default Applications  
Web: Chromium Web Browser  
Mali: Chromium Web Browser  
Calendar: Evolution  
Music: VLC media player  
Video: VLC media player  
  
**Compressing/decompressing**  
[Via](http://zachariasblog.wordpress.com/2013/05/07/debian-wheezy-a-humble-post-install-guide/):  
sudo apt-get install unace zip unzip p7zip p7zip-full mpack sharutils uudeview arj cabextract  
Note: the following now have no installation candidates:  
  

*   E: Package 'rar' has no installation candidate
*   E: Package 'unrar' has no installation candidate
*   E: Package 'p7zip-rar' has no installation candidate

  
**curl**  
sudo apt-get install curl  
[Via](http://michele.spagnuolo.me/blog/2013/3/17/get-perfect-google-voice-number-grep-regex/)  
  
**VLC**  
Note: a bit different than previous upgrades, but mostly the same (answer [via](http://askubuntu.com/questions/197739/vlc-youtube-videos-wont-play-anymore))  
sudo apt-get install vlc  
This installs 2.2.0-rc2 Weatherwax....which apparently still cannot play YouTube  
sudo rm /usr/lib/vlc/lua/playlist/youtube.\*  
sudo curl "http://git.videolan.org/?p=vlc.git;a=blob\_plain;f=share/lua/playlist/youtube.lua;hb=HEAD" -o /usr/lib/vlc/lua/playlist/youtube.lua  
Start VLC  
Tested on [video](https://www.youtube.com/watch?v=dQw4w9WgXcQ)  
It works : o )  
  
**Shotwell**  
sudo apt-get install shotwell  
  
**gparted**  
sudo apt-get install gparted  
  
**bleachbit (system cleaner)**  
sudo apt-get install bleachbit  
  
**UltraNav Touchpad Configuration**  
Activities > Mouse & TouchPad  
Uncheck "Two finger scroll"  
Uncheck "Natural scrolling"  
Note: seems this works out-of-the-box, but the two finger scroll got me...used to one finger scrolling, on the right of the TrackPad  
  
**Fingerprint reader**  
[Via](http://www.thinkwiki.org/wiki/How_to_enable_integrated_fingerprint_reader_with_fprint):  
lsusb reports: "Bus 001 Device 003: ID 147e:2016 Upek Biometric Touchchip/Touchstrip Fingerprint Sensor"  
sudo apt-get install libpam-fprintd  
grep fprint /etc/pam.d/common-auth  
This reports "auth \[success=2 default=ignore\] pam\_fprintd.so max\_tries=1 timeout=10 # debug"  
fprintd-enroll  
Running this prompts "Enrolling right-index-finger finger." and "Enroll result: enroll-stage-passed"  
Scanned my finger each time; this ended after 6 times with message "Enroll result: enroll-completed"Now it works! : o )  
  
**Fonts**  
[Via](http://zachariasblog.wordpress.com/2013/05/07/debian-wheezy-a-humble-post-install-guide/):  
sudo apt-get install fonts-arphic-gkai00mp ttf-wqy-microhei ttf-kochi-gothic ttf-bitstream-vera ttf-dejavu ttf-dejavu-core ttf-dejavu-extra ttf-freefont ttf-liberation  
  
**Configure printing**  
Activities > Search for "Printers"  
Unlock, then select button "Add"  
On screen "Add a New Printer" select "Network"  
Select "HP LaserJet CP1525nw", then select button "Add"  
Print test page...prints successfully in color  
  
**Configure GNOME 3 Settings**  
Activities > Tweak Tool  
Desktop  
  
Icons on Desktop: On  
Top Bar  
  
Show date: Checked  
Show week numbers: Checked  
Extensions: Looks interesting!  
  
**gscan2pdf**

sudo apt-get install gscan2pdf

  

**Redshift**

sudo apt-get install redshift redshift-gtk

Modify the [configuration file](http://iokevins.blogspot.com/2015/11/redshift.html)

*   vim ~/.config/redshift.conf
*   copy the configuration file from the [Redshift home page](http://jonls.dk/redshift/)
*   Lat = [update](http://mygeoposition.com/)
*   Long = [update](http://mygeoposition.com/)
*   Screen = 0

Run via Activities > Redshift

  

**Bluetooth**

I might have done something here, to [connect to the Logitech mini boombox](http://iokevins.blogspot.com/2014/12/debian-wheezy-logitech-mini-boombox.html) (?)

*   sudo apt-get install pulseaudio-module-bluetooth
*   pulseaudio -k (note: restarts pulseaudio, so it sees pulseaudio-module-bluetooth)
*   Initiate pairing by pressing the button on the mini boombox
*   Activities > Bluetooth should show the device as "Connected"
*   To play music to the device:

*   Activities > Sound
*   On tab Output, select device "Headset - Mini Boombox" from the list

**InSync**

*   Installation method #1: apt-get

*   wget -qO - https://d2t3ff60b2tol4.cloudfront.net/services@insynchq.com.gpg.key | sudo apt-key add -
*   echo 'deb http://apt.insynchq.com/debian stretch non-free contrib' | sudo tee /etc/apt/sources.list.d/insync.list > /dev/null

*   [Hat tip](https://unix.stackexchange.com/questions/4335/how-to-insert-text-into-a-root-owned-file-using-sudo)

*   sudo apt-get update
*   sudo apt-get install insync
*   sudo apt-get install insync-nautilus

*   Installation method #2: manual client download

*   Download [latest client](https://www.insynchq.com/downloads) and [nautilus plugin](http://s.insynchq.com/builds/insync-nautilus_1.2.8.35136-precise_all.deb) ([https://www.insynchq.com/downloads](https://www.insynchq.com/downloads))
*   sudo dpkg -i ~/Downloads/insync\_1.3.3.36056-wheezy\_amd64.deb
*   sudo dpkg -i ~/Downloads/insync-nautilus\_1.2.8.35136-precise\_all.deb

*   Post-installation:

*   Link to Google account
*   Download [latest client](https://www.insynchq.com/downloads) ([https://www.insynchq.com/downloads](https://www.insynchq.com/downloads))

**Steam Locomotive **

sudo apt-get install sl

  
**Power Saving**  

*   Blank screen: 15 minutes

**Canberra GTK**  
sudo apt-get install libcanberra-gtk-module  
Note: seems to resolve error "Gtk-Message: Failed to load module "canberra-gtk-module"" ([via](https://www.linuxquestions.org/questions/linux-software-2/gtk-message-failed-to-load-module-canberra-gtk-module-936168/))  
  

**Android Studio**  
[Instructions](http://iokevins.blogspot.com/2015/11/android-studio-install-instructions.html) (grew to the size of a full post)  
  
Genymotion (emulation?)  
  
**Other**  
  
sudo apt-get install pulseaudio pulseaudio-module-bluetooth pavucontrol 

sudo apt-get install bluez-tools

sudo apt-get install locate  
sudo apt-get install rfkill  
sudo apt-get install strace

sudo apt-get install airport-utils  
sudo apt-get install xclip  
sudo apt-get install tidy  
sudo apt-get install libaacs0 libbluray-bdj libbluray1

### MISTAKES

Went pretty smoothly, but always something:

*   Forgot to copy my dot files, from my home folder
*   (?)

### **LIKES/DISLIKES**

*   Liking the new handling of the [GNOME Shell](https://en.wikipedia.org/wiki/GNOME_Shell) Indicators Tray, as it now exists in the lower-left as an expandable/collapsible list, instead of a full row, at the bottom, which pops up when I move my mouse to the screen bottom
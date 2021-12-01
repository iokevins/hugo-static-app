---
title: 'Configuring Debian GNU/Linux 6.0.5 "squeeze"'
date: 2012-09-09T23:34:00.000-07:00
draft: false
tags: 
- linux
- debian
---

OK, I'm in....  
  
17:42  
  
_Install Chromium via Software Center_  

*   Select Internet > Web Browsers
*   Select Chromium > Install
*   Done; close Software Center

_Configuring Chromium_

*   Add icon to my Desktop: 

*   Applications > Internet
*   Right-select on Chromium and select "Add this launcher to Desktop"

*   Incognito mode by default:

*   sudo vim /etc/chromium-browser/default
*   add "--incognito"
*   Close

*   Run Chromium
*   Sync Chromium

*   Wrench > Options > Personal Stuff > Sync > Set Up Sync...
*   Log-in to Google Account
*   On screen Configure sync, select "Keep everything synced", then select "OK"
*   Error appears: "The sync server is busy, please try again later." x\_x
*   Chromium Version **6.0.472.**63 (59945) Built on Debian 6.0, running on Debian 6.0.5
*   about:sync

*   Authenticated null
*   Last Synced null
*   null null

*   Via this [post](http://lists.debian.org/debian-user/2012/03/msg00977.html) from Feb 2012: "The problem is that the chromium version is too old." Ah.
*   From [Wikipedia](http://en.wikipedia.org/wiki/Chromium_(web_browser)#2010): "Chrome 6 was released in both a stable and beta version on 2 September 2010 as version **6.0.472.**53" and "Chromium 23.0 was released on 9 August 2012, with the initial release version **23.0.****1231.**0." Ouch. So I have a two-year old browser.
*   Since Debian will not update Chromium except for security/severe bugs, I am stuck with version 6.

_Install Google Chrome via downloaded deb package_

*   Download Debian package from  [https://www.google.com/intl/en/chrome/browser/](https://www.google.com/intl/en/chrome/browser/)
*   System > Administration > Synaptic Package Manager

*   Error: "Failed to run /usr/sbin/synaptic as user root. Wrong password."
*   Ah, via this [post](https://answers.launchpad.net/ubuntu/+source/yelp/+question/5860), it attempts to run "su-to-root -X -c /usr/sbin/synaptic", which fails because I locked the root account
*   Hmm..."su-to-root -p "k" -X -c /usr/sbin/synaptic" returns error "Starting without administrative privileges. You will not be able to apply any changes. But you can still export the marked changes or create a download script for them."
*   It took some digging, but I discovered the [answer](http://unix.stackexchange.com/questions/47665/su-to-root-fails-when-root-user-locked): I changed the Debian menu item command from su-to-root -X -p "user" -c /usr/sbin/synaptic to gksu -S /usr/sbin/synaptic (see the link for details)

*   Cannot figure out how to install downloaded package through Synaptic Package Manager
*   Install via command line instead

*   Via this [post](http://ubuntuguide.net/update-latest-google-chrome-stable-ubuntu): 

*   sudo dpkg -i /home/k/repo/google-chrome-stable\_current\_i386.deb
*   sudo apt-get -f install , which installed libcurl3 (7.21.0-2.1+squeeze2) and libssh2-1 (1.2.6-1)

*   Applications > Internet > Google Chrome

*   It works! Version 21.0.1180.89

_Configuring Google Chrome_

*   Add icon to my Desktop: 

*   Applications > Internet
*   Right-select on Google Chrome and select "Add this launcher to Desktop"

*   Incognito mode by default:

*   Right-select on Desktop Google Chrome launcher, then select Properties
*   Add "--incognito" to the end of the text in text box "Command"
*   Close

*   Sync Google Chrome

*   Wrench > Settings > Sign In > Sign in to Chrome
*   Log-in to Google Account
*   Select button "OK, sync everything"

*   Install LastPass extension

*   Download extension [https://download.lastpass.com/lpchrome\_linux.crx](https://download.lastpass.com/lpchrome_linux.crx)
*   Hmm...Google Chrome reports message, "Extensions, apps, and user scripts can only be added from the Chrome Web Store." 
*   Wrench > Tools > Extensions
*   Search the Chrome Web Store for LastPass
*   Install the LastPass extension

*   Wrench > Tools > Extensions
*   Select "Allow in Incognito"

_Enabling NTP Support_

*   System > Administration > Time and Date
*   Select the shield icon to authenticate
*   Select pull-down list "Configuration" and choose "Keep synchronized with Internet servers"
*   Error appears: "NTP support is not installed. Please install and activate NTP support in the system to enable synchronization of your local time server with internet time servers."
*   Via this [post](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=267173): apt-get install ntp
*   Select pull-down list "Configuration" and choose "Keep synchronized with Internet servers"
*   Select time server tick.cs.unlv.edu (Las Vegas, USA) and ntp-0.cso.uiuc.edu (Illinois, USA)

_Correcting root user setup_

*   Well, shoot. It appears during installation I configured Debian with a separate root user and my user account without root privileges
*   Command sudo reports error "k is not in the sudoers file.  This incident will be reported." Heh.
*   Sudo means “substitute user do”. hmm.
*   Via this [post](http://www.linuxquestions.org/questions/debian-26/getting-rid-of-root-user-in-debian-sid-623694/#post3069559): 

*   su root
*   visudo
*   add line "yourusername    ALL=(ALL) ALL"
*   save and exit
*   exit root account
*   sudo passwd -l root (lock the root account)

_Set default editor to vim_

*   vim ~/.bashrc
*   Append line: export EDITOR="vim"

_Install vim_

*   Oy
*   apt-get install vim
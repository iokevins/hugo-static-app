---
title: 'Ubuntu Upgrade: 14.04 LTS to 17.04'
date: 2017-05-29T12:14:00.002-07:00
draft: false
tags: 
- ubuntu
- upgrade
---

Performed three release upgrades to an Ubuntu 14.04.x LTS Trusty Tahr install, on a Lenovo ThinkPad X1 Carbon, 2nd Generation (Rel 2):  
  

1.  16.04.2 LTS Xenial Xerus
2.  16.10 Yakkety Yak
3.  17.04 Zesty Zapus

The first upgrade, from 14.04.x LTS, to 16.04.2 LTS, caused the boot process to fail with the following errors:  
  

*   \[FAILED\] Load Kernel Modules ...
*   Hangs, at "Starting Show Plymouth Boot Screen"

I got to a virtual console, via Ctrl+Alt+F1, then ran sudo apt-get update && sudo apt-get dist-upgrade.

  

At this point I believe I received a variant of the following error:

> relocation error: /usr/lib/x86\_64-linux-gnu/libapt-pkg.so.5.0:  
>  symbol \_ZNKSt7\_\_cxx1112basic\_stringIcSt11char\_traitsIcESaIcEE7compareERKS4\_,  
>  version GLIBCXX\_3.4.21 not defined in file libstdc++.so.6  
>  with link time reference.  

  
I believe running "sudo apt-get install -f" or "dpkg --configure -a" allowed apt to work. After rebooting, I did a recovery boot and enabled networking.  
  
After that, it seemed like the package manager needed a later version of libstdc++. Using another device, I downloaded http://security.ubuntu.com/ubuntu/pool/main/g/gcc-5/libstdc++6\_5.4.0-6ubuntu1~16.04.4\_amd64.deb, to a thumb drive. Then I manually mounted the thumb drive on the laptop, followed by sudo dpkg -i libstdc++6\_5.4.0-6ubuntu1~16.04.4\_amd64.deb. Unfortunately, this didn't seem to work.  
  
However, this did:  
  

*   sudo add-apt-repository ppa:ubuntu-toolchain-r/test
*   sudo apt-get update && sudo apt-get -f install
*   sudo apt-get upgrade
*   sudo reboot

After the reboot, I ran sudo apt-get dist-upgrade, completing the upgrade. I think. It's a bit fuzzy.  
  
The second upgrade, from 16.04 LTS, to 16.10, I believe was uneventful.  
  
After the upgrade, I noticed some errors running sudo apt-get dist-upgrade (possibly there all the time). Namely, it couldn't update cpp because of failed dependencies.  
  
It turned out I had an newer version of gcc-6-base (possibly from repository ppa:ubuntu-toolchain-r/test) (?)  
  

*   sudo apt-get install gcc-6-base=6.2.0-5ubuntu12
*   sudo apt-get install cpp gcc
*   sudo apt-get update && sudo apt-get dist-upgrade

  
After that all was well. I think. Again, a bit fuzzy memory.  
  
Helpful commands:  
  

*   sudo rmadison -u ubuntu gcc-6-base
*   dpkg -l | grep gcc

  
Good luck!  
  
RESOURCES  
[https://wiki.ubuntu.com/Releases](https://wiki.ubuntu.com/Releases)  
[https://ubuntuforums.org/showthread.php?t=2306009](https://ubuntuforums.org/showthread.php?t=2306009)  
[https://askubuntu.com/questions/804753/i-cant-boot-after-upgrading-to-16-04-from-14-04](https://askubuntu.com/questions/804753/i-cant-boot-after-upgrading-to-16-04-from-14-04)  
[https://askubuntu.com/questions/778193/system-hangs-on-starting-show-plymouth-boot-screen](https://askubuntu.com/questions/778193/system-hangs-on-starting-show-plymouth-boot-screen)
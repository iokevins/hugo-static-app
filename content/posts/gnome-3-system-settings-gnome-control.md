---
title: 'GNOME 3 System Settings - gnome-control-center re-install'
date: 2015-09-13T13:02:00.002-07:00
draft: false
---

After manually updating libsane a few weeks ago, it seems my Debian Jessie install (stable) no longer started GNOME 3 System Settings, when I selected it:  
  

[![](/images/GNOME3SystemSettings320.png)](/images/GNOME3SystemSettings.png)

_GNOME 3 User Menu: Selecting icon "System Settings" did nothing_

  
While no error displayed after selecting the icon for "System Settings", an error did appear after I attempted to select "Wi-Fi" > "Wi-Fi Settings": (paraphrased) "gnome-control-center failed to start"  
  
Looking in /var/log/messages.1 provided more detail:  

> Sep 12 20:36:05 bucket gnome-session\[25118\]: Gjs-Message: JS LOG: error: Execution of “gnome-control-center” failed:: Failed to execute child process "gnome-control-center" (No such file or directory)

Solution: re-install gnome-control-center:  

>   
> sudo apt-get update  
> sudo apt-get install gnome-control-center 

> Swipe your right index finger across the fingerprint reader  
> Reading package lists... Done  
> Building dependency tree        
> Reading state information... Done  
> The following extra packages will be installed:  
>   colord  
> Suggested packages:  
>   libcanberra-gtk-module  
> The following NEW packages will be installed:  
>   colord gnome-control-center  
> 0 upgraded, 2 newly installed, 0 to remove and 0 not upgraded.  
> Need to get 3,604 kB of archives.  
> After this operation, 6,895 kB of additional disk space will be used.  
> Do you want to continue? \[Y/n\]  
> Get:1 http://mirrors.ocf.berkeley.edu/debian/ jessie/main colord amd64 1.2.1-1+b2 \[297 kB\]  
> Get:2 http://mirrors.ocf.berkeley.edu/debian/ jessie/main gnome-control-center amd64 1:3.14.2-3 \[3,307 kB\]  
> Fetched 3,604 kB in 34s (103 kB/s)                                              
> Selecting previously unselected package colord.  
> (Reading database ... 167964 files and directories currently installed.)  
> Preparing to unpack .../colord\_1.2.1-1+b2\_amd64.deb ...  
> Unpacking colord (1.2.1-1+b2) ...  
> Selecting previously unselected package gnome-control-center.  
> Preparing to unpack .../gnome-control-center\_1%3a3.14.2-3\_amd64.deb ...  
> Unpacking gnome-control-center (1:3.14.2-3) ...  
> Processing triggers for dbus (1.8.20-0+deb8u1) ...  
> Processing triggers for man-db (2.7.0.2-5) ...  
> Processing triggers for libglib2.0-0:amd64 (2.42.1-1) ...  
> Processing triggers for desktop-file-utils (0.22-1) ...  
> Processing triggers for gnome-menus (3.13.3-6) ...  
> Processing triggers for mime-support (3.58) ...  
> Processing triggers for menu (2.1.47) ...  
> Setting up colord (1.2.1-1+b2) ...  
> Setting up gnome-control-center (1:3.14.2-3) ...  
> Processing triggers for menu (2.1.47) ...  
> k@bucket:~$ ls

Done--everything works as expected, now.
---
### Comments:
#### How to resolve this ? apt-get install gnome-contr...
[Nina](https://www.blogger.com/profile/01129465650793748948 "noreply@blogger.com") - <time datetime="2016-04-21T23:55:57.833-07:00">Apr 4, 2016</time>

How to resolve this ?  
  
apt-get install gnome-control-center  
Reading package lists... Done  
Building dependency tree  
Reading state information... Done  
Some packages could not be installed. This may mean that you have  
requested an impossible situation or if you are using the unstable  
distribution that some required packages have not yet been created  
or been moved out of Incoming.  
The following information may help to resolve the situation:  
  
The following packages have unmet dependencies:  
gnome-control-center : Depends: libcheese-gtk25 (>= 3.18.0) but it is not going to be installed  
Depends: libcheese8 (>= 3.18.0) but it is not going to be installed  
E: Unable to correct problems, you have held broken packages.
<hr />
#### Hello, please see if this helps: https://askubunt...
[iokevins](https://www.blogger.com/profile/17049497132104803385 "noreply@blogger.com") - <time datetime="2016-04-22T12:14:35.442-07:00">Apr 5, 2016</time>

Hello, please see if this helps:  
  
https://askubuntu.com/questions/706164/cant-launch-system-settings-on-ubuntu-gnome-15-10
<hr />

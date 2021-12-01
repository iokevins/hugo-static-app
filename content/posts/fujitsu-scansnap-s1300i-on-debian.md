---
title: 'Fujitsu ScanSnap S1300i on Debian Jessie (Stable) GNU/Linux'
date: 2015-08-09T16:16:00.000-07:00
draft: false
tags: 
- linux
- debian
---

I purchased a Fujitsu ScanSnap S1300i and wanted to use it, on Debian GNU/Linux Jessie (stable).  
  
This documents my own experience with getting it to work, on a Lenovo ThinkPad X201 laptop.  
**TL;DR**  
Debian Jessie (Stable) ships with an older version of SANE. To support the Fujitsu ScanSnap S1300i, download, compile, and install SANE from source.  
  
**OVERVIEW**  
Scanner Access Now Easy (SANE) represents a commonly used GNU/Linux package API, which provides "standardized access to any raster image scanner hardware." ([via](https://en.wikipedia.org/wiki/Scanner_Access_Now_Easy))  
  
Debian Jessie packages SANE into frontend and backend components:  

1.  [sane](https://packages.debian.org/jessie/sane) - frontend packages, for the user-interface (for example, xscanimage, scanadf, xcam)
2.  [libsane](https://packages.debian.org/jessie/libsane) - backend packages, for individual scanner support (for example, the Fujitsu ScanSnap S1300i)

Debian Jessie (stable) seems to [ship](https://packages.debian.org/search?keywords=libsane) with the following SANE packages installed:  
  
$ dpkg -l | grep sane  
ii  libsane:amd64         1.0.24-8    amd64 API library for scanners  
ii  libsane-common        1.0.24-8    all   API library for scanners -- documentation and support files  
ii  libsane-dev           1.0.24-8    amd64 API development library for scanners \[development files\]  
ii  libsane-extras:amd64  1.0.22.3    amd64 API library for scanners -- extra backends  
ii  libsane-extras-common 1.0.22.3    amd64 API library for scanners -- documentation and support files  
ii  libsane-extras-dev    1.0.22.3    amd64 API development library for scanners \[development files\]  
ii  libsane-hpaio         3.14.6-1+b2 amd64 HP SANE backend for multi-function peripherals  
ii  libsane-perl          0.05-2+b2   amd64 Perl bindings for the SANE (Scanner Access Now Easy) Project  
ii  sane                  1.0.14-9    amd64 scanner graphical frontends  
ii  sane-utils            1.0.24-8    amd64 API library for scanners -- utilities  

  

Unfortunately, the shipped version of libsane 1.0.24-8 does **not** seem to properly handle the Fujitsu ScanSnap S1300i.  
  
**FIRST ATTEMPTS**  
Following the [advice](http://www.openfusion.net/linux/scansnap_1300i) of Gavin Carr, from September 2014 (note: Gavin used Centos 6), I first attempted the following steps.  

> $ sudo sane-find-scanner  
> found USB scanner (vendor=0x04c5 \[FUJITSU\], product=0x128d \[ScanSnap S1300i\]) at libusb:001:009 

> $ sudo scanimage -L  
> device \`v4l:/dev/video0' is a Noname Integrated Camera virtual device

Note: The results of running scanimage mean Debian did not find the device.

  

**INITIAL WORKAROUNDS**

The shipped version of libsane does not seem to currently include support for the Fujitsu ScanSnap S1300i. That is, Debian does not include the required firmware and configuration lines for it.  
  
Happily, these two steps seem pretty straightforward.  
  
_Install firmware file_  
Copy firmware file [1300i\_0D12.nal](http://www.openfusion.net/public/files/1300i_0D12.nal) (hat tip, to Gavin Carr, for providing it along with his instruction steps) to folder /usr/share/sane/epjitsu :

> $ sudo mkdir -p /usr/share/sane/epjitsu/  
> $ cd /usr/share/sane/epjitsu/ && sudo wget http://www.openfusion.net/public/files/1300i\_0D12.nal

_Update configuration file_  
Update configuration file /etc/sane.d/epjitsu.conf , adding these three lines:

> \# Fujitsu S1300i  
> firmware /usr/share/sane/epjitsu/1300i\_0D12.nal  
> usb 0x04c5 0x128d

_Retest with scanimage_  
After doing these two steps, scanimage finds the scanner!

> $ sudo scanimage -L  
> device \`v4l:/dev/video0' is a Noname Integrated Camera virtual device  
> device \`epjitsu:libusb:001:009' is a FUJITSU ScanSnap S1300i scanner

**SECOND ATTEMPTS**  
_gscan2pdf_  
Install and run frontend scanner GUI **gscan2pdf** :

> $ sudo apt-get install gscan2pdf  
> $ sudo gscan2pdf

However, after selecting the scanner, attempts to scan meet with error "Error during device I/O". x\_x

  
_scanimage_  
Additionally, I experienced similar errors, when running **scanimage**:  

> $ sudo scanimage -L  
> device \`v4l:/dev/video0' is a Noname Integrated Camera virtual device  
> device \`epjitsu:libusb:001:008' is a FUJITSU ScanSnap S1300i scanner  
> $ sudo scanimage --test -d 'epjitsu:libusb:001:008'  
> scanimage: sane\_start: Error during device I/O

Note: At this point, I had [set environment variables](http://lists.alioth.debian.org/pipermail/sane-devel/2015-February/033080.html):

> $ env | grep SANE  
> SANE\_DEBUG\_SANEI\_USB=128 ([note](http://manpages.ubuntu.com/manpages/saucy/man5/sane-usb.5.html): "a value of 128 requests all debug output to be printed.")  
> SANE\_DEBUG\_FUJITSU=35 ([note](http://www.sane-project.org/man/sane-fujitsu.5.html): "enables debugging output to stderr...useless noise")

**FURTHER WORKAROUND ATTEMPTS**

It seems, the shipped version of libsane, 1.0.24-8, has a few bugs. Per [SANE developer discussions](https://www.google.com/search?q=site%3Alists.alioth.debian.org%2Fpipermail%2Fsane-devel%2F+1300i), it appears developers subsequently have resolved the bugs.  
  
I first tried, unsuccessfully, to [add developer Rolf's repository](http://lists.alioth.debian.org/pipermail/sane-devel/2015-February/033079.html). However, when I attempted to pull in updates, "apt-get update" provided an error, which makes sense, given he provides Ubuntu support, not Debian:  

> $ sudo apt-get install software-properties-common (note: this provides "add-apt-repository")  
> $ sudo add-apt-repository ppa:rolfbensch/sane-git  
> You are about to add the following PPA to your system:  
>  Ubuntu SANE packages from SANE daily git snapshots (http://www.sane-project.org/snapshots/) or cloned from git (http://anonscm.debian.org/gitweb/?p=sane/sane-backends.git;a=summary) if SANE daily git snapshot isn't available on the website.  
> Unchanged SANE daily git snapshots are ignored!  
> Please send scanner related questions to the SANE mailing list <email address hidden>.  
>  More info: https://launchpad.net/~rolfbensch/+archive/ubuntu/sane-git  
> Press \[ENTER\] to continue or ctrl-c to cancel adding it  
> gpg: keyring \`/tmp/tmp069\_7hv9/secring.gpg' created  
> gpg: keyring \`/tmp/tmp069\_7hv9/pubring.gpg' created  
> gpg: requesting key B7CC8701 from hkp server keyserver.ubuntu.com  
> gpg: /tmp/tmp069\_7hv9/trustdb.gpg: trustdb created  
> gpg: key B7CC8701: public key "Launchpad PPA for Rolf Bensch" imported  
> gpg: Total number processed: 1  
> gpg:               imported: 1  (RSA: 1)  
> OK  
> $ sudo apt-get update  
> ... \*snip\* ...  
> Err http://ppa.launchpad.net jessie/main amd64 Packages  404  Not FoundIgn http://ppa.launchpad.net jessie/main Translation-en\_US  
> Ign http://ppa.launchpad.net jessie/main Translation-en  
> Fetched 127 kB in 3s (38.4 kB/s)  
> W: Failed to fetch http://ppa.launchpad.net/rolfbensch/sane-git/ubuntu/dists/jessie/main/binary-amd64/Packages  404  Not FoundE: Some index files failed to download. They have been ignored, or old ones used instead.

Some [reading](http://www.webupd8.org/2014/10/how-to-add-launchpad-ppas-in-debian-via.html) seems to imply this represents an error with attempting to pull Ubuntu updates to a Debian system, which the list post, above, did not immediately make clear. Note: "add-apt-repository" seems to represent an Ubuntu utility.

  

So, this fails because attempting to lookup Debian system packages on an Ubuntu repository represents a semi-sketchy thing to do. It has risks.

  

As a test, I did the following:

> $ sudo vim /etc/apt/sources.list.d/rolfbensch-sane-git-jessie.list 

> from: 

> \# deb http://ppa.launchpad.net/rolfbensch/sane-git/ubuntu jessie main 

> to the following, replacing "jessie" with "trusty":

> deb http://ppa.launchpad.net/rolfbensch/sane-git/ubuntu trusty main

 Running apt-get update now works:  

> ... \*snip\* ...  
> Get:14 http://ppa.launchpad.net trusty/main Translation-en \[1,220 B\]                                        
> ... \*snip\* ...

However, apt-get upgrade fails:  

> $ sudo apt-get upgrade  
> Reading package lists... Done  
> Building dependency tree      
> Reading state information... Done  
> Calculating upgrade... Done  
> The following packages have been kept back:  libsane libsane-common libsane-dev  
> The following packages will be upgraded:  
>   libsvn1 sane-utils subversion  
> 3 upgraded, 0 newly installed, 0 to remove and 3 not upgraded.  
> Need to get 2,187 kB of archives.  
> After this operation, 131 kB disk space will be freed.  
> Do you want to continue? \[Y/n\] n  
> Abort.

I next attempted to install just libsane, however, I received an error, and aborted:  

> $ sudo apt-get install libsane  
> Reading package lists... Done  
> Building dependency tree      
> Reading state information... Done  
> Some packages could not be installed. This may mean that you have  
> requested an impossible situation or if you are using the unstable  
> distribution that some required packages have not yet been created  
> or been moved out of Incoming.  
> The following information may help to resolve the situation:  
> The following packages have unmet dependencies: libsane : Depends: libjpeg8 (>= 8c) but it is not installable  
> E: Unable to correct problems, you have held broken packages.

No thanks! Note: I received the same errors with "precise" and "vivid". Some reading suggested running "dist-upgrade" but I am, at the very least, smart enough to not go nuclear to resolve this, yet.

  

So, [backed out](http://unix.stackexchange.com/questions/60595/how-to-undo-sudo-add-apt-repository) the change and removed the repository. Will have to fine something a bit less sketchy.

> $ rm /etc/apt/sources.list.d/rolfbensch-sane-git-jessie.list\*  
> $ sudo apt-key list  
> $ sudo apt-key del B7CC8701

Backports? It seems Debian Jessie currently [does not have any backports, for libsane](https://packages.debian.org/search?suite=jessie-backports&keywords=libsane):

> $ sudo vim /etc/apt/sources.list  
> Add "deb http://http.debian.net/debian jessie-backports main"  
> $ sudo apt-get -t jessie-backports install libsane  
> Reading package lists... Done  
> Building dependency tree  
> Reading state information... Done  
> libsane is already the newest version.  
> 0 upgraded, 0 newly installed, 0 to remove and 38 not upgraded.

So. dmesg reports the following:

> $ dmesg  
> \[18601.324625\] usb 1-1.2: new high-speed USB device number 9 using ehci-pci  
> \[18601.419949\] usb 1-1.2: New USB device found, idVendor=04c5, idProduct=128d  
> \[18601.419955\] usb 1-1.2: New USB device strings: Mfr=1, Product=2, SerialNumber=0  
> \[18601.419959\] usb 1-1.2: Product: ScanSnap S1300i  
> \[18601.419961\] usb 1-1.2: Manufacturer: FUJITSU

Note: some developers have suggested [EHCI](https://en.wikipedia.org/wiki/Host_controller_interface_(USB,_Firewire)#Enhanced_Host_Controller_Interface) versus [xHCI](https://en.wikipedia.org/wiki/Extensible_Host_Controller_Interface) (that is, USB 3.0) might represent the source of the problem. This shows I am using EHCI.

  
COMPILING SANE FROM SOURCE  
Uninstall SANE:  
[http://installion.co.uk/ubuntu/vivid/universe/s/sane/uninstall/index.html](http://installion.co.uk/ubuntu/vivid/universe/s/sane/uninstall/index.html)  
  
Compile SANE from source:  
[https://help.ubuntu.com/community/CompileSaneFromSource](https://help.ubuntu.com/community/CompileSaneFromSource)  
  
The Debian [build logs](https://buildd.debian.org/status/logs.php?pkg=sane-backends&arch=amd64) showed this configure command:  

> ./configure --host=x86\_64-linux-gnu --build=x86\_64-linux-gnu \\  
> \--prefix=/usr \\  
> \--libdir=\\${prefix}/lib/x86\_64-linux-gnu \\  
> \--sysconfdir=/etc \\  
> \--localstatedir=/var \\  
> \--datadir=\\${prefix}/share \\  
> \--mandir=\\${prefix}/share/man \\  
> \--with-docdir=\\${prefix}/share/doc/libsane \\  
> \--with-snmp=no \\  
> \--disable-locking \\  
> \--enable-static \\  
> \--enable-pthread \\  
> \--with-gphoto2 \\  
> \--enable-translations \\  
> \--enable-avahi \\  
> \--enable-libusb\_1\_0 \\  
> \--enable-pnm-backend \\  
> \--without-v4l

make  
sudo make install  
  
SUCCESS!  
gscan2pdf now successfully scans the document.  
  

  

LINKS  
[https://en.wikipedia.org/wiki/Scanner\_Access\_Now\_Easy](https://en.wikipedia.org/wiki/Scanner_Access_Now_Easy)

[http://www.openfusion.net/linux/scansnap\_1300i](http://www.openfusion.net/linux/scansnap_1300i)

[http://lists.alioth.debian.org/pipermail/sane-devel/2015-February/033079.html](http://lists.alioth.debian.org/pipermail/sane-devel/2015-February/033079.html)

[http://unix.stackexchange.com/questions/45879/how-to-add-repository-from-shell-in-debian](http://unix.stackexchange.com/questions/45879/how-to-add-repository-from-shell-in-debian)

[https://launchpad.net/~rolfbensch/+archive/ubuntu/sane-git](https://launchpad.net/~rolfbensch/+archive/ubuntu/sane-git)  
[https://packages.debian.org/jessie/libsane](https://packages.debian.org/jessie/libsane)  
[http://www.sane-project.org/](http://www.sane-project.org/)  
[http://www.webupd8.org/2014/10/how-to-add-launchpad-ppas-in-debian-via.html](http://www.webupd8.org/2014/10/how-to-add-launchpad-ppas-in-debian-via.html)  
[https://bugs.debian.org/cgi-bin/pkgreport.cgi?src=sane-backends&repeatmerged=yes](https://bugs.debian.org/cgi-bin/pkgreport.cgi?src=sane-backends&repeatmerged=yes)  
[https://qa.debian.org/developer.php?login=debian%40jff-webhosting.net](https://qa.debian.org/developer.php?login=debian%40jff-webhosting.net)  
[http://installion.co.uk/ubuntu/vivid/universe/s/sane/uninstall/index.html](http://installion.co.uk/ubuntu/vivid/universe/s/sane/uninstall/index.html)  
[https://buildd.debian.org/status/logs.php?pkg=sane-backends&arch=amd64](https://buildd.debian.org/status/logs.php?pkg=sane-backends&arch=amd64)
---
### Comments:
#### Can you scan to Evernote under Linux?
[Unknown](https://www.blogger.com/profile/05074707421001037577 "noreply@blogger.com") - <time datetime="2016-08-15T23:48:31.021-07:00">Aug 1, 2016</time>

Can you scan to Evernote under Linux?
<hr />
#### I don't use Evernote, at the current time, but...
[iokevins](https://www.blogger.com/profile/17049497132104803385 "noreply@blogger.com") - <time datetime="2016-08-16T05:55:02.829-07:00">Aug 2, 2016</time>

I don't use Evernote, at the current time, but utility gscan2pdf might allow sending scans to evernote, via the email function. Please let me know, if you find out. : )
<hr />
#### I see this post is for the s1300i but it ranks up ...
[PuffinBlue](https://www.blogger.com/profile/08239459920296315754 "noreply@blogger.com") - <time datetime="2016-10-10T05:24:47.173-07:00">Oct 1, 2016</time>

I see this post is for the s1300i but it ranks up there in Google for the plain old s1300 too so I thought I'd link the post below which has the drivers for the s1300 too:  
  
http://josharcher.uk/code/install-scansnap-s1300-drivers-linux/  
  
It's also got the drivers for the s300 if you need them.  
  
Hope that helps someone...
<hr />

---
title: 'GeneTorrent - Building release 3.8.7 on Debian Wheezy stable+backports system'
date: 2015-02-18T23:10:00.000-08:00
draft: false
tags: 
- linux
- debian
---

BACKGROUND  
  
The University of Californa at Santa Cruz [Genomics Institute](http://genomics.soe.ucsc.edu/), established in 2014, connects [many efforts](https://genomics.soe.ucsc.edu/projects), including the [UC Santa Cruz Cancer Genomics Hub](https://cghub.ucsc.edu/), launched in 2012:  

> The Cancer Genomics Hub (CGHub) is a central repository for the genomics information for three different National Cancer Institute (NCI) programs, including The Cancer Genomics Atlas (TCGA). In addition to providing a repository, CGHub supports the establishment of standards and application programming interfaces (APIs), and provides support to end users.

_An aside: Dawn says she thinks of the 1990's-era television series [MST3K](https://en.wikipedia.org/wiki/Mystery_Science_Theater_3000) when she hears the name "Genomics Institute," because the name sounds like [Gizmonic Institute](http://mst3k.wikia.com/wiki/Gizmonic_Institute), the fictitious cover organization of the show's antagonists. They send bad movies to the show's protagonist, Joel Robinson, __as part of a psychological experiment__. Note: Of course, UC Santa Cruz Genomics Institute staff do __not compare, __to my knowledge, to the antagonists in MST3K! : o )_  
CGHub staff provide "binary and source distributions of the [GeneTorrent client software](https://cghub.ucsc.edu/software/downloads.html) for downloading sequence data from CGHub's repository. The distribution contains two main programs: gtdownload and cgquery." Note: CGHub staff have a few other packages [available](https://bitbucket.org/cghub) at their bitbucket repository.  
  
From my very limited, outsider experience with the project, it seems UCSC CGHub staff contracted with a private vendor, [Annai Systems, Inc.](http://www.annaisystems.com/), to obtain the GeneTorrent client software and the [other architectural components](http://www.annaisystems.com/wp-content/uploads/2014/09/Annai-White-Paper_Oct-2013.pdf) needed to store and transfer the terabytes (possibly petabytes, now) of cancer genome data.  
  
From a [2012 press release](http://www.prnewswire.com/news-releases/annai-systems-provides-network-engine-to-uc-santa-cruz-for-cancer-genomics-hub-149676225.html), it appears UCSC CGHub licensed technology from Annai Systems Inc. to support the acquisition of a "new 5-petabyte-capacity data repository." The press release indicates the UCSC CGHub deployment represented the first release of the Annai Systems, Inc. architecture. Dr. David Haussler, Professor of Biomolecular Engineering at UCSC, who leads the CGHub project, stated, "Annai has been an exceptional partner in the development of CGHub." This seems to imply UCSC CGHub staff paid Annai Systems staff to create and maintain the system, at least initially, in combination with some on-campus dedicated operational support. From [commit logs](https://bitbucket.org/cghub/genetorrent/commits/all), it appears CGHub staff maintain GeneTorrent. Less likely, to me, they may only apply patches from the vendor. (?)  
  
For what it's worth, Annai Systems staff seem to have sub-contracted some or most of the development work, at least on GeneTorrent, to private vendor [Cardinal Peak](http://www.cardinalpeak.com/) (for example, see GeneTorrent repository file headers ./[README](https://bitbucket.org/cghub/genetorrent/src/3928077f157144fc5f356d38b5aabfc440821d1c/README?at=rm4943-binary-dist-bundles-all-deps), which states, "Created under contract by Cardinal Peak, LLC.  www.cardinalpeak.com"--the header reads "Copyright (c) 2011-2012, Annai Systems, Inc.")  
  
Annai Systems, in a [2013 whitepaper](http://www.annaisystems.com/wp-content/uploads/2014/09/Annai-White-Paper_Oct-2013.pdf), describes GeneTorrent as follows:  

> "Whole genome sequence data files range from several hundred gigabytes to over one terabyte in size. GeneTorrent enables accelerated transfers of terabyte-scale data. It employs a proprietary variant of the popular BitTorrent algorithm to securely transfer files at speeds limited only by the base network bandwidth. 

> **Technical Specifications** 

> GeneTorrent’s key functionality is as follows:  
> 
> *   High-fidelity parallel file transfer at up to multi-Gbits/sec (speeds as high as 200 Mbps are routinely achieved) 

> *   Highly resilient to in-network and computing failures with automatic recovery

> *   Highly secure 256-bit encrypted file transfer"

Whitepaper notwithstanding, it seems to me the GeneTorrent client's ability to operate within the larger ecosystem of the Annai Systems architecture represents the main selling point of the client. It does seem they have extended libtorrent in some minor ways, but I have not had time to investigate fully.  
  
GENETORRENT INTERNALS  
  
The source code reveals GeneTorrent version 3.8.7 relies primarily on release 0.16 of package [libtorrent](http://www.libtorrent.org/), which seems to represent the version [extant](http://code.google.com/p/libtorrent/source/detail?r=6617&path=/trunk/ChangeLog) in March 2012, during initial development:  

> "libtorrent is a C++ library that aims to be a good alternative to all the other bittorrent implementations around. It is a library and not a full featured client, although it comes with a working example client."

Currently at release 1.0.3, [libtorrent](https://en.wikipedia.org/wiki/Libtorrent) originates from Swedish programmer [Arvid Norberg](https://www.linkedin.com/pub/arvid-norberg/2/977/ab8), which also explains the origin of the word rasterbar, which I noticed frequently while building GeneTorrent. Rasterbar represents the name of a Swedish company, [Rasterbar Software](http://www.rasterbar.com/), which was founded in [Umeå, Sweden](https://en.wikipedia.org/wiki/Ume%C3%A5). This further explains the shout-out of libtorrent developers to [Umeå University](http://www.umu.se/english) for "providing development and test hardware" for the libtorrent project.  
  
The source code also relies on project [xqilla](http://xqilla.sourceforge.net/HomePage) (which requires [xerces-c](http://xerces.apache.org/xerces-c/)) for XML parsing, [OpenSSL](https://www.openssl.org/) for encryption, [libcurl](http://curl.haxx.se/libcurl/) for file transfer, and [boost](http://www.boost.org/) (used for building libtorrent and GeneTorrent).  
  
BUILDING GENETORRENT  
  
First, install prerequisite packages:  

*   autoconf
*   devscripts
*   gettext
*   libboost-all-dev
*   sudo apt-get install libp11-kit0/wheezy (note: "/wheezy" overrides installing from backports repository, to prepare the way to install libcurl4-openssl-dev)
*   libcurl4-openssl-dev (note: override backports, as above, first)
*   libtool
*   libxerces-c-dev
*   libxqilla-dev
*   lsb
*   python-openssl
*   xqilla

Second, download the source:  
  
Go [here](https://bitbucket.org/cghub/genetorrent/downloads), then select link "Download repository" ([currently](https://bitbucket.org/cghub/genetorrent/get/476d7bd44985.zip); all [versions](https://cghub.ucsc.edu/software/downloads/GeneTorrent/))  
  
Optionally (if not the first go-round): rm -rf cghub-genetorrent-476d7bd44985  
unzip cghub-genetorrent-476d7bd44985.zip  
cd cghub-genetorrent-476d7bd44985  
  
Third, customize for Debian Wheezy (7.8), as the source code currently seems to only support Debian Squeeze (6.0.6), out-of-the-box:  
  
\# Make Wheezy dpkg the same as squeeze...  
ln -s squeeze dpkg/wheezy  
  

\# grab all ./dpkg/Makefile.am lines with squeeze, modify them to wheezy, fix the spacing of backslashes,

\# then insert the modified lines back into ./dpkg/Makefile.am

export \_cghub\_file=./dpkg/Makefile.am && \\

export \_cghub\_text=$(grep squeeze ./dpkg/Makefile.am | sed 's/squeeze/wheezy/g;s/\\\\/ \\\\/g') && \\

awk '/squeeze/ && !done { print ENVIRON\["\_cghub\_text"\] ; done=1;}; 1;' $\_cghub\_file > ${\_cghub\_file}.new && \\

mv ${\_cghub\_file}.new $\_cghub\_file && \\

unset \_cghub\_text \_cghub\_file

  

\# NOTE: Manually patch ./Makefile.am as follows ... too complicated to script, for now

\# line numbers precede the actual line contents

\# Note: the name--in this case, wheezy--must match the results of command "lsb\_release -cs"

128 .PHONY: deb deb-builder deb-trusty deb-saucy deb-raring deb-precise deb-quantal deb-oneiric deb-lucid deb-squeeze deb-wheezy

161 

162 # Debian wheezy (7.8)

163 deb-wheezy:

164   $(MAKE) DEB\_DISTRO\_TAG=debian${DEB\_PACKAGE\_VER}-${DEB\_RELEASE} deb-builder

  

\# Rebuild Makefile.in ....  
./autoregen.sh  
  
Fourth, start building dependencies:  
  
\# Build dependencies  
deps/boost/buildGeneTorrentBoost.sh && \\  
deps/openssl/buildGeneTorrentOpenSSL.sh && \\  
deps/xerces-c/buildGeneTorrentXerces-C.sh && \\  
deps/xqilla/buildGeneTorrentXQilla.sh  
  
Fifth, fix what seems like a non-git bug in the configure script, which causes configure to not generate file src/gt\_scm\_rev.h:  
  
\# Fix missing header file src/gt\_scm\_rev.h (?)  
\# The GeneTorrent 3.8.5 release's NEWS file, dated March, 2014, [states](https://bitbucket.org/cghub/genetorrent/src/3928077f157144fc5f356d38b5aabfc440821d1c/NEWS?at=rm4943-binary-dist-bundles-all-deps):  
\# "Generate gt\_scm\_rev.h during configure instead of make. That way it is included in the source  
# distribution, make clean doesn't remove it, make install doesn't skip its creation."  
\# However, configure seems to fail and not create it (?) This needs verification.  
\# First, touch .git file, per scm-rev-update, which requires it to proceed to generating the file  
\# Second, re-run scm-rev-update to produce the file  
\# Possibly, this validation step prevents the creation of the file in non-git source builds (?), causing  
\# the error (?)  
touch ./scripts/.git  
./scripts/scm-rev-update  
  
Sixth, configure with dependencies (optionally, with debug/verbose):  
  
\# Configure  
\# Note: To enable verbose logging, configure with --enable-logging=verbose  
\# Note: To create a debug build, configure with --enable-debug --enable-logging=verbose  
./configure --with-boost=$PWD/deps/boost --with-openssl=$PWD/deps/openssl --with-xerces=$PWD/deps/xerces-c --with-xqilla=$PWD/deps/xqilla  

  

Seventh, build the Debian packages (optionally, make install?):

  

\# Build  
\# Note: make deb seems to represent a wrapper around make dist  
make deb  
  
Done, hopefully, without errors.  
  
TO-DO  

  

Try running gtdownload and cgquery and gtupload and cgsubmit programs.

  

NOTES - LIBCURL4-OPENSSL-DEV INSTALL ERROR  
  
I got to a certain point and saw this configure error:  

> checking curl/curl.h usability... no  
> checking curl/curl.h presence... no  
> checking for curl/curl.h... no  
> configure: error: curl headers required but not found

So, who [provides curl.h](https://packages.debian.org/search?searchon=contents&keywords=curl.h)?  

> File Packages  
> /usr/include/curl/curl.h libcurl4-gnutls-dev, libcurl4-nss-dev, libcurl4-openssl-dev  
> /usr/include/discover/curl.h libdiscover-dev  
> /usr/include/lua5.1/lua-curl.h lua-curl-dev  
> /usr/include/rheolef/curl.h librheolef-dev \[not armel, armhf\]  
> /usr/include/rheolef/s\_curl.h librheolef-dev \[not armel, armhf\]Attempts to install libcurl4-gnutls-dev, libcurl4-nss-dev, or libcurl4-openssl-dev results in errors:

Attempts to install libcurl4-openssl-dev:  

> The following packages have unmet dependencies:  
> libcurl4-openssl-dev : Depends: librtmp-dev but it is not going to be installed  
> Conflicts: libcurl-dev  
> Conflicts: libcurl4-gnutls-dev but 7.26.0-1+wheezy12 is to be installed  
> Conflicts: libcurl4-nss-dev but 7.26.0-1+wheezy12 is to be installed  
> E: Unable to correct problems, you have held broken packages.

Seems like they all depend on package librtmp-dev. Drilling down into this:  

> sudo apt-get install librtmp-dev  
> The following packages have unmet dependencies:  
> librtmp-dev : Depends: libgnutls-dev but it is not going to be installed  
> E: Unable to correct problems, you have held broken packages.

Uh-oh...going further...  

> sudo apt-get install libgnutls-dev  
> The following packages have unmet dependencies:  
> libgnutls-dev : Depends: libp11-kit-dev (>= 0.4) but it is not going to be installed  
> E: Unable to correct problems, you have held broken packages.

Erm...almost there (?)  

> sudo apt-get install libp11-kit-dev  
> The following packages have unmet dependencies:  
> libp11-kit-dev : Depends: libp11-kit0 (= 0.12-3) but 0.20.7-1~bpo70+1 is to be installed  
> E: Unable to correct problems, you have held broken packages.

So...it has come to this. libp11-kit-dev depends on libp11-kit0. What? : o \\ Let's dig a bit more:  

> sudo apt-cache policy libp11-kit0  
> libp11-kit0:  
> Installed: 0.20.7-1~bpo70+1  
> Candidate: 0.20.7-1~bpo70+1  
> Version table:  
> \*\*\* 0.20.7-1~bpo70+1 0  
> 100 http://ftp.us.debian.org/debian/ wheezy-backports/main amd64 Packages  
> 100 /var/lib/dpkg/status  
> 0.12-3 0  
> 500 http://ftp.us.debian.org/debian/ wheezy/main amd64 Packages

Wheezy backports provides a later version...ah! So, learning something new, I have to tell apt-get to use wheezy target instead of backports:  

> sudo apt-get install libp11-kit0/wheezy

This works! Now "sudo apt-get install libcurl4-openssl-dev" succeeds. Ta-da. : o )  
  
NOTES - GT\_SCM\_REV.H  
  
Running make fails.  

> libtool: compile: g++ -DHAVE\_CONFIG\_H -I. -I/usr/include -I/usr/include -I/usr/include/xercesc -I/usr/include -DGT\_RESOURCEDIR=\\"/usr/local/share/GeneTorrent\\" -DGT\_BUILD\_NUMBER=\\"undefined\\" -DGT\_BUILD\_TYPE=\\"undefined\\" -DGT\_BUILD\_TARGET=\\"undefined\\" -DTORRENT\_CALLBACK\_LOGGER -DTORRENT\_MINIMAL\_LOGGING -DTORRENT\_USE\_OPENSSL -DTORRENT\_DISABLE\_GEO\_IP -DTORRENT\_DISABLE\_DHT -DBOOST\_ASIO\_HASH\_MAP\_BUCKETS=1021 -DBOOST\_EXCEPTION\_DISABLE -DBOOST\_ASIO\_ENABLE\_CANCELIO -DTORRENT\_LINKING\_SHARED -I/usr/local/include/GeneTorrent -I/usr/local/include/GeneTorrent/libtorrent -I../libtorrent/include -g -O2 -Wall -MT libgenetorrent\_la-gtBaseOpts.lo -MD -MP -MF .deps/libgenetorrent\_la-gtBaseOpts.Tpo -c gtBaseOpts.cpp -fPIC -DPIC -o .libs/libgenetorrent\_la-gtBaseOpts.o  
> gtBaseOpts.cpp:41:24: fatal error: gt\_scm\_rev.h: No such file or directorycompilation terminated.  
> make\[2\]: \*\*\* \[libgenetorrent\_la-gtBaseOpts.lo\] Error 1

It can't find header file gt\_scm\_rev.h.  
  
Touch .git file in top directory...expected by ./scripts/scm-rev-update, line 11: 

> 11 if \[ -d .git -o -f .git \] # in git >= 1.8, .git is a file if the working copy is a submodule

This should probably handle source code builds, in addition to git source code builds.

  

QUESTIONS  

*   Do CGHub maintainers eventually foresee providing 64-bit Microsoft Windows binaries?
*   ./dpkg/squeeze/control lists Maintainer: Matt Lupfer <mlupfer@cardinalpeak.com>, but he no longer works there
*   make deb triggers re-downloading of boost package, even after running deps/boost/buildGeneTorrentBoost.sh, which downloads the tarball (?)
*   Other (?)

RANDOM OTHER ERRORS

A bunch of random errors & warnings from the build process (?) Not sure whether worthwhile to review, or not....

> 10287 ../configure: line 20168: #: command not found  
> 10348 ./config.status: line 2384: scripts/scm-rev-update: No such file or directory  
> 10516 sed: can't read include/libtorrent/version.hpp: No such file or directory  
> 10713 ../../../libtorrent/src/rss.cpp:421:3: warning: invalid access to non-static data member 'libtorrent::feed::m\_title'  of NULL object \[-Winvalid-offsetof      \]  
> 10714 ../../../libtorrent/src/rss.cpp:421:3: warning: (perhaps the 'offsetof' macro was used incorrectly) \[-Winvalid-offsetof\]  
> 10715 ../../../libtorrent/src/rss.cpp:422:3: warning: invalid access to non-static data member 'libtorrent::feed::m\_description'  of NULL object \[-Winvalid-of      fsetof\]  
> 10716 ../../../libtorrent/src/rss.cpp:422:3: warning: (perhaps the 'offsetof' macro was used incorrectly) \[-Winvalid-offsetof\]  
> 10717 ../../../libtorrent/src/rss.cpp:423:3: warning: invalid access to non-static data member 'libtorrent::feed::m\_last\_attempt'  of NULL object \[-Winvalid-o      ffsetof\]  
> 10718 ../../../libtorrent/src/rss.cpp:423:3: warning: (perhaps the 'offsetof' macro was used incorrectly) \[-Winvalid-offsetof\]  
> 10719 ../../../libtorrent/src/rss.cpp:424:3: warning: invalid access to non-static data member 'libtorrent::feed::m\_last\_update'  of NULL object \[-Winvalid-of      fsetof\]  
> 10720 ../../../libtorrent/src/rss.cpp:424:3: warning: (perhaps the 'offsetof' macro was used incorrectly) \[-Winvalid-offsetof\]  
> 10725 ../../../libtorrent/src/session\_impl.cpp:519:3: warning: invalid access to non-static data member 'libtorrent::aux::session\_impl::m\_settings'  of NULL o      bject \[-Winvalid-offsetof\]  
> 10726 ../../../libtorrent/src/session\_impl.cpp:519:3: warning: (perhaps the 'offsetof' macro was used incorrectly) \[-Winvalid-offsetof\]  
> 10727 ../../../libtorrent/src/session\_impl.cpp:523:3: warning: invalid access to non-static data member 'libtorrent::aux::session\_impl::m\_proxy'  of NULL obje      ct \[-Winvalid-offsetof\]  
> 10728 ../../../libtorrent/src/session\_impl.cpp:523:3: warning: (perhaps the 'offsetof' macro was used incorrectly) \[-Winvalid-offsetof\]  
> 10729 ../../../libtorrent/src/session\_impl.cpp:528:3: warning: invalid access to non-static data member 'libtorrent::aux::session\_impl::m\_pe\_settings'  of NUL      L object \[-Winvalid-offsetof\]  
> 10730 ../../../libtorrent/src/session\_impl.cpp:528:3: warning: (perhaps the 'offsetof' macro was used incorrectly) \[-Winvalid-offsetof\]  
> 10751 ../../../libtorrent/src/torrent.cpp: In constructor 'libtorrent::torrent::torrent(libtorrent::aux::session\_impl&, const endpoint&, int, int, const libto      rrent::add\_torrent\_params&, const sha1\_hash&)':  
> 10752 ../../../libtorrent/src/torrent.cpp:433:60: warning: large integer implicitly truncated to unsigned type \[-Woverflow\]  
> 10753 ../../../libtorrent/src/torrent.cpp:433:60: warning: large integer implicitly truncated to unsigned type \[-Woverflow\]  
> 10814 In file included from ../../src/gtBase.cpp:75:0:  
> 10815 ../../src/gtBase.h: In constructor 'gtBase::gtBase(gtBaseOpts&, gtBase::opMode)':  
> 10816 ../../src/gtBase.h:245:19: warning: 'gtBase::\_bindIP' will be initialized after \[-Wreorder\]  
> 10817 ../../src/gtBase.h:242:19: warning:   'std::string gtBase::\_resourceDir' \[-Wreorder\]  
> 10818 ../../src/gtBase.cpp:92:1: warning:   when initialized here \[-Wreorder\]  
> 10825 ../../src/gtDownload.cpp: In member function 'void gtDownload::extractURIsFromTSV(std::string, vectOfStr&)':  
> 10826 ../../src/gtDownload.cpp:528:38: warning: comparison between signed and unsigned integer expressions \[-Wsign-compare\]  
> 10827 ../../src/gtDownload.cpp: In member function 'void gtDownload::performSingleTorrentDownload(std::string, int64\_t&, int&)':  
> 10828 ../../src/gtDownload.cpp:834:21: warning: deprecated conversion from string constant to 'char\*' \[-Wwrite-strings\]  
> 10829 ../../src/gtDownload.cpp:836:21: warning: deprecated conversion from string constant to 'char\*' \[-Wwrite-strings\]  
> 10830 ../../src/gtDownload.cpp:839:18: warning: deprecated conversion from string constant to 'char\*' \[-Wwrite-strings\]  
> 10866 /usr/bin/ld: warning: libboost\_system.so.1.48.0, needed by /home/k/Documents/Code/cghub-genetorrent-476d7bd44985/GeneTorrent-3.8.7/deb-build/libtorrent/  
> 10870 /usr/bin/ld: warning: libboost\_system.so.1.48.0, needed by /home/k/Documents/Code/cghub-genetorrent-476d7bd44985/GeneTorrent-3.8.7/deb-build/libtorrent/  
> 10876 /usr/bin/ld: warning: libboost\_system.so.1.48.0, needed by /home/k/Documents/Code/cghub-genetorrent-476d7bd44985/GeneTorrent-3.8.7/deb-build/libtorrent/  
> 1  
> 10944 libtool: install: warning: remember to run \`libtool --finish /usr/lib/GeneTorrent'  
>   
> 10990 libtool: install: warning: relinking \`libgenetorrent.la'  
> 10997 libtool: install: warning: remember to run \`libtool --finish /usr/lib'  
> 11000 libtool: install: warning: \`/home/k/Documents/Code/cghub-genetorrent-476d7bd44985/GeneTorrent-3.8.7/deb-build/libtorrent/src/.libs/libtorrent-rasterbar.  
> 11001 libtool: install: warning: \`libgenetorrent.la' has not been installed in \`/usr/lib'  
> 11002 libtool: install: /usr/bin/install -c .libs/gtupload /home/k/Documents/Code/cghub-genetorrent-476d7bd44985/GeneTorrent-3.8.7/debian/tmp/usr/bin/gtupload  
> 11003 libtool: install: warning: \`/home/k/Documents/Code/cghub-genetorrent-476d7bd44985/GeneTorrent-3.8.7/deb-build/libtorrent/src/.libs/libtorrent-rasterbar.  
> 11004 libtool: install: warning: \`libgenetorrent.la' has not been installed in \`/usr/lib'  
> 11005 libtool: install: /usr/bin/install -c .libs/gtdownload /home/k/Documents/Code/cghub-genetorrent-476d7bd44985/GeneTorrent-3.8.7/debian/tmp/usr/bin/gtdown  
> 11006 libtool: install: warning: \`/home/k/Documents/Code/cghub-genetorrent-476d7bd44985/GeneTorrent-3.8.7/deb-build/libtorrent/src/.libs/libtorrent-rasterbar.  
> 11007 libtool: install: warning: \`libgenetorrent.la' has not been installed in \`/usr/lib'  
> 11111 dh\_pysupport: This program is deprecated, you should use dh\_python2 instead. Migration guide: http://deb.li/dhs2p  
> 11137 dpkg-shlibdeps: warning: package could avoid a useless dependency if debian/genetorrent-common/usr/lib/GeneTorrent/libboost\_regex.so.1.48.0 was not link  
> 11138 dpkg-shlibdeps: warning: package could avoid a useless dependency if debian/genetorrent-upload/usr/bin/gtupload was not linked against libboost\_regex.so  
> 11139 dpkg-shlibdeps: warning: package could avoid a useless dependency if debian/genetorrent-upload/usr/bin/gtupload was not linked against libboost\_filesyst  
> 11140 dpkg-shlibdeps: warning: package could avoid a useless dependency if debian/genetorrent-upload/usr/bin/gtupload was not linked against libssl.so.1.0.0 (  
> 11141 dpkg-shlibdeps: warning: package could avoid a useless dependency if debian/genetorrent-download/usr/bin/gtdownload was not linked against libboost\_rege  
> 11142 dpkg-shlibdeps: warning: package could avoid a useless dependency if debian/genetorrent-download/usr/bin/gtdownload was not linked against libxerces-c-3  
> 11143 dpkg-shlibdeps: warning: package could avoid a useless dependency if debian/genetorrent-download/usr/bin/gtdownload was not linked against libtorrent-ra  
> 11144 dpkg-shlibdeps: warning: package could avoid a useless dependency if debian/genetorrent-download/usr/bin/gtdownload was not linked against libboost\_file  
> 11145 dpkg-shlibdeps: warning: package could avoid a useless dependency if debian/genetorrent-download/usr/bin/gtdownload was not linked against libxqilla.so.  
> 11146 dpkg-shlibdeps: warning: package could avoid a useless dependency if debian/genetorrent-download/usr/bin/gtdownload was not linked against libcrypto.so.  
> 11147 dpkg-shlibdeps: warning: package could avoid a useless dependency if debian/genetorrent-download/usr/bin/gtdownload was not linked against libssl.so.1.0  
> 11150 dpkg-gencontrol: warning: package genetorrent-upload: unused substitution variable ${python:Depends}  
> 11164 Now running lintian...  
> 11165 E: genetorrent-download: binary-or-shlib-defines-rpath usr/bin/gtdownload /usr/lib/GeneTorrent  
> 11166 W: genetorrent-download: hardening-no-relro usr/bin/gtdownload  
> 11167 W: genetorrent-download: hardening-no-fortify-functions usr/bin/gtdownload  
> 11168 W: genetorrent-common: package-name-doesnt-match-sonames libgenetorrent0  
> 11169 W: genetorrent-common: hardening-no-relro usr/lib/GeneTorrent/libboost\_filesystem.so.1.48.0  
> 11170 W: genetorrent-common: hardening-no-fortify-functions usr/lib/GeneTorrent/libboost\_filesystem.so.1.48.0  
> 11171 W: genetorrent-common: hardening-no-relro usr/lib/GeneTorrent/libboost\_program\_options.so.1.48.0  
> 11172 W: genetorrent-common: hardening-no-fortify-functions usr/lib/GeneTorrent/libboost\_program\_options.so.1.48.0  
> 11173 W: genetorrent-common: hardening-no-relro usr/lib/GeneTorrent/libboost\_regex.so.1.48.0  
> 11174 W: genetorrent-common: hardening-no-fortify-functions usr/lib/GeneTorrent/libboost\_regex.so.1.48.0  
> 11175 W: genetorrent-common: hardening-no-relro usr/lib/GeneTorrent/libboost\_system.so.1.48.0  
> 11176 W: genetorrent-common: hardening-no-relro usr/lib/GeneTorrent/libboost\_thread.so.1.48.0  
> 11177 W: genetorrent-common: hardening-no-relro usr/lib/GeneTorrent/libtorrent-rasterbar.so.6.0.0  
> 11178 W: genetorrent-common: hardening-no-fortify-functions usr/lib/GeneTorrent/libtorrent-rasterbar.so.6.0.0  
> 11179 W: genetorrent-common: hardening-no-relro usr/lib/libgenetorrent.so.0.0.0  
> 11180 W: genetorrent-common: hardening-no-fortify-functions usr/lib/libgenetorrent.so.0.0.0  
> 11181 W: genetorrent-common: extra-license-file usr/share/doc/GeneTorrent/LICENSE.gz  
> 11182 W: genetorrent-common: binary-without-manpage usr/bin/cgquery  
> 11183 W: genetorrent-common: binary-without-manpage usr/bin/gtocheck  
> 11184 W: genetorrent-common: binary-without-manpage usr/bin/gtoinfo  
> 11185 W: genetorrent-common: non-dev-pkg-with-shlib-symlink usr/lib/libgenetorrent.so.0.0.0 usr/lib/libgenetorrent.so  
> 11186 E: genetorrent-dbg: extended-description-is-empty  
> 11187 W: genetorrent-dbg: wrong-section-according-to-package-name genetorrent-dbg => debug  
> 11188 W: genetorrent-dbg: empty-binary-package  
> 11189 E: genetorrent-upload: binary-or-shlib-defines-rpath usr/bin/gtupload /usr/lib/GeneTorrent  
> 11190 W: genetorrent-upload: hardening-no-relro usr/bin/gtupload  
> 11191 W: genetorrent-upload: hardening-no-fortify-functions usr/bin/gtupload  
> 11192 W: genetorrent-upload: binary-without-manpage usr/bin/cgsubmit  
> 11193 E: genetorrent-upload: python-script-but-no-python-dep usr/bin/cgsubmit  
> 11194 Finished running lintian.
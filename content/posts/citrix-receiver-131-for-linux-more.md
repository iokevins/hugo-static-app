---
title: 'Citrix Receiver 13.1 for Linux - More Citrix, More Problems'
date: 2015-01-11T09:38:00.000-08:00
draft: false
tags: 
- linux
- citrix
- debian
- receiver
---

Smiled when I saw Citrix released [Citrix Receiver 13.1 for Linux](http://www.citrix.com/downloads/citrix-receiver/linux/receiver-for-linux-131.html), what seems like a true 64-bit Citrix Receiver client. It seemed to install cleanly to Debian Wheezy--good. It even allowed me to login to my employer's install of Citrix Web Interface 5.? to access XenApp VM hosted apps--promising.  
  
However, selecting a hosted app icon via the Web Interface only seemed to change my mouse cursor from a pointer into a spinning circle for a few seconds, after which it revered to a pointer. Waiting for several minutes, nothing appeared. I tried access in both Mozilla IceWeasel 31.3.0 and Google Chrome 37.0.2062.120. Poking around in /opt/Citrix/ICAClient/, I noted running the binaries seemed to work OK (for example, selfservice)...no core dumps or broken dependencies, it seems.  
  
I also tried installing the Citrix [Receiver for HTML5 1.5](http://www.citrix.com/downloads/citrix-receiver/html5/receiver-for-html5-15.html). This seemed to have similar results as the Citrix Receiver 13.1 for Linux--successful authentication, but no success when selecting hosted app icons.  
  
A WORKAROUND  
  
A brief web search discovered this URL:  
  
[http://zo0ok.com/techfindings/archives/1743](http://zo0ok.com/techfindings/archives/1743)  
  
which pointed me to /opt/Citrix/ICAClient/wfica.sh . I downloaded the .ICA file after selecting the hosted app icon, then passed the file path to it as a parameter to wfica.sh, as described at the URL. Success.  
  
So, at this point, I know I can run hosted apps manually, which suffices....  
  
[Previously](http://iokevins.blogspot.com/2014/04/linux-debian-citrix-receiver-ssl-error.html); [Previously](http://iokevins.blogspot.com/2012/09/errata-configuring-debian-gnulinux-605.html); [Previously](http://iokevins.blogspot.com/2013/06/configuring-debian-gnulinux-7-wheezy.html)
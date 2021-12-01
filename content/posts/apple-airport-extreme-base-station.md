---
title: 'Apple Airport Extreme Base Station: Model A1408 (4th Generation)'
date: 2015-11-29T00:20:00.001-08:00
draft: false
tags: 
- base station
- A1408
- apple
- airport-utils
- linux
- debian
- airport
- airport extreme
---

A new-to-me piece of hardware: an Apple Airport Extreme Base Station: Model A1408 (4th Generation), circa 2011.  
  
Performed a factory reset, then powered it on and attempted to configure via Debian, after installing package airport-utils:  

> sudo apt-get install airport-utils

However, when I attempted to retrieve settings from the device, I got an error: 

> sudo airport2-config  
> Retrieving settings from base station /10.0.1.1......  
> Error retrieving settings (check password)

An nmap scan returns the following:  

> Starting Nmap 6.47 ( http://nmap.org ) at 2015-11-28 20:12 PST  
> Nmap scan report for 10.0.1.1  
> Host is up (0.00016s latency).  
> Not shown: 997 closed ports  
> PORT      STATE SERVICE  
> 53/tcp    open  domain  
> 5009/tcp  open  airport-admin  
> 10000/tcp open  snet-sensor-mgmt

I tried telnet to port 5009 but standard commands did not seem to receive a response, so abandoned the effort.  
  
After some tinkering, I located an iPod Touch (4th Generation) which I used to perform the initial configuration of the wireless router, setting a password and configuring the router SSID.  
  
After that, airport2-config successfully authenticates to the AEBS and retrieves the settings. That's as far as I got--I have not tried to save modifications back to the device.  
  
We currently have a Linksys WRH54G router, running DD-WRT, so, while the AEBS seems cool and supports 802.11n, a step up, without Apple devices to configure and use it with, it seems a bit out-of-place and unwieldy to manage. Some basic, open questions:  
  

*   Can I configure the AEBS to filter wireless access, by MAC address? If so, how?
*   What benefits might I get to using the AEBS?

Leaving it, for now.
---
title: 'Tomato Router: Upgrading'
date: 2021-08-15T16:38:00.002-07:00
draft: false
tags: 
- tomato
- router
- upgrade
---

Message "New version of FreshTomato 2021.5 is now available. Click here to download" indicates it's time to upgrade our Cisco Linksys EA6400 with ARMv7 Processor rev 0 (v7l).

Select Download > freshtomato-arm > 2021 > 2021.5 > K26ARM, then download the file wiht EA6400 and AIO (all in one):

freshtomato-EA6400-ARM\_NG-2021.5-AIO-64K.zip

[Note](https://www.reddit.com/r/TomatoFTW/comments/p3qr46/release_20215/?utm_source=share&utm_medium=web2x&context=3):

> When upgrading it is recommended to clear NVRAM and to NOT restore an old config file. If you keep your settings from a previous version and do experience issues step one is to clear NVRAM without restoring an old configuration to see if this resolves them.

Logon to router:

Connect to router WiFi.

http://192.168.1.1/ 

#### Backup the existing configuration file

Select menu link Administration > Configuration

Backup the existing configuration.

#### Upgrade the router

Select menu link Administration > Upgrade

Select checkbox "After flashing, erase all data in NVRAM memory".

Select file location (e.g., freshtomato-EA6400-ARM\_NG-2021.5-AIO-64K.trx)

Select button Upgrade, then on popup "Are you sure you want to upgrade using freshtomato-EA6400-ARM\_NG-2021.5-AIO-64K.trx?", select button OK.

Tomato router displays screen with timer and message "Please wait while the firmware is uploaded & flashed. Warning: Do not interrupt this browser or the router!"

After about a minute, timer continues with message, "linux: CRC OK - Image successfully flashed. Please wait while the router reboots... " 

Select button Continue when it appears.

Clearing NVRAM removes the old configuration. 

Default username / password is root / admin

Logon, then restore old configuration:

Select menu link Administration > Configuration

Load old configuration. Router reboots. 

Connect to router WiFi. 

Logon with previous username / password.

Done.
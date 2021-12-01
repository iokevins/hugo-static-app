---
title: 'Tomato Router: Resetting WWAN '
date: 2021-08-27T20:34:00.005-07:00
draft: false
tags: 
- reset
- tomato
- router
- wwan
---

This arcane spell, for future reference:

*   Log on to 192.168.1.1
*   Advanced > Virtual Wireless

*   For Interface eth2 (wl1) / 5 GHz:
*   Set Bridge = LAN0 (br0)
*   Select button Save
*   Set Bridge = none
*   Select button Save

*   Select menu link Status

*   Wireless eth2 (wl1) / 5 GHz

*   Select button Disable (wait for 5 seconds)
*   Select button Enable (wait for 5 seconds)

*   WAN0

*   Select button Release
*   Select button Renew
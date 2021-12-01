---
title: 'Netgear Nighthawk LTE Mobile Hotspot Router: Data Offloading'
date: 2020-05-26T14:58:00.001-07:00
draft: false
---

If you get an error while attempting to enable Data offloading, (e.g., "configure a unique subnet"), the solution that worked for me was to set the IP address of the hotspot to **192.168.2.1**:

*   Navigate to [http://attwifimanager/](http://attwifimanager/) and logon
*   Settings > Setup > Mobile Router Setup

*   Gateway IP Address: 192.168.2.1
*   DHCP Starting IP Address: 192.168.2.100
*   DHCP Ending IP Address: 192.168.2.150
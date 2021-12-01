---
title: 'Debian Stretch (Testing) - Connecting to Remote Desktop Services and Running a RemoteApp'
date: 2016-02-19T21:22:00.000-08:00
draft: false
tags: 
- rdp
- rds
- remote access
- stretch
- remoteapp
- linux
- gateway
- xfreerdp
- debian
- freerdp
---

Connecting, from a host running Debian Stretch (Testing), to a work site's installation of [Microsoft Remote Desktop Services (RDS)](https://en.wikipedia.org/wiki/Remote_Desktop_Services), to perform four tasks:  
  

1.  Authenticate, to Remote Desktop Gateway (RD Gateway) 
2.  Run [RemoteApp](https://en.wikipedia.org/wiki/Remote_Desktop_Services#RemoteApp) "[Remote Desktop Connection (RDC)](https://en.wikipedia.org/wiki/Remote_Desktop_Services#Remote_Desktop_Connection)"
3.  Connect to intranet-only equipment
4.  Do additional work

  
Debian Stretch supports a number of third-party clients implementing Microsoft's proprietary [Remote Desktop Protocol (RDP)](https://en.wikipedia.org/wiki/Remote_Desktop_Protocol). For example, [rdesktop](https://en.wikipedia.org/wiki/Rdesktop), [xfreerdp](http://www.freerdp.com/), [tsclient](https://en.wikipedia.org/wiki/Tsclient), and [Remmina](https://en.wikipedia.org/wiki/Remmina) (the latter are GUI frontends, for rdesktop and xfreerdp, respectively).  
  
Here's an example usage, using xfreerdp:  

> xfreerdp +clipboard +compression -themes -wallpaper /g:gateway.domain.com /gu:domain\\\\user /gp:'password123!' /app:"||mstsc" /v:hostname.local /u:domain\\\\user /p:'password123!'

#### NOTES

*   Escape the backslash, if used: domain\\\\user (note: can separate, using domain parameter /d and/or /gd)
*   Authenticating, to the work site's Remote Desktop Web Access (RD Web Access), via a web browser, triggers [two-factor authentication (2FA)](https://en.wikipedia.org/wiki/Two-factor_authentication)...but authenticating to RD Gateway, via command-line xfreerdp, does not...good to know
*   I downloaded the nightly build or xfreerdp and compiled, per [instructions](https://github.com/FreeRDP/FreeRDP/wiki/Compilation)
*   xfreerdp --version

*   "This is FreeRDP version 2.0.0-dev (git n/a)"

*   Debian Stretch currently ships, as of this writing, with package xfreerdp-x11 1.1.0 ([specifically](https://packages.debian.org/stretch/freerdp-x11), version "1.1.0~git20140921.1.440916e+dfsg1-5+b1")
*   Q: Why the name “Remmina”? A: This is mostly personal preference. :) But just for you to easier remember it, it can also stand for Remote Mini Assistant. ([via](http://www.remmina.org/wp/faq/))
*   Hostname.local, above, retrieved after authenticating to RD Web Access, selecting a RemoteApp, downloading the RDP file, when prompted, and then reviewing the RDP file contents
*   xfreerdp option /app seems to require parenthesis around the value, as well as a prefix of two pipe characters, "||"
*   Microsoft client "Remote Desktop Connection" (RDC) represents the re-branding of Microsoft Terminal Services Client, which explains the name, "mstsc"

#### RESOURCES

xfreerdp 

*   Options: [https://github.com/FreeRDP/FreeRDP/wiki/CommandLineInterface](https://github.com/FreeRDP/FreeRDP/wiki/CommandLineInterface)
*   Compiling: [https://github.com/FreeRDP/FreeRDP/wiki/Compilation](https://github.com/FreeRDP/FreeRDP/wiki/Compilation)

Microsoft Remote Desktop Services (RDS)

*   Wikipedia: [https://en.wikipedia.org/wiki/Remote\_Desktop\_Services](https://en.wikipedia.org/wiki/Remote_Desktop_Services)
*   Other (?)

Remmina: [http://www.remmina.org/](http://www.remmina.org/)
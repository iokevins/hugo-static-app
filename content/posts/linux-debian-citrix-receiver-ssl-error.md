---
title: 'Linux (Debian) + Citrix Receiver SSL Error: You have not chosen to trust "DigiCert High Assurance CA-3" the issuer of the server''s security certificate (SSL error 61)'
date: 2014-04-30T10:39:00.000-07:00
draft: false
tags: 
- linux
- debian
---

Fixed this issue today on my install of Debian.  
  
The exact error received: "You have not chosen to trust "DigiCert High Assurance CA-3" the issuer of the server's security certificate (SSL error 61)"  
  
Relevant [Google search phrase](https://www.google.com/search?q=linux+citrix+receiver+ssl+error): "linux citrux receiver ssl error"  
  
This led to this Ubuntu forums post: [http://ubuntuforums.org/showthread.php?t=1975705](http://ubuntuforums.org/showthread.php?t=1975705)  
  
I Google'd for "[DigiCert High Assurance CA-3](https://www.google.com/search?q=DigiCert+High+Assurance+CA-3&oq=DigiCert+High+Assurance+CA-3)", which led me to page, "[DigiCert Root Certificates :: Download and Test SSL](https://www.digicert.com/digicert-root-certificates.htm)"  
  
I downloaded all six certs containing the phrase "High Assurance" to my Desktop:  
  

1.  DigiCert High Assurance EV Root CA
2.  DigiCert High Assurance EV CA-1
3.  DigiCert High Assurance CA-3
4.  DigiCert High Assurance Code Signing CA-1
5.  DigiCert SHA2 High Assurance Server CA
6.  DigiCert SHA2 High Assurance Code Signing CA

Then, I moved them to the global ICAClient cacerts folder

  

sudo mv ~/Desktop/\*.crt /opt/Citrix/ICAClient/keystore/cacerts

  

Then, finally, I rehashed everything:

  

sudo c\_rehash /opt/Citrix/ICAClient/keystore/cacerts

  

After restarting my web browser (Chromium Version 32.0.1700.123 Debian 7.4 (248368)), things began working.

  

NOTE

  

I initially downloaded just certificate "DigiCert High Assurance CA-3"...but this did not work.I am not sure which of the above, therefore, allowed it to work.
---
### Comments:
#### Awesome, thanks Kevin!  
I followed your instruct...
[Vern](https://www.blogger.com/profile/03143116986504503543 "noreply@blogger.com") - <time datetime="2015-03-29T16:41:51.852-07:00">Mar 0, 2015</time>

Awesome, thanks Kevin!  
I followed your instructions and you saved me a big headache.  
Thanks for taking the time to post the solution.
<hr />

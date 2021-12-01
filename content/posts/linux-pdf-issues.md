---
title: 'Linux PDF Issues'
date: 2008-08-02T12:28:00.000-07:00
draft: false
tags: 
- okular
- kubuntu
- firefox
- foxit
- linux
- pdf
- kde4
---

Firefox failed to load a PDF I typed into the address bar.  
  
After a bit of trial and error, I discovered the [PDF Download](https://addons.mozilla.org/en-US/firefox/addon/636) add-on, which makes it all simpler when one clicks a link.  
  
I first downloaded [FoxIt PDF reader](http://www.foxitsoftware.com/pdf/desklinux/) for Linux (binary) and told Firefox to use that to open PDFs. Unfortunately, it opens the ReaderLinux binary, not the PDF. And once I associated the file type with the binary, the Linux Firefox fails to provide an easy way to disassociate itself from that.  
  
The solution: edit file ~/.mozilla/firefox/profile.default/mimeTypes.rdf, and delete the XML sections dealing with ReaderLinux. Restart Firefox. The next time you attempt to open a PDF, Firefox will prompt the user again for what to do.  
  
The final solution? Associating Okular (/usr/lib/kde4/bin/okular) with PDF file types instead works great. And PDF Download add-on works great too.
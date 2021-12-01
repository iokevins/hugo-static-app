---
title: 'CUPS Filter Failures'
date: 2016-09-18T19:42:00.003-07:00
draft: false
---

Experienced the following issue, starting Saturday, September 17, 2016, on Debian Stretch (Testing):  

*   Attempt to print PDF
*   Start Printer Settings (that is, /usr/bin/python3 /usr/share/system-config-printer/system-config-printer.py) 
*   Unlock the printer
*   Printer Properties shows printer failed with "Filter failed"
*   Viewing the print queue shows the print job "Held" or some such error

In my case, after setting debug mode, CUPS reported the following error:

> D \[18/Sep/2016:16:49:29 -0700\] \[Job 87\] 3 filters for job:D \[18/Sep/2016:16:49:29 -0700\] \[Job 87\] envp\[9\]="PATH=/usr/lib/cups/filter:/usr/bin:/usr/sbin:/bin:/usr/bin"I \[18/Sep/2016:16:49:29 -0700\] \[Job 87\] Started filter /usr/lib/cups/filter/pdftopdf (PID 14304)I \[18/Sep/2016:16:49:29 -0700\] \[Job 87\] Started filter /usr/lib/cups/filter/pdftops (PID 14305)I \[18/Sep/2016:16:49:29 -0700\] \[Job 87\] Started filter /usr/lib/cups/filter/hpps (PID 14306)D \[18/Sep/2016:16:49:29 -0700\] \[Job 87\] pdftopdf: Last filter determined by the PPD: hpps; FINAL\_CONTENT\_TYPE: application/vnd.cups-postscript => pdftopdf will log pages in page\_log.D \[18/Sep/2016:16:49:29 -0700\] \[Job 87\] PID 14304 (/usr/lib/cups/filter/pdftopdf) exited with no errors.D \[18/Sep/2016:16:49:29 -0700\] \[Job 87\] Started filter gs (PID 14308)D \[18/Sep/2016:16:49:29 -0700\] \[Job 87\] Started filter pstops (PID 14309)D \[18/Sep/2016:16:49:33 -0700\] \[Job 87\] File \\"/usr/lib/cups/filter/hpps\\", line 379, in <module>D \[18/Sep/2016:16:49:33 -0700\] \[Job 87\] PID 14306 (/usr/lib/cups/filter/hpps) stopped with status 1.D \[18/Sep/2016:16:49:33 -0700\] \[Job 87\] PID 14305 (/usr/lib/cups/filter/pdftops) exited with no errors.

I re-installed CUPS, restarted CUPS, rebooted the printer, reconnected to the printer, and so forth. No good.

  

Finally, after about 30 minutes, the job went through. I don't know what I did. 

  

Subsequently, I ran hp-check -t, and installed all the packages marked optional/required. A test print works just fine. 

  

hp-check -t

sudo vim /etc/cups/cupsd.conf  
/etc/init.d/cups restart  
sudo tail -f /var/log/cups/error\_log  
sudo grep -i filter /var/log/cups/error\_log  
  
UPSTREAM  
http://hplipopensource.com/hplip-web/index.html  
https://launchpad.net/hplip  
  
DOWNSTREAM  
https://bugs.archlinux.org/task/50588  
https://bugs.debian.org/cgi-bin/pkgreport.cgi?package=hplip
---
### Comments:
#### Наблюдаю такой же баг \[21/Aug/2017:13:08:17 +0300...
[Unknown](https://www.blogger.com/profile/07402787207033236501 "noreply@blogger.com") - <time datetime="2017-08-21T03:13:03.558-07:00">Aug 1, 2017</time>

Наблюдаю такой же баг \[21/Aug/2017:13:08:17 +0300\] \[Job 21701\] File "/usr/lib/cups/filter/hpps", line 379, in  
D \[21/Aug/2017:13:08:17 +0300\] \[Job 21701\] PID 10797 (/usr/lib/cups/backend/hp) did not catch or ignore signal 13.  
D \[21/Aug/2017:13:08:17 +0300\] \[Job 21701\] os.write(output\_fd, data)  
D \[21/Aug/2017:13:08:17 +0300\] \[Job 21701\] OSError: \[Errno 32\] Broken pipe  
D \[21/Aug/2017:13:08:17 +0300\] \[Job 21701\] Before copy\_setup - %%Page: 1 1  
D \[21/Aug/2017:13:08:17 +0300\] \[Job 21701\] Before page loop - %%Page: 1 1  
D \[21/Aug/2017:13:08:17 +0300\] \[Job 21701\] Copying page 1...  
D \[21/Aug/2017:13:08:17 +0300\] \[Job 21701\] pagew = 571.0, pagel = 818.0  
D \[21/Aug/2017:13:08:17 +0300\] \[Job 21701\] bboxx = 0, bboxy = 0, bboxw = 595, bboxl = 842  
D \[21/Aug/2017:13:08:17 +0300\] \[Job 21701\] PageLeft = 12.0, PageRight = 583.0  
D \[21/Aug/2017:13:08:17 +0300\] \[Job 21701\] PageTop = 830.0, PageBottom = 12.0  
D \[21/Aug/2017:13:08:17 +0300\] \[Job 21701\] PageWidth = 595.0, PageLength = 842.0  
D \[21/Aug/2017:13:08:17 +0300\] \[Job 21701\] PID 10796 (/usr/lib/cups/filter/hpps) stopped with status 1.  
D \[21/Aug/2017:13:08:17 +0300\] \[Job 21701\] Hint: Try setting the LogLevel to "debug" to find out more.  
D \[21/Aug/2017:13:08:17 +0300\] \[Job 21701\] Wrote 1 pages...  
D \[21/Aug/2017:13:08:17 +0300\] \[Job 21701\] PID 10799 (pstops) exited with no errors.  
D \[21/Aug/2017:13:08:17 +0300\] \[Job 21701\] PID 10798 (gs) exited with no errors.  
D \[21/Aug/2017:13:08:17 +0300\] \[Job 21701\] PID 10795 (/usr/lib/cups/filter/pdftops) exited with no errors.  
D \[21/Aug/2017:13:08:17 +0300\] \[Job 21701\] End of messages  
D \[21/Aug/2017:13:08:17 +0300\] \[Job 21701\] printer-state=3(idle)  
D \[21/Aug/2017:13:08:17 +0300\] \[Job 21701\] printer-state-message="Filter failed"  
D \[21/Aug/2017:13:08:17 +0300\] \[Job 21701\] printer-state-reasons=none
<hr />

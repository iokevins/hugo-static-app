---
title: 'ALSA Restart'
date: 2008-09-15T19:53:00.000-07:00
draft: false
---

ALSA failed this evening. Fixed it this way:  

1.  lsof | grep pcm
2.  kill -9 any processes returned
3.  restarted ALSA: sudo /etc/init.d/alsa-utils restart
4.  Didn't work--quit Firefox, then ps -ef | grep firefox
5.  kill -9 the firefox process
6.  restarted ALSA: sudo /etc/init.d/alsa-utils restart
7.  Sound returns--yippee  
    

Thanks to; http://lookherefirst.wordpress.com/2008/05/29/restarting-sound-server-in-kubuntu/
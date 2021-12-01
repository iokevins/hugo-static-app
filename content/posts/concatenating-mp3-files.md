---
title: 'Concatenating MP3 Files'
date: 2015-10-13T20:48:00.003-07:00
draft: false
---

Had a need to concatenate a number of MP3 files into one, which turns out quite simple, using _cat_:  
  
$ cat my\_file\_1.mp3 my\_file\_2.mp3 my\_file\_3.mp3 > combined\_files.mp3  
$ avconv -i combined\_files.mp3 -acodec copy combined\_files\_fixed.mp3  
  
The latter line cleans up the mp3 headers.  
Hat tip: [http://kokoko.fluxionary.net/merging-mp3-files/](http://kokoko.fluxionary.net/merging-mp3-files/)
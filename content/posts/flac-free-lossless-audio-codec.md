---
title: 'FLAC - Free Lossless Audio Codec'
date: 2016-01-23T23:23:00.001-08:00
draft: false
tags: 
- audio
- stretch
- linux
- debian
- flac
---

Looking to make archival backups of CDs, so researching FLAC, as well as surrounding topics.  
[  
Morituri](http://thomas.apestaart.org/morituri/trac/) seems like a recommended tool:  

*   .cue file generation
*   metadata lookup
*   FLAC

However, while Debian currently seems to support [morituri](https://packages.debian.org/jessie/morituri) version 0.2.3-1, in Jessie (stable), and version 0.2.3-2, in [experimental](https://packages.debian.org/experimental/morituri), but does not yet have a package supported, in Stretch (testing). As a workaround, I downloaded the latest build, via git, installed it, and attempted to run the offset utility, but it failed, with a python error, on import of gst. So, abandoning it, for now.  
  
Alternatively, with [Wine](https://wiki.debian.org/Wine) support, I can run EAC (Exact Audio Copy), which seems universally respected. I seem to have gotten Wine installed, and EAC/.NET 2.0 installed and working So, this may represent a way forward.  

### RESOURCES

*   Briefly got in the queue at [what.cd](https://www.whatinterviewprep.com/) IRC, but abandoned the effort, due to long wait
*   [Cue Sheet (Computing)](https://en.wikipedia.org/wiki/Cue_sheet_%28computing%29)
*   [CD Ripper](https://en.wikipedia.org/wiki/CD_ripper)
*   Metadata

*   [AMG's](https://en.wikipedia.org/wiki/All_Media_Guide) [LASSO](https://en.wikipedia.org/wiki/AMG_LASSO)
*   [FreeDB](https://en.wikipedia.org/wiki/FreeDB)
*   [Gracenote](https://en.wikipedia.org/wiki/Gracenote)'s [CDDB](https://en.wikipedia.org/wiki/CDDB)
*   GD3 [\[1\]](http://www.getdigitaldata.com/)
*   [MusicBrainz](https://en.wikipedia.org/wiki/MusicBrainz)
*   Text extraction, if [CD-Text](https://en.wikipedia.org/wiki/CD-Text) has been stored
*   Other: [List of online music databases](https://en.wikipedia.org/wiki/List_of_online_music_databases)

*   ["Secure" ripping](http://wiki.hydrogenaud.io/index.php?title=Secure_ripping): "Secure ripping is the process of making sure there were no errors during the extraction of audio from a CD. It normally involves attempting to get consistent results from successive re-reads of the same sectors, and is sometimes combined with other strategies...."
*   Optical drive [considerations](https://en.wikipedia.org/wiki/CD_ripper#Optical_drive_properties):

*   Small sample-offset (at best zero)
*   No [jitter](https://en.wikipedia.org/wiki/Jitter)
*   No or deactivateable [caching](https://en.wikipedia.org/wiki/Cache_(computing))
*   correct implementation and feed-back of the C1 and [C2](https://en.wikipedia.org/wiki/C2_error) error-states

*   [C1](http://www.cdmasteringservices.com/digitalerrors.htm): "C1 Errors refer to the block error rate (BLER), which consists of bit errors at the lowest level.  C1 errors are always expressed in errors per second.  All CDs and CDRs contain C1 errors.  They are a normal result of the write process.  However, the maximum C1 error rate for a quality recording is an average of 220 errors per second based on 10 second samples."
*   [C2](http://www.cdmasteringservices.com/digitalerrors.htm): "C2 Errors refer to bytes in a frame (24 bytes per frame, 98 frames per block) and is an indication of a CD player's attempt to use error correction to recover lost data.  C2 errors can be serious. In theory, a CD player should correct them. C2 errors are usually an indication of poor media quality, or the failure of a CD burner to produce a quality burn...."

*   [DAE Features Database](http://www.daefeatures.co.uk/index.php)

*   I started submitting the TSSTCorp (Samsung) SE-506, but they wanted a bunch of fields and it was getting increasingly rediculous, on Debian, to get them all, so shelved it, for now

*
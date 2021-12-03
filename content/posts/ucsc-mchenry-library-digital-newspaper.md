---
title: 'UCSC McHenry Library Digital Newspaper Displays'
date: 2015-07-24T15:43:00.000-07:00
draft: false
tags: 
- santa cruz
---

[![](/images/5928790835_c5a3327d46_z320.jpg)](/images/5928790835_c5a3327d46_z.jpg)

  

Collecting info on the newspaper displays in the lobby of the McHenry Library, which rotate frontpages from around the world.  
  
Lee Jaffe's installation photos:  
[https://www.flickr.com/photos/ldjaffe/5833872485/in/album-72157626824825533/](https://www.flickr.com/photos/ldjaffe/5833872485/in/album-72157626824825533/)  

*   Modeled after installation at UC Berkeley International House
*   "These photos document work on a 6-screen installation that will feature front pages from newspapers worldwide. The architects left us with pretty much nothing we could use and in fact added some extra surprises. I'm working with Doug Russo, a carpenter, to design and build this installation that we hope will compensate for the deficiencies of the space in an attractive and secure manner."
*   "...the electrical raceway \[was\] added for a different project just before we started our installation. Nobody thinks this was done well -- there is conduit all throughout the wall and it could have been routed differently -- but there is no money to fix it at this point. We were able to reposition our installation a bit to cover some of the raceway but we cannot hide it completely." ([photo](https://www.flickr.com/photos/ldjaffe/5827193407/in/album-72157626824825533/))
*   Installation occurred during summer 2011

Gifts funding the creation: "UC Santa Cruz receives $350,000 to create global café and reading garden at University Library"  
[http://news.ucsc.edu/2007/01/1028.html](http://news.ucsc.edu/2007/01/1028.html)  

*   "Stephen Silberstein--cofounder and former president of Innovative Interfaces, a library software company in Emeryville, California-has donated $250,000 to create a global cyber café in the campus's newly expanded and renovated McHenry Library."
*   "Plans for the UC Santa Cruz café include a rotating digital newspaper display that spotlights up-to-date front pages of approximately 140 newspapers from around the world. Representing the varied geographic areas of Asia, Europe, South America, Africa, the Middle East, and the United States, the newspaper exhibit is designed to contrast different global perspectives of current events."

UPDATE, 8/3/2015: A UCSC staff member writes:  

> "The person who was most directly involved with the implementation of this system has retired. I will try to answer your questions as best I can. 

> The current newspaper display was installed in 2011 based on an earlier pilot installation in 2009. It uses Mac Mini computers and 30" Dell monitors. The image swapping is managed by the MacOS screen saver application. The newspaper images are .jpegs managed by newseum.org and those images are updated on that site daily. The library contracted with a programmer to do some customized scripting to automate the daily download of new newspaper images. Unfortunately, I do not have any contact information for that developer."

So, it sounds like a script downloads the fixed image URLs, from Newseum, which updates the image URLs, daily. For example, the Centre, Alabama, USA newspaper, "[The Post](http://www.newseum.org/todaysfrontpages/?tfp_id=AL_TP)". The script may copy the images to a folder on the computer driving each display (or perhaps a server folder). The computer then displays the images, in the configured folder, via native screensaver utility.  
  
Seems pretty straightforward! I had wondered if Newseum represented the source; nice to see it confirmed. The script just iterates over a configured list of newspaper images, probably calling something like wget.  
  
Note: Lee Jaffe may represent the retired staff member referred to, above. The 2009 installation seems to represents the install seen in several photos from Lee's Flickr account, prior to the McHenry Library remodel.  
  
UPDATE, 8/11/2015:  
  
Stuart Camenson writes: Hardware-wise, the News Readers are simply Mac Minis connected to displays. The newspaper front pages that are displayed through the Classic Mac screensaver (a simple slideshow) where the source is set as a folder containing the front pages in jpg format. The computer is setup to turn on and shutdown at 7:30 AM and 3 AM respectively and reboot automatically during a power outage, auto login is enabled, and neither the computer nor the display ever sleep. Finally the screensaver is setup to start >20 min to allow time for the download and processing of the front pages.  
  
Software-wise, an application called Newspaper is launched automatically at startup and controls the download and processing of the front pages. The application was created on a mac using automator and its workflow is as follows:  

#### 

1.  Pause: 5 minutes

1.  This action pauses the workflow to allow the computer to connect to the network and do other things![](https://lh3.googleusercontent.com/KF_iZ06kC0aqqc5O1KMDie-YZW8v-pJd3lGlMckohzNk--mURfKmorCKUMt9IsCbfTZWaF-WrUJyoZhEBodggVJeF419CsOLVSFbWzXv_H02FW8EykAevBS1cZHC3jWt7H8lcPw)

3.  Find Finder items: in folder Fronts

1.  All newspaper images are saved to the folder Fronts
2.  This action searches for any items in the folder (yesterday’s images) and passes the results to the next action![](https://lh6.googleusercontent.com/VoJn0NDHxZT_ugjv5ndgse6RINeHVaeQvkEaWHOj1mwnJi6Sza4zl0KWImztpPOtTSY1wgdj9x7uh7KCeMnjo-_1b0B7GmgZbL2Rp8XJ9g_TKz-DdpLBkDI6bDmangNrG8fE6HY)

5.  Move Finder Items to Trash

1.  This action trashes the items from the previous action![](https://lh5.googleusercontent.com/r5rnpVLVkQIqbbRUFcZMq8H6Y-2g2qeUf4LP179O-sCGrP7oSyY3K2hUUYfXQtBNJLFwzWYVxhrTCKOgOMKCOodGOll5MQYmV0dA5fRhCsDAYwr704mwQlIeK-_y3SotMCqpHUw)

7.  Run AppleScript: empty trash

1.  This script empties the Trash![](https://lh3.googleusercontent.com/CB488lRa8HeGTcdgpn0X13jkZig6SoRs45WCustwMgShuPXibWU0wBQ18ioIcbJQucjptEmT3KKTPEeOONahRMB6e0BghV9OBm1AJqpTYHClr82b0VyQxiNvNrs1B5o2yuVbHpQ)

9.  Get Specified Text:

1.  This action inputs 1014 links for the source [newseum.org](http://newseum.org/) (see page 4). The links are formatted like this: http://webmedia.newseum.org/newseum-multimedia/dfp/jpg<<dd>>/lg/AL\_DD.jpg
2.  The <<dd>> is replaced with the date in the next action
3.  These links are subject to change by newseum but have remained the same for the last several months. The filename at the end of the link (something.jpg) is unique to each newspaper.![](https://lh5.googleusercontent.com/xIxP6urLwgAtyHaBYA_ErOJ-fjKJVjHSskhsojaSMI0TBKJYqpIl7dml3k4VB07hOjdMNo6AH3cL4tF7-s66IdiVy6rpTYwgDVxfxL-azvn6i4nsG_dkI89b9AaWLoDNEPqlO7c)

11.  Run Shell Script

1.  This action replaces <<dd>> with today’s date so that the link now looks like this: [http://webmedia.newseum.org/newseum-multimedia/dfp/jpg29/lg/AL\_DD.jpg](http://webmedia.newseum.org/newseum-multimedia/dfp/jpg29/lg/AL_DD.jpg)![](https://lh6.googleusercontent.com/nYvFaPrTJiFGNklQDfsULsPcR5Pp6u7I_nqwsV5c2DmnOv7AZujUcYdBge1gVNnwdHX8aXuybLgEJzCHKLX1E5lo5spVP6mn4GcW95rypZQhVqhPHicsZsL2Y_gK4Xvu4x1BqFI)

13.  Get Specified URLs

1.  This action passes the results from the previous action to the next action![](https://lh6.googleusercontent.com/h5mkYUr3cW_cARHN7yxbldNDaW_eA_3cr8M3ft0ZyhpO-G-TUqROI2gbo8LFm71RDmWOxNujqerePwgl2QkPn4kEHfzAEypUowHH6ZsM07IppG1PoPmJgYWR8C9S7yyiLJKtpwU)

15.  Download URLs

1.  This action downloads the files and saves them to Fronts![](https://lh6.googleusercontent.com/WId9Lq9dg6O8BXckHOGqcUR-NU-yGNuuEhixZ-un1WKulYaqFI7qaWKuAmUpv9mFYJpkKzn1Hc5KaQNEsbcquBHC9KMlexPYVUtbFJsOG92J_n0ca7GQBrhZ3eJquGtazpn7408)

17.  Start Screen Saver

1.  This action starts the screensaver![](https://lh5.googleusercontent.com/geLSrUSW22QMycvZsV5IFX6l_4iY_wtTNBEO_xYO7VqatD76ef8B-jm0266nAPuRj1b46BatzslEHDz7ej_F_cvSchiNU0f2vygzcqeV1hTIteXZrCP8vDHJPSUqZQIU0KeJyew)

Bravo! So, there you have it. : o ) Thanks, all!
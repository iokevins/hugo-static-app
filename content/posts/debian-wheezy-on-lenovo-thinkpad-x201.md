---
title: 'Debian Wheezy on Lenovo ThinkPad X201'
date: 2013-06-01T03:40:00.000-07:00
draft: false
tags: 
- linux
- debian
---

Pulling down the latest stable version of Debian Wheezy onto a new (to me) [Lenovo ThinkPad X201](http://en.wikipedia.org/wiki/ThinkPad_X_Series#X201).

  

Incidentally, to find my next laptop, I Google'd "best laptop 2010," found Laptop Magazine's [rankings](http://www.laptopmag.com/reviews/notebooks/best-notebooks-of-2010.aspx), chose the top business class laptop, then purchased it on eBay via [Buy It Now](http://www.ebay.com/sch/Laptops-Netbooks-/175672/i.html?LH_BIN=1&_sop=15&_from=R40&_nkw=x201&_dcat=177&rt=nc&LH_ItemCondition=3000). $400, with shipping and tax, so not bottom-end cheap, but I'd like to think it will last me for a few years. Incidentally, Laptop Magazine rated the 201s as the top choice, but the 201 sports roughly the same specs, differing in battery (6 vs. 9 cells, respectively) and CPU (i7 vs. i5, respectively), so I went for that since I found it for a reduced price. The one I purchased comes with a 128GB SSD, another personal-use first.

  

This represents my second attempt at installing Debian. I started the install this morning, selecting the "encrypted LVM" option. 

  

The first attempt, after I wiped Microsoft Windows 7 from the drive, failed while installing GRUB, with error similar to:

> grub-setup: Warn: Your core.img is unusually large. It won't fit the embedded area..  
> grubsetup: error: embedding not possible, but this is required for cross-disk install.

Turns out it seems to have something to do with the amount of space between sector 0 of the drive and the first sector of the partition. It was 32, I think, or 23, but I ended up using fdisk on the command line to change it to 2048, the default. This allowed me to get through the install.

  

When I attempted to boot, however, nothing happened, just a blinking underscore in the upper left. It also appears I had somehow overwritten the flash drive I had the Debian net install ISO on, as that also failed to work. I probably accidentally wrote GRUB to my flash drive, /dev/sdab, instead of to my SDD, /dev/sdaa : o P

  

This [document](https://dl.dropboxusercontent.com/u/40638984/how_to_lvm_debian_wheezy.pdf) assisted me with the second install, refreshing my memory a bit of Logical Volumes, Volume Groups, and so forth. Downloading all required files took about 45 mnutes, using the USC mirror.

  

I've used the XFCE Debian Wheezy install for the last month or two, and it's...well, I'm just not sure if I installed it right, so I'll leave it at that. With my old c. 2003 HP compaq nc6000 laptop, which does not support PAE, it really struggled with the new Wheezy OS. 

  

The Debian Wheezy install to the ThinkPad X201 failed the wiresless driver check. The first install I aborted immediately and loaded the drivers onto the USB thumb drive, but the second time I realized it wasn't needed, since I use the wired LAN.

  

Otherwise, much easier, overall, than the Debian Squeeze/Wheezy install to my HP compaq nc6000 laptop, which kept freezing. : o P

  

So, at 3:35 a.m. on Saturday morning, Debian Wheezy lives. : o )

  

I'll continue with customizing after I get more sleep.
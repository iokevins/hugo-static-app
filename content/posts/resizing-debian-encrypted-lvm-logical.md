---
title: 'Resizing Debian Encrypted LVM Logical Volumes'
date: 2016-05-15T23:17:00.000-07:00
draft: false
tags: 
- encrypted
- stretch
- disk
- linux
- storage
- gnu
- volume
- debian
- lvm
- logical
---

  

#### OVERVIEW

Running Debian Stretch (Testing) with an encrypted LVM, on a Lenovo ThinkPad X201 laptop, with a 128GB SSD.

  

When I installed the encrypted LVM, I believe I selected the following Debian installer options:

*   Partitioning method: Guided - use entire disk and set up encrypted LVM
*   Select disk to partition: /dev/sda
*   Partitioning scheme: Separate /home partition" (/, /home, swap)
*   I believe I selected the suggested defaults, for partition sizes

This produced the following partitioning scheme, as reported by utility **lsblk**:

> user@debian:/lib/live$ sudo lsblk  
> NAME                    MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINT  
> sda                       8:0    0 111.8G  0 disk  
> ├─sda1                    8:1    0   243M  0 part  
> ├─sda2                    8:2    0     1K  0 part  
> └─sda5                    8:5    0 111.6G  0 part  
>   └─crypt1              254:0    0 111.6G  0 crypt  
>     ├─bucket--vg-root   254:1    0   9.3G  0 lvm  
>     ├─bucket--vg-swap\_1 254:2    0   4.1G  0 lvm  
>     └─bucket--vg-home   254:3    0  98.1G  0 lvm  
> sdb                       8:16   1   7.5G  0 disk  /lib/live/mount/medium  
> loop0                     7:0    0   1.2G  1 loop  /lib/live/mount/rootfs/filesystem.squashfs

That is, an encrypted Logical Volume Manager (LVM) root (/) logical volume of ~10GiB and an LVM home (/home) logical volume of ~100GiB. 

#### PROBLEM

Unfortunately, the encrypted 10GB root logical volume filled up. So, the need arose to reduce the /home logical volume size, and expand the / root logical volume size.

  

I decided to expand the / (root) logical volume, by 15GiB, or 250%, and reduce the /home logical volume, by the same amount.

#### STEPS

*   Backup all data
*   Create a bootable Live media (we need to do this, when logical volumes not mounted):

*   [unetbootin](https://unetbootin.github.io/)
*   I used latest debian-live-8.4.0-amd64-gnome-desktop.iso (1.3GB; [link](http://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/); [via](https://www.debian.org/CD/live/))

*   Reboot into live media

*   Note: X201 laptop uses non-free wifi drivers; I USB tethered my mobile device, for network connectivity
*   If wifi preferred/needed, you can install non-free drivers, after adding non-free suffix to each line of /etc/apt/sources.list, via apt package firmware-iwlwifi

*   sudo apt-get update
*   Decrypt /dev/sda:

*   sudo apt-get install lvm2 cryptsetup
*   sudo modprobe dm-crypt
*   sudo cryptsetup luksOpen /dev/sda5 crypt1
*   Enter passphrase
*   sudo vgscan --mknodes
*   sudo vgchange -ay

*   Note: at this point, I unmounted the logical volumes, via the Nautilus file manager (select the eject button)
*   Verify filesystem integrity:

*   sudo e2fsck -f /dev/mapper/bucket--vg-root
*   sudo e2fsck -f /dev/mapper/bucket--vg-home

*   Reduce, then expand the logical volumes, concurrently resizing the filesystems:

*   sudo lvreduce --resizefs -L 83G /dev/mapper/bucket--vg-home
*   sudo lvextend --resizefs -l +100%FREE /dev/bucket-vg/root

This produced the following partitioning scheme, as reported by utility **lsblk**:

> k@bucket:~$ lsblk  
> NAME                    MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINT  
> sda                       8:0    0 111.8G  0 disk  
> ├─sda1                    8:1    0   243M  0 part  /boot  
> └─sda5                    8:5    0 111.6G  0 part  
>   └─sdb5\_crypt          254:0    0 111.6G  0 crypt  
>     ├─bucket--vg-root   254:1    0  24.4G  0 lvm   /  
>     ├─bucket--vg-swap\_1 254:2    0   4.1G  0 lvm   \[SWAP\]  
>     └─bucket--vg-home   254:3    0    83G  0 lvm   /home  
> sdb                       8:16   1   7.5G  0 disk  /media/k/DebianLiveUSB

That is, an encrypted Logical Volume Manager (LVM) root (/) logical volume of ~24GiB and an LVM home (/home) logical volume of ~83GiB. 

  

Reboot.

#### CAVEATS

*   GiB (always means powers of 2) != GB (ambiguous; might mean powers of 2, or powers of 10) ... know how each utility interprets these
*   This exercise did not expand or reduce the encrypted partition size, which greatly simplifies things
*   My /home logical volume was only 30% utilized; that is, lots of free space, to reduce
*   Backup all data; always worth repeating
*   By design, it's ok for the root logical volume to have non-contiguous physical storage allocations
*   If screen locks, during Debian live media session, user is "user" and password is "live"

#### RESOURCES

[https://help.ubuntu.com/community/ResizeEncryptedPartitions](https://help.ubuntu.com/community/ResizeEncryptedPartitions)

[https://blog.shadypixel.com/how-to-shrink-an-lvm-volume-safely/](https://blog.shadypixel.com/how-to-shrink-an-lvm-volume-safely/)

[https://debian-handbook.info/browse/stable/sect.installation-steps.html](https://debian-handbook.info/browse/stable/sect.installation-steps.html)  

  
  
  

Helpful tools:

*   system-config-lvm (note: special shout-out, to this graphical tool)
*   lvdisplay
*   fdisk -l
*   sfdisk -l
*   lsblk
*   lsblk -b
*   parted /dev/sda print all
*   tune2fs -l  /dev/mapper/bucket--vg-home
*   pvdisplay
*   pvs
*   vgs
*   lvs
*   vgdisplay
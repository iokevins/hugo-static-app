---
title: 'UEFI Ubuntu boot on Lenovo ThinkPad X1 Carbon'
date: 2015-04-13T19:49:00.000-07:00
draft: false
---

  

*   128GB SSD as internal primary
*   Removed recovery partition to thumb drive
*   Shrunk main partition by 20GB, to make room
*   Created partition from the free space (I think ?)
*   Downloaded Ubuntu Kylin 14.04.2 LTS
*   Used unetbootin to burn to thumb drive (another one)
*   Installed Ubuntu to the free partition...this went normally
*   Rebooted
*   No GRUB, went straight into Microsoft Windows 8.1
*   Ran the following command:

*   bcdedit /set {bootmgr} path \\EFI\\ubuntu\\grubx64.efi

*   Rebooted
*   Now GRUB appears and Ubuntu loads, but Microsoft Windows 8.1 boot manager failed to boot, with error 0xc000000e

  
  

Turns out BIOS was set to both UEFI and Legacy, with a preference for Legacy. Switching this to UEFI allowed Microsoft Windows 8.1 to load.

  

Loading into Ubuntu and running the following failed, the first time, because I had booted into Legacy mode:

*   sudo add-apt-repository ppa:yannubuntu/boot-repair  
*   sudo apt-get update
*   sudo apt-get install boot-repair
*   boot-repair 

So, I switched BIOS to use both UEFI and Legacy, but with a preference for UEFI. Then, I booted from the Ubuntu installer thumb drive. I selected Try Ubuntu, ran the above (after connecting to the wireless router), and voila, after following the instructions and using the defaults, a reboot now allows the choice of both.

  

RESOURCES

  

[https://help.ubuntu.com/community/Boot-Repair](https://help.ubuntu.com/community/Boot-Repair)

  

[http://askubuntu.com/questions/221835/installing-ubuntu-on-a-pre-installed-windows-8-64-bit-system-uefi-supported](http://askubuntu.com/questions/221835/installing-ubuntu-on-a-pre-installed-windows-8-64-bit-system-uefi-supported)

  

[http://windows.microsoft.com/en-us/windows/repartition-hard-disk#1TC=windows-7](http://windows.microsoft.com/en-us/windows/repartition-hard-disk#1TC=windows-7)

  

[http://askubuntu.com/questions/235567/windows-8-removes-grub-as-default-boot-manager](http://askubuntu.com/questions/235567/windows-8-removes-grub-as-default-boot-manager)

  

[https://help.ubuntu.com/community/UEFI#Converting\_Ubuntu\_into\_EFI\_mode](https://help.ubuntu.com/community/UEFI#Converting_Ubuntu_into_EFI_mode)
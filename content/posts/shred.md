---
title: 'Shred'
date: 2019-02-23T13:53:00.001-08:00
draft: false
tags: 
- shred
- debian
---

Quick notes on how to run shred on a Debian drive:  
  

1.  [Boot into single user mode](https://serverfault.com/a/482086)
2.  sudo umount -a -f
3.  [shred -v -z /dev/sdX](https://askubuntu.com/a/17650)
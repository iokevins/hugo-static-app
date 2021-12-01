---
title: 'Saturday Development Log'
date: 2008-08-02T14:03:00.000-07:00
draft: false
tags: 
- linux
- debian
---

Application development represents a game of inches.  

1.  Configured PDF viewing
2.  Installed and configured Subversion client kdesvn
3.  Installed IDE kdevelop--profiling and memory leak tools look promising. Will stick with Kate for now.
4.  Configured Konsole colors, font
5.  Added directory test and source file test/full-test.n.
6.  Added Makefile stubs in trunk using white-paper "Recursive Make Considered Harmful" [(http://www.xs4all.nl/~evbergen/nonrecursive-make.html](http://www.xs4all.nl/%7Eevbergen/nonrecursive-make.html)) as a guide.  
    
7.  Installed Adobe Flash: sudo apt-get install flashplugin-nonfree
8.  Installed Amarok: sudo apt-get install amarok
9.  Installed g++: sudo apt-get install g++
10.  Installed dlocate: sudo apt-get install dlocate (initialize before using each time with sudo update-dlocatedb)
11.  Installed libldap2-dev: sudo apt-get install libldap2-dev (and in doing so learned the value of finding which packages contain header files via [http://packages.debian.org/](http://packages.debian.org/))
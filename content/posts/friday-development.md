---
title: 'Friday Development'
date: 2008-08-08T18:10:00.000-07:00
draft: false
---

Friday:  

1.  Implementing [Jan's](http://ioctl.org/jan/bison/) suggested Bison/Flex C++ implementation that I discovered last night. Download [example.tar.gz](http://ioctl.org/jan/bison/example.tar.gz) failed to contain files referenced by the Makefile: validate.cc, update-individual-policy.cc, combine-multiple-policies.cc. Commented-out references to them (targets "validate", "update-individual-policy", "combine-multiple-policies", "validate.o", "update-individual-policy.o", and "combine-multiple-policies.o") and modified target all to read "all: scanner.o inifile.o parser.o dump.o". I also commented out "COPTS= -m64 -mcpu=ultrasparc". It compiles.
2.  Why don't GNU projects Bison and Flex figure out how to get compatible on C++ object implementation? It's really awful, in my opinion--it could be so much better.  
    
3.  Eluvium's "After Nature" from their album "Copia"
4.  Ludovico Einaudi's "Primavera" from their album "Divenire."
5.  Pachobel's Canon in WTF
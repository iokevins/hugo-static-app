---
title: 'Sunday Development Log'
date: 2008-08-03T16:21:00.000-07:00
draft: false
tags: 
- bison
- nonrecursive
- c++
- make
- compiler
- flex
- makefile
---

Sunday:  

1.  Finished reading the white paper "Recursive Make Considered Harmful"
2.  Consulted the Flex manual: http://flex.sourceforge.net/manual/
3.  Compiled small Flex program in anticipation of testing new non-recursive make harness.
4.  Discovered O'Reilly's online book "Managing Projects with GNU Make Managing Projects with GNU Make, Third Edition" at [http://oreilly.com/catalog/9780596006105/book/index.csp](http://oreilly.com/catalog/9780596006105/book/index.csp) , part of their [Open Book Project](http://www.oreilly.com/openbook/).
5.  It seems the nonrecursive harness uses implicit compiles for all the C files it encounters.
6.  Getting my head wrapped around the targets and dependencies of the nonrecursive make harness.
7.  Successfully modified the nonrecursive make harness so it compiles GNU Flex code into a binary.

Compiling Bison into a binary using the nonrecursive make harness represents the next step.  
  
With all this talk about nonrecursive make, one might get the wrong impression that I'm doing this solely to learn about it. In fact, I'm finishing up a summer project for my CSC-251 compiler class, which is why GNU Flex/Bison come into play.
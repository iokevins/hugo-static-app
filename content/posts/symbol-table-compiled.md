---
title: 'Symbol Table Compiled'
date: 2008-07-15T20:56:00.000-07:00
draft: false
tags: 
- compiler
---

Tonight I successfully compiled the bare-bones symbol table. The symbol table of a compiler maps high-level words (tokens) in the source language to internal symbols.  
  
I thought I compiled a test harness using the STL map last night but in reality I used std::map. g++ reports cryptic compile conflicts between the downloaded STL and std::map that seem like a namespace conflict. If I have time I plan to investigate--right now std::map meets my modest needs.  
  
One more RHCP song to close out the night: [http://youtube.com/watch?v=yuFI5KSPAt4](http://youtube.com/watch?v=yuFI5KSPAt4)
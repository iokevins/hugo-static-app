---
title: 'Java Debugger is Dumb'
date: 2009-10-17T10:41:00.000-07:00
draft: false
---

Took me about 15 minutes to realize the java bytecode compiler was not overwriting all my class files when I compiled with debugging information (-g) turned on.  
  
Removing all the class files, then recompiling worked.
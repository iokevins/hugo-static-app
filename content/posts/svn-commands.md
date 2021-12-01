---
title: 'svn commands'
date: 2008-04-28T21:34:00.000-07:00
draft: false
---

Rebuilding my repository tonight on KUbuntu. So I don't forget:  
  
Porting the repository:  

1.  svnadmin dump .subversion-repository > repo.dump
2.  cp repo.dump ~
3.  cd ~
4.  svnadmin create .subversion-repository
5.  svnadmin load .subversion-repository <>

To check out the project:  

1.  cd ~/src  
    
2.  svn co file:///home/schultkl/.subversion-repository/csc-251
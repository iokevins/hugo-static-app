---
title: 'Late Night Subversion'
date: 2008-08-01T21:48:00.000-07:00
draft: false
tags: 
- subversion
---

Recording for future use:  

1.  Create a Subversion repository: ubuntu:~/src/csc-251$ svnadmin create ///home/user/.subversion-repository
2.  Import the initial file hierarchy: ubuntu:~/src/csc-251$ svn import newlc file:///home/user/.subversion-repository/newlc -m "Initial import"
3.  Create a branch: ubuntu:~/src/csc-251$  svn copy file:///home/user/.subversion-repository/newlc/trunk file:///home/user/.subversion-repository/newlc/branches/my-branch
4.  Checkout the project: ubuntu:~/src/csc-251$ mkdir newlc && cd newlc && svn checkout file:///home/user/.subversion-repository/newlc/trunk && cd trunk  
    

Most notably, these commands seem to differ:  

*   ubuntu:~$ svnadmin create ///home/user/.subversion-repository
*   ubuntu:~$ svnadmin create .subversion-repository

Why? It's a horrible user experience, in my opinion.
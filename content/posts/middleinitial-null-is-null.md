---
title: 'MiddleInitial + NULL is NULL'
date: 2012-10-10T21:14:00.000-07:00
draft: false
---

I thought this represented a clever way to add an extra space to the end of a possibly NULL middle initial:  
  
ISNULL(MiddleInitial + ' ', '')  
  
If MiddleInitial is NULL, then any attempt to concatenate will also result in NULL, which will then trigger no space consumed.  
  
If MiddleInitial is not NULL, then you get the middle initial plus an extra space.  
  
Via: [http://stackoverflow.com/questions/2699833/combine-first-middle-initial-last-name-and-suffix-in-t-sql-no-extra-spaces](http://stackoverflow.com/questions/2699833/combine-first-middle-initial-last-name-and-suffix-in-t-sql-no-extra-spaces)
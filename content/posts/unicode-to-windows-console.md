---
title: 'Unicode to the Windows Console'
date: 2009-10-17T23:26:00.000-07:00
draft: false
---

Spent a lot of time refreshing my memory of Unicode this evening, trying to figure out how to get Unicode in Java to appear properly in the Windows console.  
  
Apparently, [native calls](http://illegalargumentexception.blogspot.com/2009/04/i18n-unicode-at-windows-command-prompt.html) to the Windows subsystem are suggested as the best way, but how can this be a good thing for a write-once, run-anywhere language?  
  
Running "chcp 65001" to select the Unicode code page for the console, and then executing the Java code as "java -Dfile.encoding=UTF-8 class" barfs all over my screen. The Unicode character I want to print comes out OK, but the rest seems broken.  
  
UPDATE:  
  
Apparently this works:  
  
System.console().writer().print("\\u2591");  
System.console().writer().flush();  
  
UPDATE #2:  
  
OK, this only works for code page #437. o\_O Time to call it a night. Will attempt to print my character tomorrow: [http://www.fileformat.info/info/unicode/char/2591/index.htm](http://www.fileformat.info/info/unicode/char/2591/index.htm)  
  
UPDATE #3:  
  
This link was informative: [http://stackoverflow.com/questions/1272032/java-utf-8-strange-behaviour](http://stackoverflow.com/questions/1272032/java-utf-8-strange-behaviour) . Perhaps it is because I am encoding some values and not others?
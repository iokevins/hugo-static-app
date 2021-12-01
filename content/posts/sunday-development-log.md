---
title: 'Sunday Development Log'
date: 2008-08-31T09:56:00.000-07:00
draft: false
---

Sunday:  

1.  Neat: [http://www.google.com/codesearch](http://www.google.com/codesearch)
2.  SymbolStorage maps Word Tokens to Identifiers.
3.  Flex maps strings to Word Tokens.
4.  Bison parses Word Tokens using a LALR engine.
5.  A way to convert "a\_class.ToString().c\_str()" to "a\_class.ToString()" for use in sprintf()--[statically allocate a fixed character buffer within ToString() and return a pointer to it](http://www.google.com/codesearch?hl=en&q=show:flMucq60xJA:BWMDAsO966w:Mg6E1QMpo_g&sa=N&ct=rd&cs_p=http://download.gna.org/xrilpoz/ri--main--0.2--patch-15.tar.gz&cs_f=ri--main--0.2--patch-15/ri.cc). No memory management, no extra class member variables, no repeat allocation. The only catch--this technique only works for predictable string lengths. For example, sprintf()'ing an integer into a string--2^64 fits into a null-terminated string of 21 bytes.  
      
    Unrestricted string lengths necessitate dynamic memory allocation.  
      
    Google [prohibits C++ streams](http://google-styleguide.googlecode.com/svn/trunk/cppguide.xml#Streams) (except for logging), which seems to rule out std::string--I haven't seen or thought of a way other than [std::ostringstream](http://www.parashift.com/c++-faq-lite/misc-technical-issues.html#faq-39.1).
---
title: 'GNU Assembler Documentation'
date: 2007-02-19T23:21:00.000-08:00
draft: false
---

Reading GNU assembler documentation this evening, and several bits of humor jumped out at me (emphasis mine):  

*   result, size and value are absolute expressions. This emits repeat copies of size bytes. Repeat may be zero or more. Size may be zero or more, but if it is more than 8, then it is deemed to have the value 8, compatible with other people's assemblers. The contents of each repeat bytes is taken from an 8-byte number. The highest order 4 bytes are zero. The lowest order 4 bytes are value rendered in the byte-order of an integer on the computer `as` is assembling for. Each size bytes in a repetition is taken from the lowest order size bytes of this number. Again, this bizarre behavior is compatible with other people's assemblers. [Link](http://www.gnu.org/software/binutils/manual/gas-2.9.1/html_chapter/as_toc.html#TOC91)  
    
*   Because `as` tries to assemble programs in one pass, new-lc may not be undefined. If you really detest this restriction we eagerly await a chance to share your improved assembler. [Link](http://www.gnu.org/software/binutils/manual/gas-2.9.1/html_chapter/as_toc.html#TOC112)

Believe me, this is funny stuff, relative to what I'm slogging through. ;)
---
title: 'Saturday Development Log'
date: 2008-08-09T10:54:00.000-07:00
draft: false
---

Saturday:  

1.  inifile-->newl\_parser
2.  inifileLexer-->newl\_lexer
3.  inifile\_driver-->newl\_driver
4.  nm views symbols of object files
5.  To remedy error "multiple definition of \`yyFlexLexer::yywrap()'", remove option %noyywrap--then manually redefine "int yyFlexLexer::yywrap() { return 1; }" in file lexer.ll. Flex defines yyFlexLexer::yywrap() in both %.cc and %.hh--the linker encounters multiple declarations if two objects (lexer.o and driver.o, for example, if driver.cc includes lexer.hh).
6.  Bond's "Duel" from the album "Born"
7.  Arvo Pärt's "An den Wassern zu Babel", from the album "Arbos"
8.  Yann Tiersen's "Le Moulin" from the album "Le Fabuleux Destin d'Amelie Poulain"
9.  parse() handles both char \* (filename) and std::istream (stdin) depending on the signature of the call.
10.  Max Richter's "Sarajevo" from his album "Memoryhouse"
11.  Completed fully object-oriented Flex+Bison simple calculator.
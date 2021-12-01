---
title: 'Sunday Development'
date: 2008-08-17T09:44:00.000-07:00
draft: false
---

Sunday:  

1.  Google's C++ style guide demands fprintf() over streams. Current inconsistency results in code like this: (\*a\_sibling\_iterator).first->ToString().c\_str()--Token.ToString() returns std::string.  
    
2.  Kasper Peeters' Tree(std::pair) might work as a syntax tree container class, but as a symbol storage container it fails to offer key-based retrieval through std::find(), even if nodes contain container std::pair. On a secondary note, it also seems to fail to support equality functor assignment at the time of declaration.  
    
3.  Researching the Standard Template Library's Associative Containers for alternatives--[std::map](http://en.wikipedia.org/wiki/Map_%28C%2B%2B_container%29) tests out acceptably.  
    
4.  Schwarz Stein's "Rise To Heaven" from their album "New Vogue Children"
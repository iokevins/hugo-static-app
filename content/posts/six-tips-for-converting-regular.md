---
title: 'Six Tips For Converting Regular Expressions to Minimized Deterministic Finite Automatons'
date: 2008-03-16T23:09:00.000-07:00
draft: false
---

Here are a few tips to make converting a  

1.  [regular expression](http://en.wikipedia.org/wiki/Regular_expression)\->
2.  [non-deterministic finite automaton](http://en.wikipedia.org/wiki/Nondeterministic_finite_state_machine) [(NFA)](http://en.wikipedia.org/wiki/Nondeterministic_finite_state_machine) with epsilon transitions->
3.  NFA without epsilon transitions->
4.  [deterministic finite automaton (DFA)](http://en.wikipedia.org/wiki/Deterministic_finite_automaton)\->
5.  minimized DFA

a bit easier:  

1.  Back-transfer accepting states all the way back--don't overlook any epsilon transitions
2.  Verify the NFA works as intended at each step of the process--if something seems amiss, it probably is.
3.  Maintaining neatness and order for lines between states helps minimize confusion.
4.  Grid/graph paper helps with drawing straight lines and uniform circles.
5.  Remove states inaccessible from the Start state only after eliminating all epsilon transitions to and from them.
6.  Use a mechanical pencil and a slab eraser to correct the mistakes  
    

I made every mistake in the book this evening working through the transformation of the regular expression (a+ba)\*b\* to a minimized DFA--but I don't mind, because my studies represent the time I want to make the mistakes--not during my upcoming midterm.  
  
Hope this helps in some small way.
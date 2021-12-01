---
title: 'L-Attributed, Top-Down-Parsable SDD Implementation of the McNaughton-Yamada-Thompson Algorithm'
date: 2008-05-17T14:49:00.000-07:00
draft: false
tags: 
- solution McNaughton Yamada Thompson algorithm 5.2.6 dragon book second edition nfa sdd l-attributed grammar
---

My solution to the 2nd edition Dragon Book's Exercise 5.2.6:  
  
Implement the McNaughton-Yamada-Thompson algorithm, which converts a regular expression into a nondeterministic finite automaton (NFA), by an L-attributed SDD on a top-down parsable grammar. Assume that there is a token char representing any character, and that char.lexval is the character it represents. You may also assume the existence of a function new() that returns a new state, that is, a state never before returned by this function. Use any convenient notation to specify the transitions of the NFA.  
  
Notes:  

1.  I use the characters '{' and '}' to delimit rules, and the rules end up taking the form "{ state-x -> symbol \-> state-y } ... { ... }".
2.  The symbol "||" means concatenation.  
    
3.  Concatenation ( T -> F Tsub1 ) represented a bit of confusion for me, since it "deletes" state Tsub1.Start from the automaton (the exercise doesn't allow for deletion). McNaughton-Yamada-Thompson write, "The accepting state of N(s) and the start state of N(t) are merged into a single state, with all the transitions in or out of either state."  
      
    My initial attempt, setting F.EndTransitions = F.EndTransitions || Tsub1.StartTransitions seems reasonable. Since state Tsub1.Start continues to exist, references to it in Tsub1.StartTransitions, Tsub1.InnerTransitions, or Tsub1.EndTransitions do not require modification.  
      
    Everything works because from F.End the automaton may remain in F, or transition to Tsub1. Once the automaton transitions to Tsub1, however, it never returns--no references in Tsub1 point to states in F. In practical terms, this means the automaton produced contains one extra state Tsub1.Start for every concatenation in the original regular expression.
4.  Adding epsilon transitions to Start or End states requires retaining the existing StartTransitions or EndTransitions, respectively.
5.  A PDF of this solution produced via LaTeX can be found [here](http://kevinschultz.com/dragon-book-5.2.6-proposed-solution.pdf).  
    

Proposed solution:  
  
S -> E  

1.  S.Start = E.Start
2.  S.End = E.End
3.  S.StartTransitions = E.StartTransitions
4.  S.EndTransitions = E.EndTransitions
5.  S.InnerTransitions = E.InnerTransitions

E -> T  

1.  E.Start = T.Start
2.  E.End = T.End
3.  E.StartTransitions = T.StartTransitions
4.  E.EndTransitions = T.EndTransitions
5.  E.InnerTransitions = T.InnerTransitions

E -> T '|' Esub1  

1.  E.Start = new()  
    
2.  E.End = new()  
    
3.  E.StartTransitions = "{ " || E.Start || " -> epsilon -> " || T.Start || " } { " || E.Start || " -> epsilon -> " || Esub1.Start || " }"
4.  E.EndTransitions = Nil
5.  T.EndTransitions = T.EndTransitions || "{ " || T.End || " -> epsilon -> " || E.End || " }
6.  Esub1.EndTransitions = Esub1.EndTransitions || "{ " || Esub1.End || " -> epsilon -> " || E.End || " }
7.  E.InnerTransitions = T.StartTransitions || T.InnerTransitions || T.EndTransitions || Esub1.StartTransitions || Esub1.InnerTransitions || Esub1.EndTransitions  
    

T -> F  

1.  T.Start = F.Start
2.  T.End = F.End
3.  T.StartTransitions = F.StartTransitions
4.  T.EndTransitions = F.EndTransitions
5.  T.InnerTransitions = F.InnerTransitions  
    

T -> F Tsub1  

1.  T.Start = F.Start
2.  T.End = Tsub1.End
3.  T.StartTransitions = F.StartTransitions
4.  T.EndTransitions = Tsub1.EndTransitions
5.  F.EndTransitions = F.EndTransitions || Tsub1.StartTransitions  
    
6.  T.InnerTransitions = F.InnerTransitions || F.EndTransitions || Tsub1.InnerTransitions  
    

F -> G  

1.  F.Start = G.Start
2.  F.End = G.End
3.  F.StartTransitions = G.StartTransitions
4.  F.EndTransitions = G.EndTransitions
5.  F.InnerTransitions = .InnerTransitions  
    

F -> G '\*' Fsub1  

1.  F.Start = new()
2.  F.End = Fsub1.End
3.  F.StartTransitions = "{ " || F.Start || " -> epsilon -> " || G.Start || " } { " || F.Start || " -> epsilon -> " || Fsub1.Start || " }"
4.  F.EndTransitions = Fsub1.EndTransitions  
    
5.  G.EndTransitions = G.EndTransitions || "{ " || G.End || " -> epsilon -> " || G.Start || " } { " || G.End || " -> epsilon -> " || Fsub1.Start || " }"
6.  F.InnerTransitions = G.StartTransitions || G.InnerTransitions || G.EndTransitions || Fsub1.StartTransitions || Fsub1.InnerTransitions  
    

G -> '(' E ')'  

1.  G.Start = E.Start
2.  G.End = E.End
3.  G.StartTransitions = E.StartTransitions
4.  G.EndTransitions = E.EndTransitions
5.  G.InnerTransitions = E.InnerTransitions  
    

G -> epsilon  

1.  G.Start = Nil
2.  G.End = Nil
3.  G.StartTransitions = Nil
4.  G.EndTransitions = Nil
5.  G.InnerTransitions = Nil  
    

G -> char  

1.  G.Start = new()
2.  G.End = new()
3.  G.StartTransitions = "{ " || G.Start || " -> " || char.lexval || " -> " || G.End || " }"
4.  G.EndTransitions = Nil
5.  G.InnerTransitions = Nil  
    

Comments, questions, concerns welcome.
---
### Comments:
#### Sadly, no.
[schultkl](https://www.blogger.com/profile/17049497132104803385 "noreply@blogger.com") - <time datetime="2011-03-19T18:49:13.902-07:00">Mar 6, 2011</time>

Sadly, no.
<hr />

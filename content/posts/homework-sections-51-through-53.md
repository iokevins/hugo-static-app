---
title: 'Homework, Sections 5.1 through 5.3'
date: 2008-06-08T17:33:00.000-07:00
draft: false
tags: 
- dragon book second edition
---

My solutions to the 2nd edition Dragon Book's Exercises for chapter five:  
  
5.1.1 a, b, c: Investigating GraphViz as a solution to presenting trees  
  
5.1.2: Extend the SDD of Fig. 5.4 to handle expressions as in Fig. 5.1:  

1.  L -> E N

1.  L.val = E.syn  
    

3.  E -> F E'

1.  E.syn = E'.syn
2.  E'.inh = F.val  
    

5.  E' -> + T Esubone'

1.  Esubone'.inh = E'.inh + T.syn
2.  E'.syn = Esubone'.syn  
    

7.  T -> F T'

1.  T'.inh = F.val
2.  T.syn = T'.syn  
    

9.  T' -> \* F Tsubone'

1.  Tsubone'.inh = T'.inh \* F.val
2.  T'.syn = Tsubone'.syn  
    

11.  T' -> epsilon

1.  T'.syn = T'.inh  
    

13.  E' -> epsilon

1.  E'.syn = E'.inh  
    

15.  F -> digit

1.  F.val = digit.lexval  
    

17.  F -> ( E )

1.  F.val = E.syn  
    

19.  E -> T

1.  E.syn = T.syn

5.1.3 a, b, c: Investigating GraphViz as a solution to presenting trees  
  
5.2.1: What are all the topological sorts for the dependency graph of Fig. 5.7?  

1.  1, 2, 3, 4, 5, 6, 7, 8, 9
2.  1, 2, 3, 5, 4, 6, 7, 8, 9
3.  1, 2, 4, 3, 5, 6, 7, 8, 9  
    
4.  1, 3, 2, 4, 5, 6, 7, 8, 9  
    
5.  1, 3, 2, 5, 4, 6, 7, 8, 9  
    
6.  1, 3, 5, 2, 4, 6, 7, 8, 9  
    
7.  2, 1, 3, 4, 5, 6, 7, 8, 9  
    
8.  2, 1, 3, 5, 4, 6, 7, 8, 9  
    
9.  2, 1, 4, 3, 5, 6, 7, 8, 9  
    
10.  2, 4, 1, 3, 5, 6, 7, 8, 9

5.2.2 a, b: Investigating GraphViz as a solution to presenting trees  
  
5.2.3: Suppose that we have a production A -> BCD. Each of the four nonterminals A, B, C, and D have two attributes: s is a synthesized attribute, and i is an inherited attribute. For each of the sets of rules below, tell whether (1) the rules are consistent with an S-attributed definition (2) the rules are consistent with an L-attributed definition, and (3) whether the rules are consistent with any evaluation order at all?  
  
a) A.s = B.i + C.s  

1.  No--contains inherited attribute
2.  Yes--"From above or from the left"
3.  Yes--L-attributed so no cycles

b) A.s = B.i + C.s and D.i = A.i + B.s  

1.  No--contains inherited attributes
2.  Yes--"From above or from the left"
3.  Yes--L-attributed so no cycles

c) A.s = B.s + D.s  

1.  Yes--all attributes synthesized
2.  Yes--all attributes synthesized
3.  Yes--S- and L-attributed, so no cycles

d)  

*   A.s = D.i
*   B.i = A.s + C.s
*   C.i = B.s
*   D.i = B.i + C.i

1.  No--contains inherited attributes
2.  No--B.i uses A.s, which depends on D.i, which depends on B.i (cycle)
3.  No--Cycle implies no topological sorts (evaluation orders) using the rules

5.2.4: This grammar generates binary numbers with a "decimal" point:  

1.  S -> L . L | L
2.  L -> L B | B
3.  B -> 0 | 1

Design an L-attributed SDD to compute S.val, the decimal-number value of an input string. For example, the translation of string 101.101 should be the decimal number 5.625. Hint: use an inherited attribute L.side that tells which side of the decimal point a bit is on.  

1.  S -> L . Lsubone

1.  L.inh = 0
2.  Lsubone.inh = -1
3.  S.val = L.syn + Lsubone.syn

3.  S -> L

1.  L.inh = 0
2.  S.val = L.syn

5.  L -> Lsubone B

1.  Lsubone.inh = L.inh + 1
2.  B.inh = L.inh
3.  L.syn = Lsubone.syn \* B.syn

7.  L -> B

1.  L.syn = B.syn \* 2^L.inh

9.  B -> 0 | 1

1.  B.syn = digit.lexval

5.2.5: Design an S-attributed SDD for the grammar and translation described in 5.2.4.  

1.  S -> L . Lsubone

1.  S.val = L.lhs + Lsubone.rhs  
    

3.  S -> L

1.  S.val = L.lhs

5.  L -> Lsubone B

1.  L.lhs = Lsubone.lhs + (2^L.lhs\_exponent \* B.val)
2.  L.rhs = Lsubone.rhs + (2^L.rhs\_exponent \* B.val)
3.  L.lhs\_exponent = Lsubone.lhs\_exponent + 1
4.  L.rhs\_exponent = Lsubone.rhs\_exponent - 1  
    

7.  L -> B

1.  L.lhs = 2^L.lhs\_exponent \* B.val
2.  L.rhs = 2^L.rhs\_exponent \* B.val
3.  L.lhs\_exponent = 0
4.  L.rhs\_exponent = -1  
    

9.  B -> 0 | 1

1.  B.val = digit.lexval

5.2.6: Link: [http://schultkl.blogspot.com/2008/05/solution-to-dragon-book-second-edition.html](http://schultkl.blogspot.com/2008/05/solution-to-dragon-book-second-edition.html)  
  
5.3.1: Below is a grammar for expressions involving operator + and integer or floating-point operands. Floating-point numbers are distinguished by having a decimal point.  

1.  E -> E + T | T
2.  T -> num . num | num

a) Give an SDD to determine the type of each term T and expression E.  

1.  E -> Esubone + T

1.  E.type = if (E.type == float || T.type == float) { E.type = float } else { E.type = integer }

3.  E -> T

1.  E.type = T.type

5.  T -> numsubone . numsubtwo

1.  T.type = float

7.  T -> num

1.  T.type = integer

b) Extend your SDD of (a) to translate expressions into postfix notation. Use the binary operator intToFloat to turn an integer into an equivalent float. Note: I use character ',' to separate floating point numbers in the resulting postfix notation. Also, the symbol "||" implies concatenation.  

1.  E -> Esubone + T

1.  E.val = Esubone.val || ',' || T.val || '+'

3.  E -> T

1.  E.val = T.val  
    

5.  T -> numsubone . numsubtwo  
    

1.  T.val = numsubone.val || '.' || numsubtwo.val  
    

7.  T -> num

1.  T.val = intToFloat(num.val)

5.3.2 Give an SDD to translate infix expressions with + and \* into equivalent expressions without redundant parenthesis. For example, since both operators associate from the left, and \* takes precedence over +, ((a\*(b+c))\*(d)) translates into a\*(b+c)\*d. Note: symbol "||" implies concatenation.

1.  S -> E

1.  E.iop = nil
2.  S.equation = E.equation

3.  E -> Esubone + T

1.  Esubone.iop = E.iop
2.  T.iop = E.iop
3.  E.equation = Esubone.equation || '+' || T.equation
4.  E.sop = '+'

5.  E -> T

1.  T.iop = E.iop
2.  E.equation = T.equation
3.  E.sop = T.sop

7.  T -> Tsubone \* F

1.  Tsubone.iop = '\*'
2.  F.iop = '\*'
3.  T.equation = Tsubone.equation || '\*' || F.equation
4.  T.sop = '\*'

9.  T -> F

1.  F.iop = T.iop
2.  T.equation = F.equation
3.  T.sop = F.sop

11.  F -> char  
    

1.  F.equation = char.lexval
2.  F.sop = nil

13.  F -> ( E )

1.  if (F.iop == '\*' && E.sop == '+') { F.equation = '(' || E.equation || ')' } else { F.equation = E.equation }
2.  F.sop = nil  
    

5.3.3: Give an SDD to differentiate expressions such as x \* (3\*x + x \* x) involving the operators + and \*, the variable x, and constants. Assume that no simplification occurs, so that, for example, 3\*x will be translated into 3\*1 + 0\*x. Note: symbol "||" implies concatenation. Also, differentiation(x\*y) = (x \* differentiation(y) + differentiation(x) \* y) and differentiation(x+y) = differentiation(x) + differentiation(y).  

1.  S -> E

1.  S.d = E.d

3.  E -> T

1.  E.d = T.d
2.  E.val = T.val

5.  T -> F

1.  T.d = F.d
2.  T.val = F.val

7.  T -> Tsubone \* F

1.  T.d = '(' || Tsubone.val || ") \* (" || F.d || ") + (" || Tsubone.d || ") \* (" || F.val || ')'
2.  T.val = Tsubone.val || '\*' || F.val

9.  E -> Esubone + T

1.  E.d = '(' || Esubone.d || ") + (" || T.d || ')'
2.  E.val = Esubone.val || '+' || T.val

11.  F -> ( E )

1.  F.d = E.d
2.  F.val = '(' || E.val || ')'

13.  F -> char  
    

1.  F.d = 1
2.  F.val = char.lexval

15.  F -> constant

1.  F.d = 0
2.  F.val = constant.lexval
---
### Comments:
#### For 5.3 1b, I think you should put the T.val first...
[KT](https://www.blogger.com/profile/10758892425972813275 "noreply@blogger.com") - <time datetime="2012-03-31T22:16:25.581-07:00">Mar 6, 2012</time>

For 5.3 1b, I think you should put the T.val first. Otherwise you may have something like 23+4. If you switch the order it will be 423+.
<hr />
#### For the following C assignment statements generate...
[nilima](https://www.blogger.com/profile/03355967435186526877 "noreply@blogger.com") - <time datetime="2021-04-22T07:40:27.316-07:00">Apr 4, 2021</time>

For the following C assignment statements generate three-address code, assuming that all array elements are integers taking four bytes each. Convert your three-address code into machine code for the machine. You may use as many registers as you need.  
a\[i\] = b\[c\[i\]\]; plz ans me
<hr />

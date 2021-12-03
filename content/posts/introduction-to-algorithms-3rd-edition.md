---
title: 'Introduction to Algorithms, 3rd edition - Chapter 2'
date: 2013-01-17T23:03:00.000-08:00
draft: false
tags: 
- algorithms
---

Switching to the third edition, just because.  
  
**Exercises**  
2.1-1  Using Figure 2.2 as a model, illustrate the operation of INSERTION-SORT on the array  = < 31, 41, 59, 26, 41, 58 >  

[![](/images/2.1-1640.png)](/images/2.1-1.png)

Note: solution produced via free tool [LucidChart](https://www.lucidchart.com/)  
  
2.1-2  Rewrite the INSERTION-SORT procedure to sort into nonincreasing instead of nondecreasing order.  
`  
INSERTION-SORT(_A_)  
1. **for** _j_ = 2 **to** _A_._length_  
2.   _key_ = _A_[_j_]  
3.   // Insert A[j] into the sorted sequence A[1..j - 1].  
4.   _i_ = _j_ - 1  
5.   **while** _i_ > 0 and _A_[_i_] < _key_  
6.     _A_[_i_ + 1] = _A_[_i_]  
7.     _i_ = _i_ - 1  
8.   _A_[_i_ + 1] = _key_`  
  
[](http://draft.blogger.com/blogger.g?blogID=17308164)2.1-3 Consider the **searching problem:**  

> **Input:** A sequence of _n_ numbers _A_ = < _a1_, _a2_, ..., _an_ > and a value _v_.  
> **Output:** An index _i_ such that _v_ = _A_\[_i_\] or the special value NIL if _v_ does not appear in _A_.

Write pseudocode for _linear search_, which scans through the sequence, looking for _v_. Using a loop invariant, prove your algorithm is correct.  
  
`LINEAR-SEARCH(_A_, _v_)  
1. _i_ = 1  
2. **while** _i_ <= _A_._length_  
3.   if _v_ == _A_[_i_]  
4.     **return** _i_  
5.   _i_ = _i_ + 1  
6. **return** NIL `  
  
**Loop invariant:** At the start of each iteration of the **while** loop of lines 2-5, the algorithm has yet to find value _v_ in subarray _A_\[1.._i_ - 1\], which represents the searched elements of array _A_.  
**Initialization:** We start by showing the loop invariant holds before the first loop iteration, when index _i_ = 1. Since the algorithm has yet to begin searching for value _v_, subarray _A_\[1.._i_ - 1\] correctly consists of zero elements and therefore cannot contain value _v_. Therefore, the loop invariant holds prior to the first iteration of the loop.  
**Maintenance:** Next, we tackle the second property: showing each iteration maintains the loop invariant. The body of the **while** loop tests whether value _v_ equals array element _A_\[_i_\] (line 3). If so, it exits with an output of index _i_. Otherwise, incrementing _i_ for the next iteration of the **while** loop preserves the loop invariant, as the algorithm will now have fruitlessly searched subarray _A_\[1.._i_ - 1\] for value _v_.  
**Termination:** Finally, we examine what happens when the loop terminates. Condition _i_ > _A.length = n_ causes the **while** loop to terminate. Since each loop iteration increases _i_ by 1, we must have _i_ = _n_ + 1 at that time. Substituting _n_ \+ 1 for _i_ in the wording of the loop invariant, we have the subarray _A_\[1.._n_\] consisting of the searched elements of array _A_. Observing subarray _A_\[1.._n_\] represents the entire array, we conclude _v_ does not exist in _A_. At this point, the algorithm returns the special value NIL. Hence, the algorithm is correct.  
  
2.1-4 Consider the problem of adding two _n_\-bit binary integers, stored in two _n_\-element arrays _A_ and _B_. The sum of the two integers should be stored in binary form in an (_n_ + 1)-element array _C_. State the problem formally and write pseudocode for adding the two integers.  
**Input:** A sequence of _n_ binary numbers _A_ = < _a1_, _a2_, ..., _an_ > and _B_ = < _b1_, _b2_, ..., _bn_ >, representing binary integers _A_ and _B_, with binary numbers _a1_ and _b1_ representing the least-significant bits of each sequence, respectively  
**Output:** A sequence of _n_ + 1 binary numbers _C_ = < _c1_, _c2_, ..., _cn_+1 > representing the sum of binary integers _A_ + _B_, with binary number _c1_ representing the least-significant bit  
  
`BINARY-SUM(_A_, _B_, _C_)  
1.  _carry_ = 0  
2.  **for** _i_ = 1 **to** _A_._length_  
3.    **if** (_A_[_i_] + _B_[_i_] + _carry_) == 3  
4.      _carry_ = 1  
5.      _C_[_i_] = 1  
6.    **elseif** (_A_[_i_] + _B_[_i_] + _carry_) == 2  
7.      _carry_ = 1  
8.      _C_[_i_] = 0  
9.    **elseif** (_A_[_i_] + _B_[_i_] + _carry_) == 1  
10.     _carry_ = 0  
11.     _C_[_i_] = 1  
12.   **else**  
13.     _carry_ = 0  
14.     _C_[_i_] = 0  
15. _C_[_i_] = _carry_`  
  
2.2-1 Express the function _n_^3 / 1000 - 100_n_^2 - 100_n_ + 3 in terms of Θ-notation  
  
Θ(n^3)  
  
2.2-2 Consider sorting _n_ numbers stored in array _A_ by first finding the smallest element of _A_ and exchanging it with the element in _A_\[1\]. Then find the second smallest element of _A_, and exchange it with _A_\[2\]. Continue in this manner for the first _n_ - 1 elements of _A_. Write pseudocode for this algorithm, which is known as _selection sort_. What loop invariant does this algorithm maintain? Why does it need to run for only the first _n_ - 1 elements, rather than for all _n_ elements? Give the best-case and worst-case running times of selection sort in Θ-notation.  
  
`SELECTION-SORT(_A_)`  
`1.  **for** _i_ = 1 **to** _A_._length_ - 1`  
`2.    _min_index_ = _i_`  
`3_._    **//** Find the smallest number in unsorted subarray _A_[_i_ + 1.._n_]`  
`4.    **for** _j_ = _i_ + 1 **to** _A_._length_  
5.      **if** _A_[_j_] < _A_[_min_index_]  
6.        _min_index _= _j_`  
`7_.    _**//** Exchange current and smallest unsorted element`  
`8_.    key_ = _A_[_i_]  
9.    _A_[_i_] = _A_[_min_index_]  
10.   _A_[_min_index_] = _key_  
`  
  
**Loop invariant:** At the start of each iteration of the **for** loop of lines 1-10, the subarray _A_\[1.._i_ - 1\] consists of the _i_ - 1 smallest elements of _A_, in sorted ascending order.  
  
It only needs to run for the first _n_ - 1 elements of _A_ because upon termination, index _i_ will equal (_A_._length_ - 1) + 1 = _n_. The loop invariant guarantees subarray _A_\[1.._n_ - 1\] will consist of the _n_ - 1 smallest elements of _A_ in sorted ascending order, which implies the remaining original element not only resides in _A_\[_n_\], but it also represents the _n_th smallest element of _A_.  
  
**Best and worst case:** SELECTION-SORT(_A_) performs the same, in terms of Θ-notation, regardless of input. For example, the algorithm executes the same number of steps with a sorted or reverse-sorted array as input.  
  
The algorithm runs in **Θ(n^2):** The outer loop takes _n_ - 1 iterations. The [inner loop](http://www.wolframalpha.com/input/?i=summation&a=*C.summation-_*Calculator.dflt-&f2=k&f=Sum.sumfunction_k&f3=1&f=Sum.sumlowerlimit_1&f4=n-1&x=11&y=9&f=Sum.sumupperlimit_n-1&a=*FVarOpt.1-_**-.***Sum.sumvariable---.*--) takes  
  

[![](/images/2.2-2_innerloop.gif)](/images/2.2-2_innerloop.gif)

  
iterations. Together, both outer and inner take  
  

[![](/images/2.2-2_inner_outer.gif)](/images/2.2-2_inner_outer.gif)

  

where _c_ equals the number of incidental, non-comment lines of code in SELECTIOTN-SORT. This [simplifies](http://www.wolframalpha.com/input/?i=simplify+1%2F2+*+%28n+-+1%29n+%2B+%28n+-+1%29+%2B+c) to

  

[![](/images/2.2-2_complexity.gif)](/images/2.2-2_complexity.gif)

  
which equals a running time of Θ(n^2).  
  
2.2-3 Consider linear search again (see [2.1-3](http://schultkl.blogspot.com/2013/01/introduction-to-algorithms-3rd-edition.html#213)). How many elements of the input sequence need to be checked on the average, assuming the element being searched for is equally likely to be any element in the array? How about in the worst case? What are the average-case and worst-case running times of linear search in Θ-notation? Justify your answers.  
  
On the average, assuming the element being searched for is equally likely to be any element in the array, LINEAR-SEARCH(_A_, _v_) will check the _i_\-th element of input sequence  

> _A_.length - (_i_ - 1) 

times. For example, if _A_.length == 100 and we call LINEAR-SEARCH(_A_, _v_) 100 times with the same inputs, it will, on the average, check element #1 100 times, element #2 99 times, element #3 98 times, and so forth, checking element #100 only 1 time. So, on average, we will check  

> (_A_.length + _A_.length-1 + _A_.length-2 + ... + 1) / _A_.length

[or](http://www.wolframalpha.com/input/?i=summation&a=*C.summation-_*Calculator.dflt-&f2=k%2Fn&x=12&y=11&f=Sum.sumfunction_k%2Fn&f3=1&f=Sum.sumlowerlimit_1&f4=n&f=Sum.sumupperlimit_n&a=*FVarOpt.1-_**-.***Sum.sumvariable---.*--)  

[![](/images/MSP26271a540iedb70hff7e000014cdh08g7b7a08h1.gif)](/images/MSP26271a540iedb70hff7e000014cdh08g7b7a08h1.gif)

  
So, on the average, assuming the element being searched for is equally likely to be any element in the array, LINEAR-SEARCH(_A_, _v_) will check  
  

[![](/images/MSP15911a5410g29ede96ci00004h21egca6ei4h2g9.gif)](/images/MSP15911a5410g29ede96ci00004h21egca6ei4h2g9.gif)

  
elements of the input sequence, or a little over one-half of all elements.  
  
In the worst case, when value _v_ matches the last element in _A_ (or matches no elements in _A_), LINEAR-SEARCH(_A_, _v_) will check **all** elements in _A_.  
  
Therefore, both on the average and in the worst case, LINEAR-SEARCH(_A_, _v_) runs in **Θ(n)** time. As _n_ represents the leading term in each case, given large enough array sizes, it dominates the order of growth calculation.  
  
2.2-4 How can we modify almost any algorithm to have a good best-case running time?  
  
We can modify almost any algorithm to have a good best-case running time by ensuring it runs in constant time for at least one input.  
  
2.3-1  
  
Using Figure 2.4 as a model, illustrate the operation of merge sort on the array _A_ = <3, 41, 52, 26, 38, 57, 9, 49>  
  

[![](/images/2.3-1640.png)](/images/2.3-1.png)

  
Note: solution produced via free tool [LucidChart](https://www.lucidchart.com/)  

  

  
2.3-2  
  
Rewrite the MERGE procedure so it does not use sentinels, instead stopping once either array _L_ or _R_ has had all its elements copied back to _A_ and then copying the remainder of the other array back into _A_.  
  
MERGE(_A_, _p_, _q_, _r_)  
`1.   _n_sub1 = _q_ - _p_ + 1`  
`2.   _n_sub2 = _r_ - _q_`  
`3.   let _L_[1.._n_sub1] and _R_[1.._n_sub2] be new arrays`  
`4.   **for** _i_ = 1 **to** _n_sub1`  
`5.     _L_[_i_] = _A_[_p_ + _i_ - 1]`  
`6.   **for** _j_ = 1 **to** _n_sub2`  
`7.     `_R_\[_j_\] = _A_\[_q_ + _j_\]  
`8.   _i_ = 1`  
`9.   _j_ = 1`  
`10.  _k_ = 1`  
11\.  **while** _n_sub1 > 0 **and** _n_sub2 > 0  
12\.    **if** _L_\[_i_\] <= _R_\[_i_\]  
13\.      _A_\[_k_\] = _L_\[_i_\]  
14\.      _i_ = _i_ + 1  
15\.      _k_ = _k_ + 1  
16\.      _n_sub1 = _n_sub1 - 1  
17\.    **else** _A_\[_k_\] = _R_\[_j_\]  
18\.      _j_ = _j_ + 1  
19\.      _k_ = _k_ + 1  

20\.      _n_sub2 = _n_sub2 - 1  

21\.  **if** _n_sub1 > 0

22\.    **do**

23\.      _A_\[_k_\] = _L_\[_i_\]

24\.      _k_ = _k_ + 1  

25\.      _i_ = _i_ + 1

26\.      _n_sub1 = _n_sub1 - 1

27\.    **while**_n_sub1 > 0  

28\.  **else**

29\.    **do\\**  
30\.      _A_\[_k_\] = _R_\[_j_\]  
31\.      _k_ = _k_ + 1  
32\.      _j_ = _j_ + 1  
33\.      _n_sub2 = _n_sub2 - 1  
34\.    **while** _n_sub2 > 0

  
2.3-3  
  
Use mathematical induction to show that when _n_ is an exact power of 2, the solution of the recurrence  
  

[![](/images/gif.gif)](/images/gif.gif)

  
is _T_(_n_) = _n_ lg _n_ (where lg = log base 2).  
  
**Base case**: Let _n_ = 2. Then _T_(_n_) = 2, which equals _T_(_n_) = _n_ lg _n_, as 2\*log2(2) = 2\*1 = 2.  
  
**Inductive step**: Assuming _T_(_n_) holds, for some unspecified value of _n_ where _n_ = ![](http://latex.codecogs.com/gif.latex?2^k) and _k_ > 1, we must show _T_(2_n_) holds, as 2_n_ represents the next valid input. In this case, ![](http://latex.codecogs.com/gif.latex?2n%20=%202^{k+1}).  
  
We want to show  

![](http://latex.codecogs.com/gif.latex?T(2n)%20=%202T(\frac{(2n)}{2})%20+%20(2n)%20=%20(2n)%20\lg({2n}))

  

This simplifies to 

![](http://latex.codecogs.com/gif.latex?T(2n)%20=%202T(n)%20+%20(2n)%20=%20(2n)%20\lg({2n}))

  

Since we assume _T_(_n_) holds, we substitute in _n _lg(_n_) for _T_(_n_), which results in 

![](http://latex.codecogs.com/gif.latex?T(2n)%20=%202(n\lg({n}))%20+%20(2n)%20=%20(2n)%20\lg({2n}))

  

Via associative and distributive properties, this simplifies to

  

![](http://latex.codecogs.com/gif.latex?T(2n)%20=%20(2n)(\lg{(n)}%20+%201)%20=%20(2n)\lg{(2n}))

Our proof only concerns cases in which _n_ represents a multiple of 2. Specifically, the case in which ![](http://latex.codecogs.com/gif.latex?2n%20=%202^{k+1}). Substituting ![](http://latex.codecogs.com/gif.latex?2^{k+1}) for 2_n_ and ![](http://latex.codecogs.com/gif.latex?2^k) for _n_ allows us to rewrite the formula as  
  

![](http://latex.codecogs.com/gif.latex?T(2^{k+1})%20=%20(2^{k+1})(\lg{(2^k)}%20+%201)%20=%20(2^{k+1})\lg{(2^{k+1}}))

  
Simplifying via logarithmic identify ![](http://latex.codecogs.com/gif.latex?\log_b{(b^x)}%20=%20x) reduces this to:  
  

![](http://latex.codecogs.com/gif.latex?T(2^{k+1})%20=%20(2^{k+1})(k%20+%201)%20=%20(2^{k+1})(k+1))

  
thereby showing inductive step _T_(2_n_) holds.  
  
Since both the basis and the inductive step have been proved, we have therefore proved _T_(_n_) holds for all _n_ where _n_ = ![](http://latex.codecogs.com/gif.latex?2^k) and _k_ >= 1. Q.E.D.  
  
2.3-4  
  
We can express insertion sort as a recursive procedure as follows. In order to sort _A_\[1.._n_\], we recursively sort _A_\[1.._n_ - 1\] and then insert _A_\[_n_\] into the sorted array _A_\[1.._n_ - 1\]. Write a recurrence for the running time of this recursive version of insertion sort.  
  
  
`INSERTION-SORT(_A_, _n_)  
1.  **if** _n_ > 2  
2.    INSERTION-SORT(_A_, _n_ - 1)`  
`3.  INSERT(_A_, `_n_ - 1, _A_\[_n_\])  
INSERT(_A_, _sorted\_end_, _el_)  
1\.   // Insert _el_ into the sorted sequence A\[1.._sorted\_end_\].  
2\.   // Assume total buffer equals _A_\[1.._sorted\_end_ + 1\], with  
3\.   // _el_ initially at _A_\[_sorted\_end_ + 1\]  
4\.   _i_ = _sorted\_end_  
5\.   **while**_i_ > 0 and _A_\[_i_\] > _el_  
6\.     _A_\[_i_ + 1\] = _A_\[_i_\]  
7\.     _i_ = _i_ - 1  
8\.   _A_\[_i_ + 1\] = _el_  
  

![](http://latex.codecogs.com/gif.latex?T(n)%20=%20\left\{%20\begin{array}{ll}%20\Theta(1)%20&%20\mbox{if%20}%20n%20=%201\mbox{%20},%20\\%20T(n-1)+\Theta(n)%20&%20\mbox{if%20}%20n%20%3E%201%20\mbox{%20.}%20\end{array}%20\right.)

  

As with the non-recursive insertion sort, a reverse-sorted array represents the worst-case scenario, while a sorted array represents the best-case scenario.

  
2.3-5  
  
Referring back to the searching problem (see [2.1-3](http://schultkl.blogspot.com/2013/01/introduction-to-algorithms-3rd-edition.html#213)), observe that if the sequence _A_ is sorted, we can check the midpoint of the sequence against _v_ and eliminate half of the sequence from further consideration. The _binary search_ algorithm repeats this procedure, halving the size of the remaining portion of the sequence each time. Write pseudocode, either iterative or recursive, for binary search. Argue ![](http://latex.codecogs.com/gif.latex?\Theta(\lg{n})) represents the worst-case running time of binary search.  
  
The iterative case:  
  

`  
BINARY-SEARCH(_A_, _v_)`  
`1.  _l_ = 1`  
`` `2.  _r_ = _A_._length_` ``  
`` `3.  **while** _l_ != _r_` ``  
`4.    `_mid_ = _l_ + CEILING((_r_ - _l)_ / 2)

5\.    **if** _v_ == _A_\[_mid_\]  
6\.      **return** _mid_`7.    **elseif** _v_ > _A_[_mid_]`  
`` `8.      _l = mid_` ``  
`` `9.    **else**` ``  
`` `10.     _r_ = _mid_` ``  
`` `11. **return** NIL ` ``  
  

  

`The recursive case:`

  

`` `BINARY-SEARCH(_A_, _v_)` ``

`` `1.  **return** `SEARCH(_A_, _v_, 1, _A_._length_)``

`` `  
SEARCH(_A_, _v_, _l_, _r_)` ``

``` `` `1.  **if** _l_ == _r_` `` ```

``` `` `2.    **return** NIL` `` ```

``` `` `3.  **else**` `` ```

``` `` `4.    ` ``_mid_ = _l_ + CEILING((_r_ - _l)_ / 2)```

```5.    **if** _v_ == _A_[_mid_]  
6.      **return** _mid_`` `7.    **elseif** _v_ > _A_[_mid_]` ``  
`` `8.      **return** SEARCH(_A_, _v_, _mid_, _r_)` ``  
`` `9.    **else**` ``  
`` `10.     ` ``**return** SEARCH(_A_, _v_, _l_, _mid_)```

  
  
We can express the recursive case with recurrence:  
  

![](http://latex.codecogs.com/gif.latex?T(n)%20=%20\left\{%20\begin{array}{ll}%20c%20&%20\mbox{if%20}%20l%20==%20r\mbox{%20or%20}%20v%20\mbox{%20found%20,}%20\\%20T(n/2)%20+%20c&%20\mbox{otherwise%20.}%20\end{array}%20\right.)

  

where the constant _c_ represents the time required to solve problems of size 1.

  

[![](/images/2.3-5320.png)](/images/2.3-5.png)

Note: solution produced via free tool [LucidChart](https://www.lucidchart.com/)

  
We can construct a recursion tree to see why BINARY-SEARCH runs in worst-case lg_ n_ time. In (a) and (b), above, we see _T_(_n_) progressively expanding. In (c), we see the fully expanded tree, which has lg_ n_ + 1 levels and each level contributes a total cost of _c_. The total cost, therefore, is _c _lg_ n_, which is ![](http://latex.codecogs.com/gif.latex?\Theta(\lg{n})).  
  
2.3-6  
  
Observe that the **while** loop of lines 5-7 of the INSERTION-SORT procedure in Section 2.1 uses a linear search to scan (backward) through the sorted subarray _A_\[1.._j_ - 1\]. Can we use a binary search (see Exercise 2.3-5) instead to improve the overall worst-case running time of insertion sort to ![](http://latex.codecogs.com/gif.latex?\Theta(n\lg%20n))?  
  
INSERTION-SORT(_A_)  
1. **for**_j_ = 2 **to**_A_._length_  
2\.   _key_ = _A_\[_j_\]  
3\.   // Insert A\[j\] into the sorted sequence A\[1..j - 1\].  
4\.   _i_ = _j_ - 1  
5\.   **while**_i_ > 0 and _A_\[_i_\] <_key_  
6\.     _A_\[_i_ + 1\] = _A_\[_i_\]  
7\.     _i_ = _i_ - 1  
8\.   _A_\[_i_ + 1\] = _key  ,'''''''''''''''''''_  
  

  
  
Previous - [Chapter one](http://schultkl.blogspot.com/2012/12/introduction-to-algorithms-2nd-edition.html)  
Next - Chapter three
---
### Comments:
#### please post chapter 3 too Today I have a paper tom...
[Yasir Habib](https://www.blogger.com/profile/06581189468431039185 "noreply@blogger.com") - <time datetime="2014-02-25T03:05:49.525-08:00">Feb 2, 2014</time>

please post chapter 3 too Today I have a paper tomorrow God Bless you
<hr />
#### Thank you, Yasir. I have not had the time to compl...
[schultkl](https://www.blogger.com/profile/17049497132104803385 "noreply@blogger.com") - <time datetime="2014-02-25T12:29:34.748-08:00">Feb 2, 2014</time>

Thank you, Yasir. I have not had the time to complete chapter three. Wishing you all the best.
<hr />
#### well if you could upload please 3.1-4 3.2-2 3.2-3 ...
[Yasir Habib](https://www.blogger.com/profile/06581189468431039185 "noreply@blogger.com") - <time datetime="2014-02-25T12:41:29.359-08:00">Feb 2, 2014</time>

well if you could upload please 3.1-4 3.2-2 3.2-3 3.2-6 3.2-7 upload it you will made my day so beautiful
<hr />

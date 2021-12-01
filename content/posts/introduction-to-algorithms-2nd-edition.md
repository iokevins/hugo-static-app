---
title: 'Introduction to Algorithms, 2nd edition - Chapter 1'
date: 2012-12-26T22:11:00.000-08:00
draft: false
---

**Notes**  
**1.1 Algorithms **  
Algorithm = Inputs -> Outputs (Specific procedure)  
  
Computational problem = desired I/O relationship (general)...an algorithm defines a _specific_ relationship  
  
Nondecreasing = same or greater  
  
Define computational problem by specifiying I/O  
  
Instance = One input  
  
Correct algorithm = halts on all inputs with correct output  
  
Correct algorithm **solves** a problem  
  
Specification = Precise description of guts  
  
"Incorrect algorithms can sometimes be useful"  
  
Problems solved by algorithms:  
  

*   Determining sequences (Human Genome Project)
*   Finding good routes; quickly find Internet pages
*   Negotiate and exchange electronic commerce
*   Allocate scarce resources

2-D -> 3-D mapping?

  

Given = inputs

Wish to find = outputs

  

Two common characteristics of algorithms:

1.  Many candidate solutions
2.  Practical applications

Data structure = store and organize data to facilitate access and modifications

  

Problems without published algorithms

  

Efficiency

  

Interesting NP-complete properties:

1.  it is unknown whether or not efficient algorithms exist
2.  If an efficient algorithm exists for any one of them, then efficient algorithms exist for all of them
3.  Several NP-complete problems are similar, but not identical, to problems for which we do not know of efficient algorithms

Real world NP-complete problems arise in real world

  

Traveling salesman

  

**1.2 Algorithms as a technology**

Terminates with correct answer

  

What if infinite speed and free memory?

  

Good software engineering practice = well designed and documented

  

Bounded resources (like computing time) should be used wisely

  

Algorithms are greater than hardware and software considerations

  

Insertion sort

  

Merge sort

  

Constant factors versus input sizes

  

Running time

  

Crossover point

  

Algorithms are important

  

Algorithms = core of contemporary technology

  

Algorithm knowledge technique = truly skilled programmer

  

  
**Definitions**  
  
  

*   [Concave polygon](http://en.wikipedia.org/wiki/Convex_and_concave_polygons) (one of the angles surpasses 180-degrees)
*   [Permutation](http://en.wikipedia.org/wiki/Permutation) (a rearranging of terms)
*   [Linear programming](http://en.wikipedia.org/wiki/Linear_programming) (Linear programming (optimization)  is a specific case of mathematical programming (mathematical optimization).
*   Graph
*   Product
*   Vertex
*   Associative
*   [Dynamic programming](http://en.wikipedia.org/wiki/Dynamic_programming) (a method for solving complex problems by breaking them down into simpler subproblems...The word dynamic was chosen by Bellman to capture the time-varying aspect of the problems, and because it sounded impressive.\[3\] The word programming referred to the use of the method to find an optimal program, in the sense of a military schedule for training or logistics. This usage is the same as that in the phrases linear programming and mathematical programming, a synonym for mathematical optimization.)
*   Constant not dependent on _n_
*   [Pipelining](http://en.wikipedia.org/wiki/Pipelining) (a set of data processing elements connected in series, so that the output of one element is the input of the next one)
*   [Superscalar](http://en.wikipedia.org/wiki/Superscalar) (a form of parallelism called instruction level parallelism within a single processor. It therefore allows faster CPU throughput than would otherwise be possible at a given clock rate. A superscalar processor executes more than one instruction during a clock cycle by simultaneously dispatching multiple instructions to redundant functional units on the processor.)

  
  
**Exercises 1.1**  
  
1.1-1 Give a real world example in which one of the following computational problems appears: sorting, determining the best order for multiplying matrices, or finding the convex hull.  
  

*   Sorting

*   Sorting files in a directory by creation date
*   Sorting various paper denominations of money
*   Sorting tax return forms by form ID number

*   Determining the best order for multiplying matrices

*   ???

*   Finding the convex hull

*   Identifying area of forest burned by fire

  
1.1-2 Other than speed, what other measures of efficiency might one use in a real-world setting?  
  

*   Storage requirements during runtime
*   Power consumption
*   Size of hardware
*   Size of software at rest

  
1.1-3 Select a data structure you have seen previously and discuss its strengths and limitations.  
Stack  
  

*   Strengths

*   Simple to implement: two operations, push and pop
*   Push and pop operate in constant time

*   Limitations

*   Not elegant way to traverse elements, since have to pop and store elsewhere in order to inspect and preserve order

  
1.1-4 How are the shortest-path and traveling-salesman problems given above similar? How are they different?  
  

*   Same

*   Both want shortest path, per constraints
*   Both seem like NP-complete problems

*   Differences

*   Traveling-salesman requires begin and end at same node
*   Shortest-path goes point-to-point

  
1.1-5 Come up with a real-world problem in which only the best solution will do. Then come up with one in which a solution that is "approximately" the best is good enough.  
  

*   Only the best solution

*   Note: best means no cutting corners, not necessarily "perfection"
*   Everything comes down to acceptable tolerances, in the real world
*   Typically, anything involving human safety in life and death situations

*   Space station airlocks (opening and closing)
*   Airplane auto-pilot systems
*   Traffic control systems (for example, traffic lights)

*   Financial transactions

*   ATM

*   Approximately the best is good enough

*   Pretty much everything else ; o )
*   Point-to-point driving when time not of the essence...probably OK to get reasonably close to a location and then figure out parking, eating, and so forth
*   Pouring a beer...OK to have a bit of foam at the top

**Exercises 1.2**

  

1.2-1 Give an example of an application that requires algorithmic content at the application level, and discuss the function of the algorithms involved.

> Section 1.1 of this book defines an algorithm as "any well-defined computational procedure that takes some value, or set of values, as _input_ and produces some value, or set of values, as _output_." Given this broad definition, I suggest the example of a web-based [SQL formatter](http://www.dpriver.com/pp/sqlformat.htm). As input, it takes a sequence of characters representing a SQL query. As output, it produces formatted SQL code, per constraints specified by the user. The algorithm functions as a set of rules which transform the input into the output based on the constraints specified by the user. For example, if the user selects "DB2" SQL as the input and C# as the output, the algorithm logic would transform the inputs into outputs conforming to C# rules.

  

1.2-2 Suppose we are comparing implementations of insertion sort and merge sort on the same machine. For inputs of size _n_, insertion sort runs in 8_n_^2 steps, while merge sort runs in 64_n_lg_n_ steps. For which values of _n_ does insertion sort beat merge sort?

> We wish to find the greatest value of n for which 8n^2 < 64nlgn. Since this seems to represent a transcendental function, I have elected to plug and chug to arrive at the answer. I used OpenOffice.org Calc to calculate the results below:  
> 
> *   When n = 2, we have 8(4) < 64(2)(1) => 32 < 128, which is true.
> 
> *   When n = 4, we have 8(16) < 64(4)(2) => 128 < 512, which is true.
> 
> *   and so forth, until n = 44, when we have 15,488 < 15373.8, which is false
> 
> Therefore, in this particular implementation, insertion sort beats merge sort for values of 2 <= n <= 43.

1.2-3 What is the smallest value of _n_ such that an algorithm whose running time is 100_n_^2 runs faster than an algorithm whose running time is 2^_n_ on the same machine?

> We wish to find the smallest value of n for which 100n^2 < 2^n. Since this seems to represent a transcendental function, I have elected to plug and chug to arrive at the answer. I used OpenOffice.org Calc to calculate the results below:  
> 
> *   When n = 1, we have 100(1) < 2^1 => 100 < 2, which is false.
> 
> *   When n = 2, we have 100(4) < 2^2=> 400 < 4, which is false.
> 
> *   and so forth, until n = 15, when we have 22,500 < 32,768, which is true
> 
> Therefore, in this particular implementation, the algorithm with running time 100(n^2) runs faster than the algorithm with running time 2^n for values of n >= 15.

**Problems**  
  
1-1 Comparison of running times  
For each function f(n) and time t in the following table, determine the largest size n of a problem that can be solved in time t, assuming that the algorithm to solve the problem takes f(n) microseconds.  
  
Note: I found this problem statement confusing, initially. The authors treat the computational problem and algorithm as a black box. The black box can solve an input of n items in f(n) microseconds. The authors ask the reader to calculate the largest size n the black box can solve on or before various times (t). For example, for f(n) = n, the black box can solve an input of 1 item in f(1) = 1 microsecond and 2 items in f(2) = 2 microseconds.  
  
We first convert the times in the header row into microseconds (one [microsecond](http://en.wikipedia.org/wiki/Microsecond) = 1/1,000,000 of a second):  

*   1 second = 1 \* 10^6 or 1,000,000 microseconds
*   1 minute = 6 \* 10^7 or 60,000,000 microseconds
*   1 hour = 3.6 \* 10^9 or 3,600,000,000 microseconds
*   1 day = 8.64 \* 10^10 or 86,400,000,000 microseconds
*   1 month = 2.592 \* 10^12 or 2,592,000,000,000 microseconds (assuming 30 days per month, on average)
*   1 year = 3.15576 \* 10^13 or 31,557,600,000,000 microseconds (assuming 365.25 days per year)
*   1 century = 3.15576 \* 10^15 or 3,155,760,000,000,000 microseconds

Second, for each cell, we need to calculate the largest size n the black box can solve on or before the specified number of microseconds:  
  

  

Notes

1 second

1 minute

1 hour

1 day

1 month (assume 30 days, on average)

1 year (assume 365.25 days)

1 century

lg(n)

Put both sides on base 2; this converts 2^lg(n) to n.

2^(1 \* 10^6)

2^(6 \* 10^7)

2^(3.6 \* 10^9)

2^(8.64 \* 10^10)

2^(2.592 \* 10^12)

2^(3.15576 \* 10^13)

2^(3.15576 \* 10^15)

sqrt(n)

Squaring both sides solves for n.

(1 \* 10^6)^2 = 1 \* 10^12

(6 \* 10^7)^2 = 3.6 \* 10^15

(3.6 \* 10^9)^2 = 1.296 \* 10^19

(8.64 \* 10^10)^2 = 7.46496 \* 10^21

(2.592 \* 10^12)^2 = 6.718464 \* 10^24

(3.15576 \* 10^13)^2 = 9.9588211776×10^26

(3.15576 \* 10^15)^2 = 9.9588211776×10^30

n

1 \* 10^6

6 \* 10^7

3.6 \* 10^9

8.64 \* 10^10

2.592 \* 10^12

3.15576 \* 10^13

3.15576 \* 10^15

nlg(n)

Put both sides as an exponent on base 2; since nlg(n) = lg(n^n), this converts 2^(lg(n^n)) to n^n. Transcendental...so we have to do things the hard way.

6.2746 \* 10^4 ([link](http://www.wolframalpha.com/input/?i=solve+n%5En+-+2%5E%2810%5E6%29+%3D+0))

2.801417 \* 10^6 ([link](http://www.wolframalpha.com/input/?i=solve+%28n*+log%5B2%2C+n%5D%29+-+%286+*+10%5E7%29+%3D+0) to get approximation, then manual refinement)

1.33378058 \* 10^8 ([link](http://www.wolframalpha.com/input/?i=solve+%28n*+log%5B2%2C+n%5D%29+-+%283.6+*+10%5E9%29+%3D+0) to get approximation, then manual refinement)

2.755147513 \* 10^9 ([link](http://www.wolframalpha.com/input/?i=solve+%28n*+log%5B2%2C+n%5D%29+-+%288.64+*+10%5E10%29+%3D+0) to get approximation, then manual refinement)

7.1870856404 \* 10^10 ([link](http://www.wolframalpha.com/input/?i=solve+%28n*+log%5B2%2C+n%5D%29+-+%282.592+*+10%5E12%29+%3D+0) to get approximation, then manual refinement)

7.98161 \* 10^11 ([link](http://www.wolframalpha.com/input/?i=solve+%28n*+log%5B2%2C+n%5D%29+-+%283.15576+*+10%5E13%29+%3D+0) to get approximation, then manual refinement)

6.86565x10^13 ([link](http://www.wolframalpha.com/input/?i=solve+%28n*+log%5B2%2C+n%5D%29+-+%283.15576+*+10%5E15%29+%3D+0) to get approximation, then manual refinement)

n^2

Taking the square root of both sides solves for n.

sqrt(1 \* 10^6) = 1 \* 10^3 or 1,000

sqrt(6 \* 10^7) = 7.745966692 \* 10^3 or 7,745

sqrt(3.6 \* 10^9) = 6 \* 10^4 or 60,000

sqrt(8.64 \* 10^10) = 2.939387691 \* 10^5 or 293,938

sqrt(2.592 \* 10^12) = 1.609968944 \* 10^6 or 1,609,968

sqrt(3.15576 \* 10^13) = 5.617615152357805 \* 10^6 or 5,617,615

sqrt(3.15576 \* 10^15) = 5.617615152357 × 10^7 or 56,176,151

n^3

Taking the cube root of both sides solves for n.

cuberoot(1 \* 10^6) = 1 \* 10^2 or 100

cuberoot(6 \* 10^7) = 3.914867641×10^2 or 391

cuberoot(3.6 \* 10^9) = 1.532618865×10^3 or 1,532

cuberoot(8.64 \* 10^10) = 4.420837798×10^3 or 4,420

cuberoot(2.592 \* 10^12) = 1.373657091×10^4 or 13,736

cuberoot(3.15576 \* 10^13) = 3.1601×10^4 or 31,601

cuberoot(3.15576 \* 10^15) = 1.46679335×10^5 or 146,679

2^n

Taking lg of both sides solves for n.

log(1 \* 10^6) / log(2) = 1.993156857×10^1 or 19

log(6 \* 10^7) / log(2) = 2.583845916×10^1 or 25

log(3.6 \* 10^9) / log(2) = 3.174534976×10^1 or 31

log(8.64 \* 10^10) / log(2) = 3.633031226×10^1 or 36

log(2.592 \* 10^12) / log(2) = 4.123720286×10^1 or 41

log(3.15576 \* 10^13) / log(2) = 4.484305×10^1 or 44.84305

log(3.15576 \* 10^15) / log(2) = 5.1486909×10^1 or 51

n!

Plug and chug...[Wolfram Alpha](http://www.wolframalpha.com/input/?i=solve+17%21+-+%283.15576+*+10%5E15%29) helps

9

11

12

13

15

16

17
---
### Comments:
#### How was that n solved for (nlgn), when computing r...
[Uma G](https://www.blogger.com/profile/06340801835348066681 "noreply@blogger.com") - <time datetime="2013-12-14T00:09:12.711-08:00">Dec 6, 2013</time>

How was that n solved for (nlgn), when computing running times in the problem 1-1. You have provided with a link but what expression to be given over there.  
Need help. Thank you.
<hr />
#### Hii, I think you should equal 1000,000 to the (nlo...
[YashSharmaBharatpur](https://www.blogger.com/profile/02587514415952076302 "noreply@blogger.com") - <time datetime="2021-01-23T09:29:58.664-08:00">Jan 6, 2021</time>

Hii, I think you should equal 1000,000 to the (nlog n) and then solve it to find the answers. 1000000 for only 1 second.
<hr />

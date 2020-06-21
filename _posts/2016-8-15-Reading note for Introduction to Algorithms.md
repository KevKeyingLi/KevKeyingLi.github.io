# Reading note for Introduction to Algorithms



## Foundations

## and Order Statistics

## Data Structures

## Advanced Design and Analysis Techniques

### Dynamic Programming
DP is typically used for solving optimization problems, there are basically four steps:
* Characterize the structure of an optimal solution
* Recursively define the value of an optimal solution
* compute the value of an optimal solution, typically in a bottom-up fashion(top-down memoization is also usable some times)
* Construct an optimal solution from the computed information(Interview questions might not need this)
## 15.1 Rod cutting problem
Rod cutting problem exhibits **optimal substructure**: optimal solution to a problem incorpporate optimal solution to related **subproblems**, which we may solve **independently**. 

The biggest benefit of DP is to reduce the overlapping/wasted computations. Basically two ways
* top-down memoization: recursive way, but stores information when backtracking
* bottom up memorization: iterative way usually, going through all unique sub problems. 

DP is an example of *time-memory tradoff*

A DP approach runs in polynomial time when the number of distinct subproblems involved is polynomial in the input size and we can solve each such subproblem in polynomial time.

In **Bottom-up method**, we sort the subproblems by size and solve them in size order, smallest first. 

In some cases, top-down method might be faster than bottom up solution, since some subproblems that the latter computed, might not be used in constructing final solution.
### Sub problem graph
Sub problem graph
## 15.2 Parenthesis Matrix Chain Multiplication


## My thinking after these two examples:
### On their difference:
* Why rod cutting is cutting off one piece every time while matrix multiplication, splits the problem into two subproblems?
* What if each cut has a cost for *rod cutting*
* What is the difference of their representation? Why
    - rod cutting only need to keep track of one index to identify the sub problem, while matrix multiplication, uses two indices to keep track of which problem is tracked.
    - This indicates the space/time complexity of the solution
    - **Representation of the problem determines the complexity of the problem**

### Another way to think about it:
The book gives us a quite standard way to think about this problem:
* Optimal structure of problems and subproblems, first break down the optimal problem into combination of smaller **Independent** optimal subproblems. 
* Use spcae to assist computation, and reduce redundant compuation

I am thinking may be we can think it in a different way, just for fun. When you are givin a optimization problem:
* first start off think from the smallest problems, base situations. 
* Solve every base problems, and to see if you could, combine that information to build up a solution for second level problem. 
* Keep going from there...

This way of thinking follows the same step of the bottom up method:
* Rod - cutting, build a tabular that comtains all possible lengths, from the shortest possible, and grow one step at a time.
* Parenthesize Matrix Multiplication: Start off compute the cost of multiplying all matrix pairs, then triplets, then for consecutive matrixs...Each step built on the previous. 

Also, consider the all possible solution for these problems, the number of all possible solution is usually exponential, but by computing the small element and build the solution bottom up, will avoid overlapping compuatioin


### Greedy Aglorithms

### Amortized Analysis

## Advanced Data Structures

(trees Sets)

## Graph Algorithms

### 22 Elementary Graph Algorithms

### 23 Minimum Spanning Tree

### 24 Single-Source Shortest Paths 643

####24.1 The Bellman-Ford algorithm 651

####24.2 Single-source shortest paths in directed acyclic graphs

#### 24.3 Dijkstra’s algorithm 658

####24.4 Difference constraints and shortest paths 664

#### 24.5 Proofs of shortest-paths properties 671

### 25 All-Pairs Shortest Paths 684

#### 25.1 Shortest paths and matrix multiplication

#### 25.2 The Floyd-Warshall algorithm 693

#### 25.3 Johnson’s algorithm for sparse graphs

### 26 Maximum Flow 708

#### 26.1 Flow networks 709

#### 26.2 The Ford-Fulkerson method 714

#### 26.3 Maximum bipartite matching 732



## Selected Topics


Status: #LectureNote
Tags: [[AlgoDat]]

# AlgoDat2-Greedy-Strategies-and-Approximation-Algorithms

### What are greedy algorithms?
```ad-info 
title: Idea of Greedy algorithms
These find the *best local solution* while hoping for an optimal global solution.

Often following the scheme of processing a sequence of elements in a carefully chosen order.
```
```ad-example
title: Usecases for Greedy algorithms
1. Usually applied to optimization problems
2. Usually the solution is not reconsidered
3. Results are not always optimal, sometimes just approximations

Eg. predecessor of [[AlgoDat1-Max-Flow#^ford-fulkerson|Ford-Fulkerson algorithm]]
```
### What are approximation algorithms?
```ad-info
title: Idea of Approximation Algorithms
These don't find an optimal solution but approximate it. Used if it's hard to compute the optimal solution.

**Aim:** Find a *near optimal* solution that is *within a certain factor* of the optimal solution and terminates in *polynomial time.*
```

---
tags:
  - dynamic-programming
---
## How To
1. High level question
	1. Decompose the problem into small problems
	2. Finite set of possible answers
	3. For any answer, the task looks like the original
2. Set up proper notation
	1. $G$-function: Stores answers to subproblems
	2. Variables, recurrence, base cases
3. Analysis: DP runtimes are almost always of the form $$\text{(\# sub-problems)}\cdot\text{(time per sub-problem)}$$
## Top-Down vs. Bottom-Up

There are two general paradigms under which dynamic programming is actually implemented. In the top-down case, we ask the final question we're looking for, then recursively solve sub-problems as needed, saving the answers as we go. This is called **memoization**.

In the bottom-up approach, we determine an order for the subproblems such that by the time we reach the final question we're asking, we'll already have computed all the subproblems we need to get our result. This is called **tabulation.** Typically, we start at the base case and go up.

## Optimal Substructure

The notion of optimal substructure is the implicit foundation of dynamic programming. In general, we've shown that dynamic programming problems can be broken down into something of the form 
$$G(i)=f(G(j)), j<i$$
Implicitly, this means that the solution to a problem can be solved by the optimal solutions to smaller subproblems. 
### When Optimal Substructure Fails

Consider the following problem:

>[!problem]
>**Input:** A directed graph $G$, a start vertex $s$, and an end vertex $t$.
>
>**Output:** The longest path in $G$ from $s$ to $t$.

A plausible DP-style approach would be asking the question, Does the path go through $v$ (the subproblem would then be the longest path from $s$ to $v$, then the longest path from $v$ to $t$? This fails, however, because when these paths are computed independently, some edges could be repeated. 

## Example: Number of Paths in Grid

>[!problem]
>**Input:** An $n\times m$ grid
>
>**Output:** The number of paths from the bottom left to the top right, where in each step we can either go one step up or one step to the right. 

Let $P(n, m)$ denote this solution. Then, we can say $$P(n,m)=P(n-1,m)+P(n,m-1)$$That is, the sum of recursive calls depending on whether we step up or to the right.

Using dynamic programming, we can store the values for each square so that we don't re-do work for the same positions. Then, our answer runs in $O(nm)$ time.
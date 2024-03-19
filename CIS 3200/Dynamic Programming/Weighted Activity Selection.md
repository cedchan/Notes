---
tags:
  - dynamic-programming
Date:
---
## Optimization

>[!problem]
>**Inputs:**
>- $S$: set of possible solutions
>- $f:S\mapsto\mathbb R$: an objective function that assigns a "cost" to each solution
>- $K\subset S$: a set of solutions that satisfy constraints on the solution space
>  
>**Output:** $\underset{x\in K\subset S}{\min/\max\,} f(s)$

## Problem Description

>[!problem]
>You are the owner of a concert hall.
>
>**Inputs:**
>- Performances $1,\dots,n$, each with
>	- Start time $s_i$
>	- End time $t_i$
>	- Price $p_i$ they are willing to pay for the space
>
>**Output:** Set of performers to rent out the space to such that you maximize the total amount of rent collected.

In the language of optimization, we can rewrite this problem as follows:
- Solution space $S$: subsets of performers
- $f: S\mapsto \mathbb R: f(s)=\sum_{i\in S}p_i$
- $K$ constraints: performers in $S$ should not overlap

And in more typical problem format:
- Inputs: $(s_1, t_1, p_1), \dots, (s_n, t_n, p_n)$
- Output: Subset $S\subset[n]$ s.t. (1) performers don't overlap, and (2) $\max\sum_{i\in S}p_i$

## Divide-and-Conquer Solution

${\rm A\small LG}(\{(s_i,t_i,p_i)\}_{i\in[n]})$ (assume inputs are sorted w.r.t. $s_i$)
1. Find $j(1)$, the smallest start time after $t_1$
2. $c_1\gets {\rm A\small LG}(\{(s_i,t_i,p_i)\}_{i\in[j(1)..n]})$
3. $c_2\gets {\rm A\small LG}(\{(s_i,t_i,p_i)\}_{i\in[2..n]}$
4. Output $\max(c_1+p_1, c_2+p_2)$

### Runtime

Finding $j(1)$, given that the inputs are sorted, stakes $O(\log n)$ time. Then, the recursive calls yield the following recurrence:
$$\begin{align}
T(n)&=O(\log n)+T(n-j(1))+T(n-1)\\
&\geq O(1)+2T(n-1) \\
&=O(2^n)
\end{align}$$

Even though we've divided, we're still getting the same runtime as brute force.

## Dynamic Programming Solution

The key observation is that in the divide and conquer solution, we're re-calculating the same subproblems over and over again. Specifically, all subproblems on $i\in[j(x)..n]$ will be among $[1..n],[2..n], \dots, [n..n]$. Then, we can speed up the algorithm by storing the results for these subproblems.

Let the array where we store these results be called $G$, where $G[i]$ corresponds to the output on $\{(s_i,t_i,p_i)\}_{i\in[j..n]}$.

${\rm A\small LG}(\{(s_i,t_i,p_i)\}_{i\in[n]})$ (assume inputs are sorted w.r.t. $s_i$)
1. Find $j(1)$, the smallest start time after $t_1$
2. Check if $G[j(1)]$ is non null. If so,
	1. $c_1\gets {\rm A\small LG}(\{(s_i,t_i,p_i)\}_{i\in[j(1)..n]})$
3. Otherwise, $c_1\gets G[j(1)]$
4. Check if $G[2]$ is non null. If so,
	1. $c_2\gets {\rm A\small LG}(\{(s_i,t_i,p_i)\}_{i\in[2..n]}$
5. Otherwise $c_2\gets G[2]$.
6. Output $\max(c_1+p_1, c_2+p_2)$

### Runtime

The important observation—and benefit of using dynamic programming—is that each subproblem is only going to be solved once. For each problem, we just need to find $j(i)$, which takes $O(\log n)$, resulting in total $O(n\log n)$ time. 

If instead we stipulated that the inputs were not sorted, we could also sort them in the same amount of asymptotic time. 
---
tags:
  - dynamic-programming
---
>[!problem]
>**Input:** 
>1. $t_1, \dots, t_n \in \mathbb R$
>2. $k \in [1..n]$
>
>**Output:** Find $k$ centers $s_1, \dots, s_k \in \mathbb R$ such that the distance between the furthest point and its closest center is minimized.

**Solution Space:** $(s_1, \dots, s_k)\in \mathbb R^k$

**Objective Function:** $$f(s_1,\dots,s_k)=\max_{i\in[1..n]}\min_{j\in[1..k]}|t_i-s_j|$$
**Subproblem:** Where do we place the first station?
- Phrased another way: which towns does the first station serve?

If $i$ is the last station that the first station serves, then we should have
$$s_i=\frac{t_1+t_i}{2}$$
That is, it should be at the midpoint between the two endpoints of the interval it serves.

$$\begin{align}G(1..n,k)&=
\text{min $f$-value for serving towns $t_1,\dots,t_n$ using $k$-centers} \\
&=\min_{i\in[1..n]}
\max\left\{\frac{|t_1-t_i|}{2},G(i+1..n, k-1)\right\}
\end{align}$$
Then to generalize,
$$\begin{align}
G(i,j)&=\text{min $f$-value of placing $j$ stations to serve towns $t_i,\dots,t_n$} \\
&=\min_{l\in[i..n]}
\max\left\{\frac{|t_i-t_l|}{2},G(l+1, j-1)\right\}
\end{align}$$
with base cases
$$\begin{align}
G(n+1,j)&=0 \\
G(i,0)&=\infty
\end{align}$$
## Analysis

There are $nk$ subproblems of the form $G(i,j)$. 

The time to solve each such problem, assuming that all smaller subproblems have been solved, is $O(n)$ (to iterate through the minimums).

Thus, the overall runtime is $O(n^2k)$.
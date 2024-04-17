---
tags:
  - graph-algorithms
  - dynamic-programming
---
## Problem

>[!problem]
>**Input:** Directed graph $G=(V,E)$ with weight function $w:E\to\mathbb R$. Assume that there are no negative-weight cycles.
>
>**Output:** $D(u,v)=\text{length of shortest path }u\to v$.

This is a generalization of the single-source shortest-path problem that we've studied at different levels: [BFS](Graphs%20Review.md#Single-Source%20Shortest%20Path%20Problem) in the unweighted case, [Dijkstra's algorithm](Dijkstra's%20Algorithm.md) in the non-negative weighted case, and [Bellman-Ford algorithm](Bellman-Ford%20Algorithm.md) in the general weighted case.

As a baseline, we can consider $n$ runs of Bellman-Ford—one for each vertex. Since Bellman-Ford runs in $O(nm)$ time, this corresponds to $O(n^2m)=O(n^4)$ time.

The Floyd-Warshall algorithm, which we present below, solves the problem in $O(n^3)$ time.

## Naive Algorithm

The key idea behind Bellman-Ford's algorithm is using [dynamic programming](Dynamic%20Programming.md). Specifically, let's define the following $G$ function:

$$\begin{align}
G(u,v,k)&=\text{shortest path $u\to v$ using $\le k$ edges} \\
G(u,v,0)&=\begin{cases}0 & \text{ if }u=v \\ \infty & \text{o.w.}\end{cases}
\end{align}$$
To solve our subproblem, we note that the subpath of a shortest path is a shortest path itself. Thus, we can find $G(u,v,k+1)$ by looking through all shortest paths of length $k$, then looking at the edge between that path and $v$. That is,
$$G(u,v,k+1)=\min_{(z,v)\in E}G(u,z,k)+w(z,v)$$
### Analysis

With dynamic programming, we analyze the runtime by looking at the number of subproblems and the time it takes to solve each of them.

There are $O(n^3)$ subproblems (we have $n$ vertices possible each for $u$ and $v$, then $k\in[0..n-1]$ edges in a simple path). Then, each subproblem takes $n$ time to execute (because we look through at most $n$ edges of the form $(z,v)\in E$). This gives total $O(n^4)$ runtime, which doesn't beat our baseline.

## Efficient Algorithm

Instead, we can decompose our problem in a different, clever manner to achieve a faster runtime. What if instead of restricting the length of the path, we restrict the vertices that can be used in the path?

Specifically, we number the vertices $[1..n]$, then define $G$ as:
$$G(u,v,k)=\text{length of shortest path $u\to v$ that only uses internal vertices in $[1..k]$}$$
Note that $u,v$ aren't necessarily in $[1..k]$ for these subproblems. We then have the base case
$$G(u,v,0)=\begin{cases}
0 & u=v\\
w(u,v)& (u,v)\in E \\
\infty & \text{o.w.}
\end{cases}$$

To solve $G(u,v,k+1)$, we observe that the only paths we haven't considered in $G(u,v,k)$ are those that stop at $k+1$ at some point between $u$ and $v$. Noting that this path consists of two shortest paths using vertices in $[1..k]$ respectively from $u\to k+1$ and $k+1\to v$. Then, we can say
$$G(u,v,k+1)=\min\{G(u,v,k),G(u,k+1,k)+G(k+1,v,k)\}$$
### Analysis

We still have the same number of subproblems $O(n^3)$, but we can now solve each subproblem in constant time, so our overall runtime is $O(n^3)$. 
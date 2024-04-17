---
tags:
  - graph-algorithms
  - greedy-algorithms
---
>[!note]
>See [CIS 1210](Shortest%20Path.md#Dijkstra's%20Algorithm) notes on the same topic.

## Problem

>[!problem]
>**Input:** 
>- Directed graph $G=(V, E)$
>- Weight function $w:E\to\mathbb R_{\ge0}$
>- A source vertex $s\in V$
>
>**Output:** All shortest paths from $s$ to $u\in V$. We denote the length of the shortest path $s\rightsquigarrow u$ as $\delta(s,u)$.

First, a note on the problem specification. There are three related problems in the shortest path family:
- Single source to single target
- **Single source to all targets**
- All pairs shortest paths

As it turns out, there's no computational benefit for choosing the first over the second, so Dijkstra's algorithm is essentially the solution to both. The third is solved by a more general solution than Dijkstra's.

## Motivation

>[!lemma]
>Consider $G, w$. $\forall s, u\in V$, the shortest path from $s$ to $u$ in $G$ is a simple path.

**Proof.** Assume for contradiction that there exists some cycle along the shortest path from $s$ to $u$. Let $c_1, c_2, \dots, c_1$ be the vertices along that cycle. Then, the path $s\rightsquigarrow c_1\rightsquigarrow u$ (that is, bypassing all the vertices along the cycle) still gets us from $s$ to $u$ and is at most the same length as the original path.

>[!lemma]
>Consider $G,w$. If $p$ is the shortest path from $s$ to $u$ and $p_{s\rightsquigarrow v}$ is the subpath of $p$ from $s$ to $v$, then $p_{s\rightsquigarrow v}$ is itself a shortest path.

**Proof.** Assume again for contradiction that $p_{s\rightsquigarrow v}$ is not a shortest path. Let $p'_{s\rightsquigarrow v}$ be the true shortest path from $s$ to $v$. Then, the path $p'_{s\rightsquigarrow v}+p_{v\rightsquigarrow u}$ is a strictly shorter path from $s$ to $u$. That is, replacing $p_{s\rightsquigarrow v}$ with $p'_{s\rightsquigarrow v}$ in the path from $s$ to $u$ will yield a necessarily shorter path.

## Algorithm

>[!algorithm]
>1. Initialize $D: V\to\mathbb R_{\geq0}\cup\{\infty\}$:
>	1. $D(s)=0, D(u)=\infty$
>	2. We will maintain that $D(u)\geq\delta(s,u)$
>2. Keep set $S=\{s\}$
>3. Keep a heap of vertices holding $V\setminus S$ with keys $D(v)$
>4. Repeat:
>	1. Extract-min on the heap. Keep $D(v)$ fixed.
>	2. $\forall z$ such that $(v,z)\in E, D(z)=\min\{D(z), D(v)+w(v,z)\}$

### Correctness

>[!lemma]
>Let $D(u)\geq \delta(s,u)$ and consider $S\subseteq V$ such that $\forall u\in S, D(u)=\delta(s, u)$. Now suppose $\forall v\in V\setminus S$,  $\forall u\in S, D(v)\leq D(u)+w(u,v)$ and $v$ is the smallest among these.
>
>Then, $D(v)=\delta(s,v)$. 

**Proof.** Suppose $p$ is the true shortest path $s\rightsquigarrow v$. 

*Case 1:* $p:s\rightsquigarrow u\rightsquigarrow v$, where $u\in S$
$$\begin{align}
D(v)&\le D(u)+w(u,v)\\
&=\delta(s,u)+w(u,v)\\
&=\text{length of }p=\delta(s,v)
\end{align}$$
*Case 2:* $p:s\rightsquigarrow u\rightsquigarrow v$, where $u\in V\setminus S$

Assume for contradiction that $D(v)>\delta(s,v)$. 
$$\begin{align}
D(v)&>\delta(s,v) \\
&=\delta(s,z)+\delta(z,v)\\
&=D(z)+\delta(z,v) \\
&\geq D(z)
\end{align}$$
### Runtime

We do $n$ extract-min operations, each of which requires $O(\log n)$. Further, we do $m$ decrease key operations, which also take $O(\log n)$ time.

Using a Fibonacci heap, the decrease key operations can be sped up to $O(1)$ amortized time.



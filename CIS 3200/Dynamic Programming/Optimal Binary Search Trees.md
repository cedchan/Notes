---
tags:
  - dynamic-programming
---
## Problem Description

>[!definition]
>A **binary search tree (BST)** stores values in sorted order in a tree structure.
>
>The depth of an element corresponds to the time it takes to access that element. An optimal BST will have $O(\log n)$ search time.

>[!problem]
>**Input:** Indices $1,\dots,n$, and $p_1, \cdot, p_n$ such that $p_i$ is the measure of how often index $i$ appears.
>
>**Output:** BST $T$ containing elements $1,\dots,n$ such that we have $$\min\sum_{i=1}^np_i\cdot{\rm depth}(i,T)$$

Another way of phrasing it is that we're trying to minimize the expected time it takes to access elements in the tree. That is, we minimize
$$\underset{i\sim p}{\mathbb E}[{\rm depth}(i,T)]$$

## Algorithm

**Solution Space:** All possible BSTs $1,\dots,n$.

**Objective Function:** $p_1,\dots,p_n\in\mathbb R$
$$f(T)=\sum_{i=1}^np_i\cdot{\rm depth}(i, T)$$

**Top-Level Question:** What should we place at the root?

For each $i$ we try as the root, we can decompose the rest of the tree into the optimal tree for inputs $1,\dots, i-1$ and $i+1,\dots,  n$.

Let
$$G(i,j)=\text{min $f$-value of BST storing $i,\dots,j$ w.r.t. $p_i, \dots, p_j$}
$$
where $i\in[1..n]$ is the "start" index and $j\in[1..n], j\geq i$ is the "end".
$$\begin{align}G(i,j)&=\min_{k\in[i,j]}\left\{\overbrace{p_k}^\text{root cost}+\underbrace{G(i,k-1)+\sum_{\ell=i}^{k-1}p_\ell}_\text{left tree cost, shifted down}+\underbrace{G(k+1,j)+\sum_{\ell=k+1}^jp_\ell}_\text{right tree cost, shifted down}\right\} \\
&=\min_{k\in[i,j]}\left\{G(i,k-1)+G(k+1,j)+\sum_{\ell\in[i,j]}p_\ell\right\}
\end{align}$$
The $\sum p_\ell$ terms come because we have to shift the right and left subtrees down by 1 (since we're attaching them below the root). That is, for a tree from $i$ to $j$, if we shift everything down by one, we get weighted depth
$$\begin{align}
\sum_{\ell=i}^jp_\ell\cdot(1+{\rm depth}(\ell, T))&=\sum_{\ell=i}^jp_\ell\cdot{\rm depth}(\ell, T)+\sum_{\ell=i}^jp_\ell \\
&=G(i,j)+\sum_{\ell=i}^jp_\ell
\end{align}$$
Then we can set our base cases. $G(i, i)=p_i$. 

## Analysis

There are $O(n^2)$ subproblems, which each take $O(n)$ time to compute. This results in $O(n^3)$ runtime. Note that the $\sum_{\ell\in[i,j]}p_\ell$ problem can be computed on its own for all combinations, adding $O(n^2)$ time. 


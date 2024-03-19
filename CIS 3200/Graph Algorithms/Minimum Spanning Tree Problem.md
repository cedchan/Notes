---
tags:
  - graph-algorithms
  - greedy-algorithms
---
>[!note]
>See CIS 1210 [notes](Minimum%20Spanning%20Trees%20(MSTs).md) on the same subject.

## Problem Setup

>[!problem]
>**Input:** A weighted, connected graph $G=(V,E)$ with weight function $w:E\to\mathbb R_{\geq0}$.
>
>**Output:** Minimum spanning tree $T=(V,E'), E'\subseteq E$ that minimizes that sum of the sum of the weights of edges in the subgraph.

Some applications:
- Minimizing the cost of building a road network/broadcast network
- Single-linkage clustering—modeling evolutionary trees
- As a subroutine in other algorithms

## Cut Property

>[!lemma]
>
>Let $G=(V,E)$ be any connected graph, and let $(S,V\setminus S)$ be any non-empty cut. Then, 
>1. $\exists (u,v)\in E$ such that $u\in S, v\in V\setminus S$.
>2. $\exists$ a minimum-weight edge $e$ crossing the cut in some $\rm O\small PT$.

**Proof.** The first observation follows from the fact that $G$ is connected.

The second observation can be shown using an exchange argument. Suppose that we have some optimal MST such that the minimum-cost edge $e$ crossing the cut is not in the tree. Instead, some edge $e'$ connects the two sides of the cut. We replace $e'$ with $e$. We maintain optimality because the weight of the subgraph of the tree with vertices in $S$ and $V\setminus S$ remain the same, but connecting them now requires less. 

## Prim's Algorithm

>[!algorithm]
>1. Initialize $S=\{v\}, T=\emptyset$
>2. Find minimum weight edge $e=(v,u)$ such that it crosses $(S,V\setminus S)$
>3. Update $S\gets S\cup\{u\}$ and include $e$ in $T$.
>4. Repeat until $S=V$

These steps provide a good outline of the outer-loop execution, but there are a couple of implementation details that remain to be hammered out for each iteration
1. We must maintain a set $S\subset V$
2. We must at all times be able to find the minimum weight edge crossing the cut
3. We must add a vertex to $S$

We can achieve this by using a [min-heap](Heaps.md) that stores edges $(v, u)$ with key $w(v, u)$. For each step, we remove other edges incident on $u$ that go to $S$, and add all other edges incident on $u$. 

**Runtime:** We run the outer loop $n$ times—once for each vertex. Then, within each vertex, each heap operation takes $O(\log n)$ time. We require one operation for extracting the minimum weight edge, and ${\rm deg}(u)$ operations to modify the heap based on the edges incident on $u$. Thus, we have total
$$\begin{align}
n\cdot O(\log n)+\sum_{u\in V}{\rm deg}(u)\cdot O(\log n)=O(n\log n)+O(m\log n)=O((m+n)\log n)
\end{align}$$

A more efficient algorithm can achieve $O(m+n\log n)$.
## Kruskal's Algorithm

>[!algorithm]
>1. Initialize $T=\emptyset$ and maintain the connected components of $T$.
>2. Sort the edges according to the weight.
>3. Process edges in order. For each edge $(u, v)$, if $u$ and $v$ are already connected, throw out the edge. Otherwise, include $(u,v)$ in $T$.

We can also apply the cut property here to show correctness. If for each iteration, we let $S$ be the connected component that $u$ is in, then, by the cut property $(u,v)$ must be in the optimal.

The data structure problem we face with Kruskal's is different, though:
1. Maintain sets of connected components
2. Check if two elements belong to the same set (to show if $u,v$ are in the same CC)
3. Merge two sets

This is solved by the [union find](Union%20Find.md) data structure.

The key idea is that each set has a representative. These sets can be represented as up-trees, where the root of the tree is the representative of the set. Checking if two elements belong to the same takes time proportional to the height of the tree: we check if the two elements share the same representative.

Finding the union of two sets takes constant time—we can just make one root the parent of the other—but the risk is that we add at most 1 to the height of the new tree. By doing union by rank—making the representative of the taller tree the representative of the union—we can ensure that the height of the tree is bounded by $\log n$. 

We can thus calculate runtime: It takes $m\log m=m\log n$ time to sort the edges. Then, we run the outer loop $m$ times and for each iteration we take $O(\log n)$ time to calculate membership and $O(1)$ time to merge sets. Thus we have total time $O(m\log n)$.

We can speed things up even more by using path compression. The idea is that we can do union and find in the same way: while you're finding the representative of a node, set the parent of that node to be the representative. This also affects every element along the path to the root, flattening the path to all have height 1. 

This yields $O(\alpha m)\leq 4$. So if we have the edges pre-sorted, we can achieve nearly linear-time MST.





## Problem

Consider a graph whose vertices are partitioned into a set of students and a set of residency slots. An edge connects a student $u$ to a residency slot $v$ iff $u$ is qualified for $v$.
![|100%x250](Drawing%202024-03-25%2016.26.03.excalidraw.md)
Recall the definition of a matching:

>[!definition]
>A **matching** of a graph is a collection of edges such that each vertex is incident on one edge in the collection.
>
>In a **perfect matching**, every vertex is matched to something else (i.e., it's a bijection).

We have 3 questions we want to answer:

>[!problem]
>
>Given $(A,B,E)$, where $A$ is the first set, $B$ is the second set, and $C$ is the set of edges between them,
>
>**Question 1:** Is there a perfect matching?
>
>**Question 2:** How fast can we find a perfect matching, if one exists?
>
>**Question 3:** If a perfect matching doesn't exist, how can we find a maximum-cardinality matching?

Let's consider a benchmark for these problems. The simplest is brute force: We can try every possible assignment. This is $O(n!)$.

## Hall's Theorem

>[!theorem]
>Consider any bipartite graph $(A, B, E)$. There exists a perfect matching<sup>1</sup> iff two conditions hold:
>1. $|A|=|B|$
>2. $\forall U\subseteq A, |N(U)|\ge |U|$
>
><small>[1]: Note that if we only want an $A$-saturating matching—that is, a matching that includes every vertex in $A$, but not necessarily $B$, then we only need the second condition.</small>

Note that $N(U)$ denotes the neighborhood of $U$. That is,
$$N(U)=\{v\mid \exists u\in U \text{ s.t. } (u,v)\in E\}$$
**Proof.**
($\impliedby$) That is,
$$\exists\text{ perfect matching}\implies|A|=|B|\land \forall U\subseteq A,|N(U)|\ge|U|$$

($\implies$) That is,
$$|A|=|B|\land \forall U\subseteq A,|N(U)|\ge|U|\implies\exists\text{ perfect matching}$$
*Case 1:* Consider all $U\subset A$ such that $|N(U)|>|U|$

Consider $(u,v)$ 

...

## Max Flow Bipartite Matching

Recall that the [max flow](Network%20Flows.md#Problem) problem allows us to solve bipartite matching by constructing the following graph (proof in linked notes):

![100%x300](Drawing%202024-03-27%2016.23.01.excalidraw.md)
### Running Time

In such a graph, the max flow is $O(mn)$, so with [Ford-Fulkerson](Network%20Flows.md#Ford-Fulkerson%20Algorithm) we get $O(mn)$ time. [Capacity scaling](Network%20Flows.md#Capacity%20Scaling) gives us $O(m^2)$ time. Finally, [Edmonds-Karp](Network%20Flows.md#Edmonds-Karp%20Algorithm) gives us the standard $O(m^2n)$ time.

## Hopcroft-Karp Algorithm

This is a modification of the general Edmonds-Karp algorithm, optimized for bipartite matching.

>[!algorithm]
>1. Maintain $f$ (i.e., current matching $M$)
>2. Find residual graph $G_f$
>	1. Compute $d(f)$
>	2. Find as many $(s,t)$ paths in $G_f$ of $d(f)$ hops

>[!idea]
>For each iteration, we use DFS to push as much flow on vertex-disjoint paths.

The claim is that this can be done in $O(m)$ time on the DFS tree (i.e., excluding back edges). Thus, in $O(m)$ time, we can increase $d(f)$ by one. This gives us $O(mn)$ running time. 

### Analysis

>[!claim] Claim 1
>Suppose $P_1, \dots, P_k$ form a maximal set of $d(f)$-length $(s,t)$ paths in $G_f$. Then, after pushing flow $d(f')\ge d(f)+1$. 

This shows that the number of iterations we need is at most $O(n)$. 

**Proof.** Suppose $\tilde P$ still has length $d(f)$ after pushing flow. Then, we can only use forward edges (if we used any back edges, we'd have to increase $d(f')$ in order to make up for the lost distance (in terms of hops)). But if we use only forward edges, then this path must've existed in some previous iteration, contradicting that $P_1, \dots, P_k$ is maximal.

>[!claim] Claim 2
>Suppose $\sc{OPT}-M=k$ (that is, we are $k$ away from the optimal solution). Then, there exist $k$ alternating paths in $G_f$. This implies that at least one of these paths must be length at most $\frac nk$. This means $d(f)\le\frac nk$.

The key observation made is at iteration $\sqrt n$. From the above claims, $\sqrt n\le d(f)\le\frac nk$. Rearranging the terms, we get that $k\le \sqrt n$.

>[!claim]
>In $O(m)$ time, we can find the maximal set of vertex-disjoint paths in $G_f$ of length $d(f)$.

**Algorithm:**
1. Compute $d(f)$ using BFS
2. Greedily start DFS from unmatched $u\in L_1$. 
	1. DFS reaches $t$ in $d(f)$ steps. Remove vertices on path $P_1$.
	2. If DFS backtracks on an edge, remove it.







---
tags:
  - graph-algorithms
---
>[!note]
>See [CIS 1210](Graph%20Traversals.md) notes on the same topic.

## Properties

A undirected, unweighted graph $G$ can be represented as the tuple $(V, E)$, where $V$ is the set of vertices and $E\subset V\times V$ is the set of edges $(u, v)$.

There are particular ways of actually representing graphs in programming languages, such as adjacency lists or matrices. For the purposes of algorithmic analysis, however—and considering that the different representations are provably equivalent and can be converted using efficient algorithms—we consider only abstract properties of graphs here. Namely,
- We can inspect nodes and their neighbors
- We can check connectivity between nodes

### Distance

An important, and well-studied, notion in graph theory is the "distance" between two nodes $v_1, v_2\in V$. Formally, a distance function is defined as $d:V\times V\to \mathbb R_{\geq0}$. 

In mathematics, there are several axioms that distance functions must follow. Some important ones are shown below:
1. $d(x, x)=0$
2. $d(x, y)=d(y,x)$
3. $d(x,y)\leq d(x,z)+d(z,y)$

Based on these axioms, we can define a distance function $d_G$ for graphs.

>[!definition]
   $$d_G(u,v)=\text{length of the shortest path from $u$ to $v$ in $G$}$$

## Single-Source Shortest Path Problem

>[!problem]
>**Input:** Graph $G=(V,E)$, and source vertex $s\in V$.
>
>**Output:** A list $d_G(s,v),\forall v\in V$
>

This is the classic problem solved by the **breadth-first search (BFS)** algorithm.

### Algorithm

We maintain several pieces of data that will make analysis easier:
- Each vertex keeps a **color** in $\{\text{``white", ``gray", ``black"}\}$, where $\rm white$ vertices are unexplored, $\rm gray$ vertices are in the process of being explored, and $\rm black$ vertices are done being explored. $s$ is initialized to $\rm gray$ while all other vertices are initialized to $\rm white$. 
- Each vertex has a **level** $\ell$ that is initialized to $\infty$ for all nodes except $s$, which has level $0$.
- Each vertex has a **parent** $\pi$ that "discovers" it. It follows that we can represent the entire search as a tree rooted at $s$, which encodes paths from $s$ to every reachable node in $G$.

>[!algorithm]
>1. Maintain a queue $q$, initially set to $\{s\}$
>2. While $q$ is non-empty, do the following:
>	1. Dequeue $v$ and set its color to $\rm black$
>	2. For neighbors $u$ of $v$ such that their color is $\rm white$, set their color to gray and add them to $q$. Set $\pi(u)=v$, and $\ell(u)=\ell(v)+1$.

## Analysis

**Runtime:** $O(n+m)$. Each edge is "touched" once when we check the neighbors of $u$, and each node is touched once when it is dequeued. Because we are checking the colors of the nodes, we ensure that these operations happen at most once.

>[!lemma]
>Let $V_d=\{v\mid d_G(s,v)=d\}$. By definition, $V_0=\{s\}$. 
>
>If $u\in V_d$ and $v\in V_{d+1}$, then $u$ enters the queue before $v$.

**Proof.** We prove this by induction.

*Induction Hypothesis:* Assume for induction that $u\in V_d, v\in V_{d+1}\implies u$ enters the queue before $v$.

*Base Case:* $u\in V_0$, $v\in V_1$. Since only $s$ is in $V_0$, and it is added as the first step of the algorithm, this is trivially true.

*Induction Step:* WTS $u\in V_{d+1},v\in V_{d+2}\implies u$ enters the queue before $v$. Assume for contradiction that $v$ enters the queue before $u$. We know from the IH that all nodes in $V_{d+1}$ are added to the queue before nodes in $V_d$. Then, if $v\in V_{d+2}$ is added to the queue before $u$, it must have some parent in $V_d$. This contradicts that $v\in V_{d+2}$, since $d_G(s,v)=d_G(s,\pi(v))+1=d+1\neq d+2$.


>[!lemma]
>$$u\in V_d\implies \ell(u)=d$$
>after the execution.

**Proof.** Again, we induct on $d$. If $u\in V_{d+1}$, it enters enter the queue after $V_d$ by our previous lemma. Further, we know $u$ has a parent in $V_{d+1}$ (by definition of $V_d$). Then, when this parent is explored, $u$ will get set to $\ell(u)=\ell(v)+1=d+1$. 

## Depth-First Search (DFS)

DFS works on directed graphs in ways that BFS sometimes cannot. For DFS, we maintain the same colors for each node as in BFS.

$\text{DFS-Visit}(v)$:
1. Color $v$ gray
2. Iterate through all white neighbors $u$ of $v$:
	1. Set $u$ to gray
	2. $\pi(u)\gets v$
	3. Call $\text{DFS-Visit}(u)$
	4. Set $u$ to black

### Analysis

**Runtime:** $O(n+m)$. Similarly, we go through each node and edge exactly once.

### Topological Sorting of Directed Acyclic Graphs (DAGs)

>[!note]
>See CIS 1210 notes on [DAGs](Directed%20Acyclic%20Graphs%20(DAGs).md).


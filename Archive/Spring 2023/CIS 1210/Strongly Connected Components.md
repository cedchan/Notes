## Definitions

>[!definition]
>A **strongly connected component (SCC)** of a [directed graph](Graph%20Traversals.md) $G=(V, E)$ is a maximal set of vertices $C\subset V$ such that for every pair of vertices $u, v\in C$, we have both $u\rightsquigarrow v$ and $v\rightsquigarrow u$. That is, vertices $u$ and $v$ are reachable from each other.

>[!hint]
>Connected components are defined for [undirected graphs](Graph%20Traversals.md), and strongly connected components are defined for directed graphs.

Finding connected components in an undirected graph is easy: We run a [DFS](Graph%20Traversals.md#Depth-First%20Search%20(DFS)). Each tree in the resulting DFS forest is a connected component.

>[!definition]
>Suppose we combine each strongly connected component of $G$ into a "giant vertex." Let us define $G^{SCC}=(V^{SCC},E^{SCC})$ as follows:
>- $V^{SCC}$: Contains a vertex $v_i$ for each SCC $C_i$ in $G$
>- $E^{SCC}$: Contains edge $(v_i, v_j)$ if $G$ contains a directed edge $(x, y)$ such that $x\in C_i$ and $y\in C_j$

## Kosaraju's Algorithm

>[!lemma]
>$G$ and $G^T$ (the [transpose](Computer%20Science.md#Graph%20Theory#Graph%20Transpose) of $G$) have the same strongly connected components.

*Proof:* If there is a path from $u\rightsquigarrow v$ in $G$, there must be a $v \rightsquigarrow u$ in $G^T$, because each edge along that path is flipped. Thus, for every pair $u, v\in G$ that are reachable by each other, the same is true in $G^T$. 

```
Kosaraju(G):
	Call DFS(G) to compute finishing times u.f
	Compute G.T
	Call DFS(G.T) but consider vertices in order of decreasing u.f
	return the vertices of each DFS tree as separate SCCs
```

### Proof of Correctness

>[!lemma]
>Let $C$ and $C'$ be distinct strongly connected componets in directed graph $G=(V, E)$, let $u, v\in C$ and $u', v' \in C'$, and suppose that $G$ contains a path $u \rightsquigarrow u'$. Then $G$ cannot also contain a path $v' \rightsquigarrow v$. 
>
>Thus, $G^{SCC}$ is a [DAG](Directed%20Acyclic%20Graphs%20(DAGs).md).

*Proof:* If both such paths exist, then all vertices in both $C$ and $C'$ can reach each other via those four vertices. Thus, $C, C'$ aren't maximal and combined into a larger SCC.

#### The Intuition

Now that we've established that $G^{SCC}$ is a DAG, the intuition is simple. Consider a [sink vertex](Computer%20Science.md#Graph%20Theory#Sink%20Vertex) in $G^{SCC}$. For example, the last vertex $v_n$ in the [topological ordering](Directed%20Acyclic%20Graphs%20(DAGs).md#Topological%20Ordering) of $G^{SCC}$ is a sink (clearly, if it had out edges, then it wouldn't be the last in the sorting, and there are no "back" edges). Then, if we do a DFS from some vertex $u$ in $v_n$, the DFS tree with $u$ will be a strongly connected component. This is because $u$ can obviously reach all other vertices in $v_n$, but it further can't reach any other vertices outside $v_n$ because $v_n$ is a sink. When the DFS continues, then, it must start a new tree. Again, we choose our new sink (since we remove the vertices of $v_n$, we still have a DAG and we can find a new sink), again producing the same result until we have constructed our full forest. 

#### Proof

We prove that Kosaraju's works (each DFS tree of $G^T$ is an SCC) by induction on the number of DFS trees.

**Induction Hypothesis:** The first $k$ trees produced are SCCs.

**Base Case:** $k=0$ is trivially true

**Inductive Step:** By IH, the first $k$ trees are SCCs. Now we look at the $k$-th tree, whose root is $v$ in SCC $C$. Since we construct trees in decreasing finish time order, $u.f=C.f > C'.f$ for any SCC $C'$ that has yet to be visited. 

By IH, all other vertices of $C$ are white when $u$ is visited (since it's the root). Thus, by the [white path theorem](Graph%20Traversals.md#Depth-First%20Search%20(DFS)#White%20Path%20Theorem%20(WPT)), all these vertices are descendants of $u$. Further, $u$ has no other descendants because $C$ is a sink. Thus, the vertices of the DFS tree rooted at $u$ are exactly one SCC.
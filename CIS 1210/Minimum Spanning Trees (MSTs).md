
## Background

>[!definition]
>A **spanning subgraph** of $G$ is a subgraph of $G$ that contains all the vertices in $G$.
>
>A **minimum weight spanning subgraph** (minimum spanning subgraph) is a spanning subgraph whose total cost is the minimum over all other spanning subgraphs.

Our goal is to find a minimum spanning subgraph $T$.

>[!theorem]
>A minimum spanning subgraph that is connected (i.e., $T$ as described above) is a tree. This is called a **minimum spanning tree (MST)**.

*Proof:* We know $T$ is connected by construction. Then assume for contradiction there exists a cycle in it. We can remove any edge in the cycle and it will still be connected, but the sum of edge weights would've decreased, assuming each weight is positive. This contradicts that $T$ is a minimum spanning subgraph.

### The Cut Property

>[!theorem]
>For a connected, undirected graph $G=(V, E)$, consider any nonempty $S\subset V$. Let $e$ be the minimum cost edge with on end in $S$ and the other in $V\setminus S$. Every MST must contain $e$. 

*Proof:* Assume for contradiction that a minimum spanning tree $T$ doesn't contain $e$. There must exist some other edge $e'$ in $T$, then, with one edge in $S$ and the other in $V \setminus S$, since $T$ is connected. We can replace $e'$ with $e$ in $T$ because it will still be connected, and since $w(e)<w(e')$, we produce a spanning tree with a smaller overall weight. This contradicts that $T$ is an MST.

### The Cycle Property

>[!theorem]
>Let $G=(V, E)$ be a connected, undirected graph. Let $C$ be any cycle in $G$ and let $e=(u, v)$ be the heaviest edge in $C$. Then $e$ doesn't belong in any MST of $G$.

*Proof:* Assume for contradiction that some MST $T$ of $G$ contains $e$. We can replace $e$ with any other edge in $C$ to maintain connectedness while decreasing the overal weight, contradicting that $T$ is an MST.

## Prim's Algorithm

Prim's algorithm is very similar to [Dijkstra's algorithm](Shortest%20Path.md#Dijkstra's%20Algorithm). We start at some vertex $s$, then add each cheapest vertex while doing edge relaxation. The difference is that we only care about the minimum cost to connect to each vertex to our tree $T$, not find a path from $s$ to each vertex. Thus, we change $\text{dist}$ from Dijkstra to simply the minimum weight from a vertex $v$ to some other vertex $u\in T$. 

Alternatively, we can say that we start with $T=\{s\}$, and each iteration, we add the vertex for which "crossing the cut" from $T$ to the other edges requires the smallest weight.

```
Input: A connected graph G = (V, E) as an adjacency list, a weight funtion w: E -> R, and a starting node s
Outpur: An MST of G

Prim(G, s):
	Let PQ be a priority queue containing every vertex in G
	for each v in V do
		v.key = INFINITY
		parent[v] = NIL
		
	s.key = 0
	
	while PQ is not empty do
		v = PQ.ExtractMin()
		for each u in Adj[v] do
			if u in PQ and w(u, v) < u.key then
				u.key = w(u, v)
				parent[u] = v
				
	return parent
```

### Runtime

This requires $O(m\lg n)$ time, from Dijkstra's [runtime](Shortest%20Path.md#Dijkstra's%20Algorithm#Runtime).

### Correctness

In each iteration we maintain a set $S\subseteq V$, then add the minimum-weight edge $e$ to cross the cut into $V\setminus S$. By the [cut property](Minimum%20Spanning%20Trees%20(MSTs).md#Background#The%20Cut%20Property), $e$ must be in $T$. Since we output a spanning tree, we have an MST.

## Kruskal's Algorithm

Kruskal's algorithm begins with a graph without edges $T$. Then it iterates through the edges in increasing weight order, and adds each edge to $T$ if adding that edge won't create a cycle.

[TK links]

To check if adding an edge $(u, v)$ creates a cycle, we use the Union Find (UF) data structure, which has the following methods:
- `MakeSet(x)`: Creates a set with just the element $x$
- `Find(x)`: Returns the ID of the set that contains $x$
- `Union(x, y)`: Combines the sets containing $x$ and $y$

```
Input: A connected graph G = (V, E) as an adjacency list, and a weight function w: E -> R
Output: An MST of G

Kruskal(G):
	T = {}
	Sort the edges in E in increasing order of weight
	for each v in V do
		MakeSet(v)

	for each e = (u, v) in E do
		if Find(u) != Find(v)
			T = T + {e}
			Union(u, v)
	
	return T
```

### Runtime

Kruskal's algorithm runs in $O(m\lg n)$ time, just like Prim's and Dijkstra's.

Sorting the edges takes $O(m\lg m)=O(m\lg n)$ time, which dominates the other operations. (See UF notes for details.) 

[Link TK]

### Correctness

Consider an edge $e=(u, v)$ added by Kruskal's. Clearly, $u\in S$ but $v\notin S$ (otherwise it would form a cycle). Further, since we iterate in increasing order of weight, $e$ is the lightest crossing from $S$ to $V\setminus S$ because no other edges in $V\setminus S$ have yet been encountered. Then, by the [cut property](Minimum%20Spanning%20Trees%20(MSTs).md#Background#The%20Cut%20Property), we have an MST.

## Reverse Delete

Reverse delete is like the opposite of Kruskal's. It starts with $G$, then iterates through edges in decreasing order of weight and deletes edges so long as the graph remains connected.

```
Input: A connected graph G = (V, E) as an adjacency list, and a weight function w: E -> R
Output: An MST of G

ReverseDelete(G):
	T = E
	Sort the edges in E in decreasing order of weight
	
	for each e (u, v) in E do
		if T - {e} is connected
			T = T - {e}
	
	return T
```

### Runtime

Reverse delete uses $O(m^2)$ time.

Sorting requires $O(m\lg n)$ time. Then, checking if $T-\{e\}$ is connected can be done using [BFS](Graph%20Traversals.md#Breadth-First%20Search%20(BFS)) in $O(n+m)$ time. We do this for each edge $m$, requiring $O(m(n+m)$ for this step. This gives in total $O(m\lg n + m(n + m))=O(m^2)$. 

### Correctness

This follows directly from the [cycle property](Minimum%20Spanning%20Trees%20(MSTs).md#Background#The%20Cycle%20Property). We iterate in decreasing order of weight, removing edges so long as the graph doesn't become disconnected. If removing such an edge doesn't disconnect a graph, it must not be part of a minimally connected component—i.e., it's part of a cycle. Thus, we have an MST.

## MSTs with Equal Edge Weights


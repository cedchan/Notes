>[!definition]
>A **graph** is a set of **vertices** and **edges**. Formally, we have a graph $G=(V, E)$, where $E\subset V \times V$. Typically, we denote $n=|V|, m=|E|$.
>
>A graph is **undirected** iff $\forall (i, j) \in E, (j, i) \in E$ (edges are bidirectional). It is **directed** otherwise.

In undirected graphs, $m\leq\binom{n}{2}=\frac{n(n-1)}{2}$. In directed graphs, $m\leq 2\binom{n}{2}=(n-1)$. 

>[!equation]
>Thus, $$m=O(n^2), \log m = O(\log n)$$

>[!definition]
>A graph is **connected** if $\forall u, v\in V, \exists \text{ a path } u\rightsquigarrow v$. For an undirected connected graph, $m\geq n-1$. 
>
>A graph is **sparse** if it has few edges, and **dense** if it has many.

## Graph Representations

There are two standard methods of representing graphs in memory: adjacency matrices and adjacency lists.

### Adjacency Matrix

An adjacency matrix $A$ is an $n \times n$ matrix, where each row and column corresponds to a vertex. The $A[i][j]=1$ if $(i, j) \in E$ and $0$ otherwise. 

Checking if an edge exists or adding an edge takes $O(1)$ time, but for a large number of edges, this can be space-intensive ($\Theta(n^2)$), especially for a sparse graph, where most of the matrix will be 0.

### Adjacency List

An adjacency list $A$ is an array of $n$ elements, where each element is a linked list of vertices. If $A[i]$ contains $j$, then $(i, j) \in E$. 

Searching for an edge can take at most $\text{deg}(i)$ time, but it requires much less space ($\Theta(m+n)$) than an adjacency matrix, for sparse graphs. 

## Breadth-First Search (BFS)

The idea of a BFS is that from a source $s$, we travel through each "layer" of the graph. A "layer" $i$ consists of all nodes that are of distance $i$ to $s$. 

>[!definition]
>Consider $V_k=\bigcup\limits_{i=0}^{k-1}L_i$. A layer $L_k$ is formally:
>$$L_k=
\begin{cases}
\{s\} & \text{if } k = 0 \\
\{v\notin V_k \mid \exists u \in V_k \text{ s.t. } (u, v) \in E\} & \text{otherwise}
\end{cases}$$

We can also represent the BFS search as a tree, where $s$ is the root and each level represents vertices at a certain depth in the tree. 

During the search, we keep track of whether each node is discovered in the array `discovered`, and from which node a node is discovered in `parent`.

```
BFS(G, s):
	for each v in V do
		discovered[v] = FALSE
		parent[v] = NIL

	Let Q be an empty Queue
	Q.enqueue(s)
	discovered[s] = TRUE

	while Q is not empty do
		v = Q.dequeue()
		for each u in Adj[v] do
			if discovered[u] == FALSE then
				discovered[u] = TRUE
				Q.enqueue(u)
				parent[u] = v
```

Note that the order nodes of a certain level are visited in doesn't matter.

### Properties
1. For each $k\geq 1$, the layer $L_k$ consists of all nodes at distance exactly $k$ from $s$.
2. There is a path from $s$ to $t$ in $G$ iff $t$ appears in some layer (i.e., BFS finds it).
3. Consider $(x, y)\in E$. In the BFS tree $T$, $x\in L_i, y\in L_j$. Then $i, j$ differ by at most 1.

### Runtime

BFS runs in $O(m+n)$ time.

For each node, we examine its neighbors. So for each $v\in V$ we do $O(\text{deg}(v))$ work. By the handshake lemma, $\sum\limits_{v\in V}\text{deg}(v)=2m$. Thus, we have $O(n+2m)=O(n+m)$.

## Depth-First Search (DFS)

Unlike BFS, which goes layer by layer, DFS tries to get to the lowest layer reachable by following some path before going back to the siblings of the original vertex. It continues this process until all vertices have been discovered. DFS works for both directed and undirected graphs. 

>[!hint]
>This means that DFS produces a forest, whereas BFS only produces a tree.

DFS keeps track of several things in its search:
1. Vertices are of 3 colors: white (undiscovered), gray (discovered and examining), or black (finished).
2. Each vertex $v$ is timestamped with discovery time $v.d$ and finishing time $v.f$. 

	(In terms of color, $v.d$ is when the vertex first becomes gray, and $v.f$ is when it becomes black.)
3. After DFS completes, each edge will either be a **tree edge**, **back edge**, **forward edge**, or **cross edge**. (See [Classifying Edges](Graph%20Traversals.md#Depth-First%20Search%20(DFS)#Properties#Classifying%20Edges).)

```
DFS(G):
	for each v in V do
		color[v] = WHITE
	time = 0

	for each v in V do
		if color[v] = WHITE then
			DFS-VISIT(G, v)

DFS-VISIT(G, u):
	time = time + 1
	d[u] = time
	color[u] = GRAY
	for each v in Adj[u] do 
		if color[v] = WHITE then
			parent[v] = u
			DFS-VISIT(G, v)        // go deeper in the graph
	color[u] = BLACK               // all u's neighbors explored
	time = time + 1
	f[u] = time
```

An iterative approach can be written similar to [BFS](Graph%20Traversals.md#Breadth-First%20Search%20(BFS)). 

### Runtime

DFS runs in $O(n+m)$ time (just like BFS).

As written, `DFS-VISIT` is called on each vertex (recall that DFS searches *all* vertices). For each vertex, then, we iterate through each of its neighbors, requiring $\sum_{v\in V}\text{deg}(v)=O(m)$ time, not including the calls to `DFS-VISIT`. Thus in total we use $O(n+m)$ time.

### Properties

In a DFS forest, $v$ is a descendant of $u$ iff $v$ is discovered while $u$ is gray. 

#### Parenthesis Theorem

>[!theorem] 
>In a DFS graph, for any vertices $u, v$, exactly one of the following holds:
>1. The intervals $[u.d, u.f]$ and $[v.d, v.f]$ are entirely disjoint, and neither $u$ nor $v$ is a descendant of the other in the DFS forest.
>2. The interval $[u.d, u.f]$ is contained entirely within the interval $[v.d, v.f]$, and $u$ is a descedant of $v$ in a DFS tree.
>3. The interval $[v.d, v.f]$ is contained entirely within the interval $u.d, u.f]$, and $v$ is a descendant of $u$ in a DFS tree.

We can therefore say that $v$ is a proper descendant of $v$ in the DFS forest iff $u.d<v.d<v.f<u.f$. 

#### White Path Theorem (WPT)

>[!theorem]
>In a DFS forest, vertex $v$ is a descendant of $u$ iff at time $u.d$, there exists a path from $u$ to $v$ in $E$ consisting entirely of white vertices.

(Proof in lecture notes.)

#### Classifying Edges

>[!definition]
>Let $G_F$ be the DFS forest that results from calling DFS on $G$. The edge $e=(u, v)$ is a
>- **tree edge** if $e\in E(G_F)$. This happens when $v$ is discovered by exploring  $e$.
>- **back edge** if $u$ is a descendant of $v$ in $G_F$.
>- **forward edge** if $v$ is a descendant of $u$ in $G_F$, but $e\notin E(G_F)$.
>- **cross edge** otherwise (e.g., going between vertices in a DFS tree without ancestor/descendant relationships, or between DFS trees).

We classify $(u, v)$ based on the color of $v$ when the edge is first explored:
- If $v$ is white, $(u, v)$ is a tree edge
- If $v$ is gray, $(u, v)$ is a back edge
- If $v$ is black, $(u, v)$ is either a forward or a cross edge

>[!theorem]
>In a DFS of an undirected graph $G$, every edge is either a tree edge or a back edge.

## The Problem

The **shortest path** problem looks in a graph $G$ for a path $u \rightsquigarrow v$ such that the sum of the edge weights in the path is minimized. 

For notation, let $d(s, t)$ denote the shortest distance from $s$ to $t$. 

## Unweighted Graphs

The algorithm for unweighted graphs is easy: Just run [BFS](Graph%20Traversals.md#Breadth-First%20Search%20(BFS)) and return the path from $u$ to $v$ in the resulting tree, if it exists.

*Proof:* BFS searches each layer from $u$, meaning all nodes that are distance $i$ from $u$ in the $i$-th layer. Then, since there are no edge weights, the shortest distance is the shortest number of edges, which is what the path from $u$ to $v$ in the BFS tree is.

## Dijkstra's Algorithm

### The Intuition

Dijkstra's Algorithm is a [greedy algorithm](Computer%20Science.md#Algorithms#Greedy%20Algorithm) that solves the shortest path problem for graphs with *non-negative weights*. The algorithm maintains an array $\text{dist}$ that acts as an upper bound on the distances to each point, and chooses based on minimizing that distance.

More specifically, there are two key ideas behind the algorithm:
1. At any point in time, $\text{dist}[t]\geq d(s, t)$
2. When $t$ is finished, $\text{dist}[t]=d(s,t)$

Dijkstra maintains a set $S$ of vertices such that  each vertex $v\in S$ is "finished," as described above (i.e., its shortest path weight has been found). Then for all other vertices $u$, if $\text{dist}[u]>\text{dist}[v]+\text{weight(v, u)}$, it updates $\text{dist}[u]$ to that new lower bound. That is, it checks for all vertices outside of $S$ if a shorter distance can be calculated via some path $s\rightsquigarrow v\rightarrow u$, since we assume the distance found from $s$ to $v$ is minimized already. This updating is called **edge relaxation**.

### Algorithm

```
Input: Graph G = (V, E) as an adjacency list, source vertex s in V
Output: Arrays dist and parent, where for v in V, dist[v] is the shortest distance from s to v, and parent[v] is the previous vertex in the shortest path to v

Dijkstra(G, s):
	for each v in V do
		dist[v] = INFINITY
		parent[v] = NIL
	
	dist[s] = 0
	
	S = {}
	Q = min-priority queue on all vertices, with dist as keys
	
	while Q is not empty do
		u = ExtractMin(Q)
		S = S + {u}
		for each v in Adj[u] do
			if dist[v] > dist[u] + w(u, v) then
				dist[v] = dist[u] + w(u, v)
				parent[v] = u
	
	return dist		
```

### Correctness

>[!theorem]
>At any point during the execution of Dijkstra, for each $u\in S$, the path $P_u$ (i.e., the shortest path that Dijkstra has found to $u$) is a shortest $s\rightsquigarrow u$ path.

*Proof:* Induction on $|S|$. 

**Base Case:** $|S|=1$ trivially holds because if there is only one element, it must be $s$, and $\text{dist}[s]=0$. 

**Induction Hypothesis:** Assume the claim holds when $|S|=k$ for some $k\geq 1$.  

**Induction Step:** Consider $|S|=k+1$. Let $v$ be the last added vertex and $(u, v)$ be the final edge in our path $P_v$. By IH, $P_u$ is a shortest $s\rightsquigarrow u$ path. 

Let $P$ be a shortest path $s\rightsquigarrow v$ path. We want to show $P$ is at least as long as $P_v$. Let $y$ be the first node in $P$ that isn't in $S$. By definition, $P$ must be at least as long as $P_v$ because if it weren't, then Dijkstra would've chosen to add $y$ to $S$ instead of $v$. 

### Runtime

The runtime of Dijkstra depends on the [heap](Heaps.md) implementation. With our binary min heaps, the runtime is $O((V + E)\lg V)$, which is $O(E\lg V)$ if all vertices are reachable from the source. The fastest implementation uses Fibonacci heaps and is $O(V\lg V + E)$. 

For our implementation, we must [build](Heaps.md#Building%20a%20Heap) the heap in $O(n)$ time, then call [extract min](Heaps.md#Heap%20Extract%20Maximum) for each vertex. Our loop further checks each edge in the adjacency list once and thus calls [decrease key](Heaps.md#Heap%20Increase%20Key) at most once for each edge. Thus, our runtime is dominated by our extractions and key decreases, which require $O(\lg n)$ time for each vertex and edge, giving $O((V+E)\lg V)$. 

## Shortest Path of a DAG

We can calculate the shortest path in a [Directed Acyclic Graphs (DAGs)](Directed%20Acyclic%20Graphs%20(DAGs).md) by relaxing edges according to a [topological ordering](Directed%20Acyclic%20Graphs%20(DAGs).md#Topological%20Ordering) of its vertices. 

```
DAG-Shortest-Path(G, s):
	Topologically sort G
	for each v in V do
		dist[v] = INFINITY
		parent[v] = NIL
	
	dist[s] = 0
	
	for each vertex u, in topological order do
		for each vertex v in Adj[u] do
			if dist[v] > dist[u] + w(u, v) then
				dist[v] = dist[u] + w(u, v)
				parent[v] = u
				
	return dist
```

>[!hint]
>Note that this also works with negative edge weights because there can't be cycles, so the greedy procedure will still work.

### Correctness

Assume for contradiction that in the topological ordering, for some vertex $v$, $\text{dist}[v] \neq d(s, v)$. Let the real shortest path be $s\rightsquigarrow w\rightarrow v$.

**Case 1:** $\text{dist}[v] = \infty$.

$w$ comes before $v$ in a topological sorting, and $\text{dist}[w]=d(s, w)$, thus, while iterating through the neighbors of $w$, we would decrease $\text{dist}[v]$ from $\infty$. This is a contradiction.

**Case 2:** $\text{dist}[v] < \infty$.

Again, we would've decreased $\text{dist}[v]$ while iterating through the neighbors of $w$ if $\text{dist}[v]>\text{dist}[w]+w(w, v)$. Thus, this is a contradiction.

### Runtime

This requires $\Theta(V+E)$ time.

Topological sort requires $O(V + E)$ [time](Directed%20Acyclic%20Graphs%20(DAGs).md#Tarjan's%20Algorithm#Runtime). Then our for loop goes through each vertex and edge once for edge relaxation. This gives total time $\Theta(V + E)$. 
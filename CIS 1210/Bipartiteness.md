
## Definitions

>[!definition]
>A graph $G=(V, E)$ is **bipartite** if $V$ can be partitioned into $X, Y$ such that every edge in $E$ has one end in $X$ and the other in $Y$.

We can also say that a graph is bipartite iff it is two colorable. 

>[!lemma]
>If a graph $G$ is bipartite, then it has no odd cycles.

## Algorithm

We assume that $G$ is connected (if it isn't, we run the algorithm on each connected component). 

```
Bipartite(G, s, color):
	color[s] = color
	if color == RED then
		color = BLUE
	else
		color = RED
	for each v in Adj[s] do
		if (color[v] != NIL and color[v] != color) then
			return FALSE
		Bipartite(G, s, color)

	return TRUE
```

Note that this essentially copies the process of doing a [BFS](Graph%20Traversals.md#Breadth-First%20Search%20(BFS)). Thus, we can equivalently say: Run BFS. Color all nodes in $L_{2k}, k\geq 0$ red, and color all nodes in $L_{2k+1}, k\geq 0$ blue. If this results in a valid coloring, $G$ is bipartite. Otherwise, it isn't.

### Correctness

It's obvious that if our algorithm produces a valid two coloring, then $G$ is bipartite. We must show that if our process fails, then no two coloring can exist.

>[!lemma]
>Let $L_0, L_1, \dots$ be the layers produced by a BFS on $G$, starting at $s$. Exactly one of the following must hold:
>1. There is no edge joining two nodes of the same layer. Then, $G$ is bipartite and colored as described above.
>2. There is an edge joining two nodes of the same layer. In this case, $G$ contains an odd cycle, and so it cannot be bipartite.

(Proof in lecture notes.)
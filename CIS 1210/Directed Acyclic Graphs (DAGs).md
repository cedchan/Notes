>[!definition]
>A **DAG** is a **D**irected **A**cyclic **G**raph.

## Topological Ordering

>[!definition]
>A **topological ordering** of a graph $G$ is an ordering of its nodes $v_1, v_2, \dots, v_n$ such that for each edge $(v_i, v_j), i<j$. In other words, the edges point "forward" in the ordering.

>[!theorem]
>$G$ is a DAG iff it has a topological ordering.

*Proof:*

($\impliedby$) Assume for contradiction that $G$ has a topological ordering $v_1, v_2, \dots, v_n$ and a cycle $C$. Let $v_i$ be the lowest-indexed node in $C$. Let $v_j$ be the node that precedes $v_i$ in $C$. Because $i$ has the lowest index, $j>i$, but this contradicts the topological ordering condition.

($\implies$) We will first prove the following lemma:

>[!lemma]
>In every DAG, there is a node with no incoming edges—a **sink**.

*Proof:* Pick any vertex $v$. If it has an incoming edge $(u, v)$, go to $u$. Repeat this until you find a vertex with no incoming edges. Such a vertex must exist because after $n+1$ repetitions, we must visit the same node twice by PHP. But this would create a cycle, which is impossible in a DAG. 

Now, we continue the main proof by showing inductively on the number of nodes that a topological ordering always exists.

**Base Case:** $n=1$. Clearly, with only one node there is a topological ordering. Similarly with $n=2$, there can only be one edge (otherwise it'd be a cycle), so we put the source first and the target second, creating a valid topological ordering.

**Induction Hypothesis:** Assume all DAGs with $k\geq 2$ nodes have a topological ordering.

**Induction Step:** Let $G$ be a DAG on $k+1$ nodes. Let $v$ be a node with no incoming edges (this exists by the previously shown lemma). Then consider the graph $G'=G\setminus\{v\}$. By IH, $G'$ has a valid topological ordering. Then, we put $v$ in front of this ordering. This results in a valid topological ordering for $G$ because $v$ has no incoming edges, so it is impossible to have an edge $(v_i, v)$. 

## Khan's Algorithm

Khan's algorithm for topological sorting follows the procedure that the inductive proof above suggests:
1. Find a node $v$ with no incoming edges
2. Put $v$ next in the topological ordering
3. Remove $v$ and its incident edges
4. Repeat

```
TopoSort(G):
	Let L be a new queue
	Let OUT be a new list

	// Calculate in-degree of each node
	for each v in V do
		for each u in Adj[v] do
			in[u] = in[u] + 1

	// Initialize L
	for each v in V
		if in[v] = 0 then
			L.enqueue(v)

	while L is not empty do
		v = L.dequeue()
		OUT.append(v)
		for each u in Adj[v]
			in[u] = in[u] - 1
			if in[u] = 0 then
				L.enqueue(u)

	return out
```

### Runtime

Khan's algorithm runs in $O(n+m)$ time.

The algorithm checks the degrees of each node initially using $O(n+m)$ time. Then, in the main while loop, it examines each vertex at most once, then looks through each of its incident neighbors, doing constant work on each. Thus, this requires $O(n+m)$ time, giving us a total runtime of $O(n+m)$. 

## Tarjan's Algorithm

Another way to produce a topological ordering is to simply apply [DFS](Graph%20Traversals.md#Depth-First%20Search%20(DFS)).

```
TopoSort(G):
	Perform a DFS on G

	return the nodes in decreasing order of finish time
```

### Runtime

Since this just does a DFS, it requires the same amount of [time](Graph%20Traversals.md#Depth-First%20Search%20(DFS)#Runtime): $O(n+m)$. 

### Correctness

We want to show that if $(u, v)\in E$, then $u.f>v.f$.

**Case 1:** $u.s<v.s$

$v$ must be a descendant of $u$ in the DFS tree (i.e., at time $u.s$, $v$ must be white). Then, by the [parenthesis theorem](Graph%20Traversals.md#Depth-First%20Search%20(DFS)#Parenthesis%20Theorem), $u.s<v.s<v.f<u.f$. 

**Case 2:** $u.s>v.s$

Since $G$ is a DAG and we have edge $(u, v)$, there can't be a path from $v$ to $u$ (otherwise we would form a cycle). Thus, $u.f>v.s$. And since $v.s>v.f$, we have $u.f>v.f$. 
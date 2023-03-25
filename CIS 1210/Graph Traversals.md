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




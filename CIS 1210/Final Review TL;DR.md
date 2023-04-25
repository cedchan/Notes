## Heaps

- **Peek**: $O(1)$
- **extractMax:** $O(\lg n)$
- **buildHeap**: $O(1)$
- **decreaseKey:** $O(\lg n)$
- **minheapify:** $O(\lg n)$

## Huffman

Prefix free encodings that utilize a heap. A greedy algorithm

## Traversal Algorithms

### BFS
- $O(n+m)$
- Output: layers or BFS tree
- Used for unweighted shortest path and bipartite testing

### DFS
- $O(n+m)$
- Cycle detection
- Used in Tarjan's algorithm

## Toposort

### Khan's
- $O(n+m)$

### Tarjan's
- $O(n+m)$

## SCCs

### Kosaraju's
- $O(n+m)$
- Outputs: $G^{SCC}$

## Shortest Path

### Dijkstra's
- $O(m\lg n+n\lg n)$
- REVIEW WHERE RUNTIME COMES FROM

## MSTs

### Prim's
- $O((m+n)\lg n)$
- Very similar to Dijkstra

### Kruskal's
- $O(n\lg^*n)$
- Uses UF data structure

## Hashing
- $\alpha=\frac{n}{m}$, $n$ is the number of elements, $m$ is the number of slots
- Open Addressing
	- Unsuccessful search $O(\frac{1}{1-\alpha})$
	- Successful search $O(\frac1\alpha\lg\frac1{1-\alpha})$
- Simple Uniform Hashing ($m!$ equally likely probe sequences)
	- Unsuccessful search $\Theta(1+\alpha)$
	- Successful search $\Theta(1+\alpha)$
- Linear probing: $h(x)=(h'(x)+i)\mathrm{\ mod\ }m$
	- $m$ probe sequences
- Quadratic probing: $h(x)=(h'(x)+c_1i+c_2i^2){\rm\ mod \ }m$
	- $m$ probe sequences
- Double hashing: $h(x)=(h_1'(x)+ih_2'(x)){\rm\ mod \ }m$
	- $m^2$ probe sequences


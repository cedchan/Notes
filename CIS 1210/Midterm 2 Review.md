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
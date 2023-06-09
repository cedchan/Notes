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



## Todo
- [ ] GS Algorithm
- [x] Greates Common Divisor
- [x] Insertion Sort
- [ ] Running time
- [ ] Code snippets
- [ ] Powers of 2
- [x] Linear and binary search
- [ ] MergeSort
- [ ] Recurrence practice
- [ ] Quicksort
- [x] Counting inversions
- [ ] Selection problem
- [ ] Closest pair
- [x] Stacks and queues
- [ ] Binary heaps
- [ ] Huffman coding
- [ ] BFS and DFS
- [ ] Bipartiteness
- [ ] DAGs and Toposort
- [ ] SCCs
- [ ] Shortest path
	- [ ] Dijkstra
	- [ ] Shortest path in a DAG
- [ ] MST
	- [ ] Prim's
	- [ ] Kruskal's
	- [ ] Reverse-delete
- [ ] Union find
- [x] Hashing
- [x] Tries
- [x] AVL trees
- [x] Skip lists
- [x] Bloom filters
- [x] Red-black trees
	- [ ] Review
- [x] Min cut
	- [ ] Review
- [x] 2-SAT
	- [ ] Review
- [x] Checking sortedness
	- [ ] Review

Huffman question

We first note that there must be four or more characters (or there must be an encoding of length 1). Further, the top of the Huffman tree must be a full binary tree with four leaves (which could represent individual or )

Case 1: There exists a frequency $f_4>0.44$. Since $f_1>0.44$, $f_2+f_3<0.12$. Thus, $f_2, f_3$ would merge first, then merge with the smaller of $f_1, f_4$, leaving an encoding of length 1.

Case 2: There doesn't exist another frequency $>0.44$. Let $f_3, f_4$ be the djkf
## Algorithms

### Greedy Algorithm

A **greedy algorithm** makes decisions based on locally optimal choices. That is, they don't consider what might happen after the current choice, based on the current inputs, is made. Because of this heuristic, greedy algorithms work well for some problems but may produce the wrong answer for others.

Examples of greedy algorithms include [Huffman compression](Huffman%20Encoding.md) and [Dijkstra's Algorithm](Shortest%20Path.md#Dijkstra's%20Algorithm).

## Graph Theory

### Graph Transpose

The **transpose** of a graph $G=(V, E)$ is defined as $G^T=(V, E^T)$, where $E^T=\{(u, v)\mid (v, u)\in E\}$. That is, $G^T$ has the same vertices as $V$, but the directions of the edges are all flipped.

### Source Vertex

A **source vertex** has in-degree 0. That is, there are no edges that lead to source vertices.

### Sink Vertex

A **sink vertex** has out-degree 0. That is, there are no edges that originate from sink vertices.
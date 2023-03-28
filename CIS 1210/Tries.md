Data structure that preprocesses a text to support efficient pattern matching.
- $S$: Set of strings over alphabet $\Sigma$.
- Trie is a rooted tree in which each internal node has $\leq d$ children ($d=|\Sigma|$).
- Each edge is labeled with a letter $\in\Sigma$.
- Each string in $S$ is associated with a leaf in the tree.

Assumption: No string in $S$ is a prefix of another string.
$n=\sum\limits_{s\in S}s$.
$m$: length of the longest string

## Compressed Trie

Also known as "Patricia Trie."

When there is a series of nodes that only have one child each, they all get combined into one node. E.g., $a\rightarrow b\rightarrow c$ becomes $abc$. Thus, it is a [full binary tree](Computer%20Science.md#Graph%20Theory#Full%20Binary%20Tree).

Number of internal nodes: $O(|S|)$
Total number of nodes: $O(|S|)$


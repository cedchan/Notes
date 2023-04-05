>[!definition]
>A **trie** is a tree-based data structure that preprocesses a text to support efficient pattern and prefix matching.
>
>**Prefix matching** involves being given a string and looking for all strings in $S$ that begin with that string.

We use the following notation
- $\Sigma$: Our alphabet of letters
- $S$: Set of strings over $\Sigma$
- $n=\sum\limits_{s\in S}s$ (the total length of all strings)
- $m$: length of the longest string

## Standard Trie

A **standard trie** for $S$ is an ordered tree $T$ with these properties:
- Each node of $T$ except the root is labeled with a character in $\Sigma$
- The children of each internal node have distinct labels
- $T$ has $|S|$ leaves, each of which represents a string in $S$, such that the concatenation of the nodes on the path from the root to the leaf forms the string
- The height of $T$ is equal to the length of the longest string in $S$
- Each internal node has $\leq d$ children ($d=|\Sigma|$)
- The number of nodes of $T$ is at most $n+1$

**Assumption**: No string in $S$ is a prefix of another string. This makes analysis easier. 

In reality, we can resolve the prefix issue in two ways:
1. Add a special character like "$" at the end of each string.
2. Put an "end of word" marker (i.e., field or variable) at the last character node of each word.

### String Search

One of the most basic trie operations is searching to see if $X$ is a string in $S$. We do this by tracing the path from the root to a leaf, choosing nodes by each subsequent character in $X$. If we reach a leaf node, then the string is in $S$. If we either cannot finish finding $X$ before we run out of suitable character nodes, or if we finish $X$ but end on an internal node, then $X$ is not in $S$. 

**Runtime:** $O(m\cdot|\Sigma|)$ for a string of length $m$, since we visit at most $m+1$ nodes of $T$ and spend at $O(|\Sigma|)$ time at each to determine which child to go from.

We can reduce the $O(|\Sigma|)$ part to $O(\log|E|)$ or expected $O(1)$ by mapping characters to children with a secondary search table or hash table.

Thus, we usually say that a string search can be completed in $O(m)$ time.

### Constructing a Trie

Using the assumption that no string is a prefix of another, we can construct a trie by iterating through each string and adding them one by one. We add a string by tracing a path from the root, following the string's characters (just like in a string search), then adding nodes whenever we get stuck.

**Runtime:** Since we do the same sort of path search, we still use $O(m\cdot|\Sigma|)$ time for each string, which can be simplified to $O(m)$ using hash tables and other techniques. Thus, the overall runtime is $O(n)$, where $n$ is the total length of all strings.

## Compressed Trie

>[!definition]
>A **compressed trie**, also known as a **Patricia trie**, enforces the invariant that each internal node has at least two children. 

That is, when there is a series of nodes that only have one child each, they all get combined into one node. E.g., $a\rightarrow b\rightarrow c$ becomes $abc$. 

### Redundance

We say that an internal node $v$ is **redundant** if $v$ has only one child and is not the root.

We call a chain of edges $(v_0, v_1)(v_1, v_2)(v_2, v_3)\dots(v_{k-1},v_k)$ redundant if $v_i, i=1,\dots,k-1$ is redundant, but $v_0, v_k$ aren't. We create a compressed trie by compressing all redundant chains into a single edge $(v_0, v_k)$, whose value is the concatenation of all characters along the chain.

### Properties
- Every internal node has between 2 and $d$ children (where $d$ is the alphabet size).
- $T$ has $s$ leaf nodes. The number of nodes of $T$ is $O(s)$.

Number of internal nodes: $O(|S|)$
Total number of nodes: $O(|S|)$


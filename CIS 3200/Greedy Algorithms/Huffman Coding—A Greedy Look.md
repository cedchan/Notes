---
tags:
  - greedy-algorithms
---
>[!note] 
>See notes on [Huffman encoding](Huffman%20Encoding.md) for CIS 1210 for another perspective.

## Coding Theory

>[!problem]
>**Input:** 
>- Alphabet $\{1,\dots,n\}$
>- Frequencies of each character $f_1,\dots,f_n\in\mathbb N$
>
>**Output:** Prefix-free code $C:\{1,\dots,n\}\to\{0,1\}^*$ (that is, $c_1, c_2,\dots,c_n\in\{0,1\}^*$) such that $\sum_{i\in[1..n]}f_i|c_i|$ is minimized.

What makes a code valid? There are several natural properties that valid codes must satisfy:
1. $c_i\neq c_j$ if $i\neq j$
2. "Prefix free": $c_i$ is not a prefix of $c_j$ if $i\neq j$

Then, to be optimal, a valid code must achieve minimum-length messages.

### Codes as Binary Tree

Every prefix-free code can be represented as a binary tree, where leaves represent elements of the codebook. 

In this view, we can reword our output to be a binary tree $T$ such that the leaves represent encodings $1,\dots,n$, and we minimize $\sum_{i\in[1..n]}f_i\cdot{\rm depth}(i, T)$, where ${\rm depth}(i, T)$ is the depth of the leaf $i$ in the tree $T$. 

We can further specify that $T$ should be full (that is, all internal nodes should have exactly 2 children). Consider the case when $T$ is not full; then we could move the only child of an internal node to the internal node, which would decrease the expected depth while still keeping $T$ prefix-free.

Consider $f_1\leq f_2\leq\dots\leq f_n$ in sorted order. Observe the following two facts:

>[!lemma]
>Any full binary tree with $\geq 2$ leaves must have 2 leaves that are siblings at the deepest level.

**Proof.** Consider the deepest node $v$. Consider $v$'s parent. Since we know $T$ is full, $v$'s parent must have another child $u$. If $u$ is a leaf, then we have our siblings. If it isn't then, it's deeper than $v$, contradicting that $v$ is the deepest node.

>[!lemma]
>Suppose ${\rm O\small PT}$ is a full binary tree such that it minimizes the objective function $f({\rm O\small PT})$. Then, there exists $\widetilde{\rm O\small PT}$ such that $f_n, f_{n-1}$ (the smallest occurrences) exist as siblings in the deepest level and such that $f(\widetilde{\rm O\small PT})=f({\rm O\small PT})$.

**Proof.** Consider ${\rm O\small PT}$. If $n, n-1$ are on the deepest level, we're done. Otherwise, let $h'$ be the height of $n$, and $h$ be the height of the tree. Let $v$ be the deepest node (and isn't $n,n-1$). Swap $n$ and $v$. Then, the objective function changes by $hf_n+h'f_v-hf_v-h'f_n$ which is optimal.

Supposing these facts are true, let $K_1$ be the set of all full binary trees such that the leaves $1,\dots,n$ have $n,n-1$ as siblings in the deepest node. Let $T\in K_1$. Then,
$$\begin{align}
f(T)&={\rm depth}(n-1, T)(f_{n-1}+f_n)+\sum_{i=1}^{n-2}f_i{\rm depth}(i,T)\\
&=({\rm depth}[\pi(n-1),T]+1)(f_{n-1}+f_n)+\sum_{i=1}^{n-2}f_i{\rm depth}(i,T)\\
&=f_{n}+f_{n-1}+{\rm depth}[\pi(n-1),T](f_{n-1}+f_n)+\sum_{i=1}^{n-2}f_i{\rm depth}(i,T)
\end{align}$$
Then,
$$\min_Tf(T)=f_n+f_{n-1}+\min_T\sum_{i=1}^{n-2}f_i\cdot{\rm depth}(i,T)+(f_{n-1}+f_n)\cdot{\rm depth}(\pi(n-1),T)$$
This is good algorithmically because the second minimization has the same form as our original problem. Note that the last term is like merging $f_n, f_{n-1}$ and putting them on $\pi(n-1)$ (that is, their shared parent), then assigning that node their combined frequency. 
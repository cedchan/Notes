>[!definition] 
>A **red-black tree** is a BST [LINK] where each node is colored either red or black. The red-black properties guarantee that the tree is approximately balanced. 
>
>The red-black properties are
>1. Every node is either red or black
>2. The root is black
>3. Every leaf (nil) is black
>4. If a node is red, its children are black
>5. For each node, all paths from the node to descendant leaves contain the same number of black nodes.

Let the **black-height** $bh(x)$ of a node be the number of black nodes on a path from, but not including $x$ to a leaf. 

>[!lemma] 
>The subtree rooted at $x$ contains at least $2^{bh(x)}-1$ internal nodes.

*Proof.* We use strong induction on the height of $x$.

**Base Case:** At height 0, $x$ must be a leaf, so the root has indeed $2^0-1=0$ internal nodes.

**Induction Hypothesis:** Assume the claim holds for all nodes height $0\leq j\leq k$. 

**Induction Step:** For a node $x$, its children must have black-height of $bh(x)$ or $bh(x)-1$, depending on if $x$ is red or black. Thus by IH, we can say that each child has at least $2^{bh(x)-1}-1$ internal nodes. It follows that $x$, since it has 2 such subtrees (and itself), has at least $2(2^{bh(x)-1}-1)+1=2^{bh(x)}-1$ internal nodes.

>[!theorem]
>A red-black tree with $n$ internal nodes has height at most $2\lg(n+1)$. 

*Proof.* Let $h$ be the height of the tree. By property 4, at least half the nodes on any path from root to leaf must be black. Thus, the black-height of the root must be at least $\frac{h}{2}$. By the previous lemma, 
$$\begin{align}
n&\geq2^{\frac h2}-1 \\
h&\leq2\lg(n+1)
\end{align}$$
Thus we can use worst-case logarithmic time for typical binary search operations (although red-black trees must have their own implementations for `Insertion`, `Deletion`, and `Rotation`).



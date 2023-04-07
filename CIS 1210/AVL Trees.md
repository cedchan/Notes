
## Binary Search Tree

>[!definition]
>The **binary search tree property** is: Let $x$ be a node in a binary search tree. If $y$ is a node in the left subtree of $x$, then $y.key\leq x.key$. If $y$ is in the right subtree of $x$, then $y.key\geq x.key$.

All basic operations on binary trees run in $O(h)$ time. In the worst case, each node has only one child—that is, the tree is essentially in the form of a linked list. In this case, $h=n$. In order to maximize runtime, we want $h=\lg n$. 

## Definition of an AVL Tree

>[!definition]
>The **height-balance property** states the for every internal node $v$ of $T$, the hieghts of the children of $v$ differ by at most 1. 
>
>An **AVL tree** is any tree that satisfies the height-balance property. (It is named after its inventors Adel'son-Vel'skii and Landis.)

Note that by definition, any subtree of an AVL tree is also an AVL tree.

>[!theorem]
>The height of an AVL tree with $n$ entries is $O(\lg n)$.

*Proof*: It is easier to show that $n(h)$, the minimum number of nodes in an AVL tree of height $h$, grows exponentially. 

The base cases are simple: $n(1)=1, n(2)=2$, since having height 1 must mean having some node in the tree, and height 2 necessarily has 1 node on 2 levels. For an arbitrary height $h$, note that at least one child must be of height $h-1$. Then, by the AVL definition, the other child must be of height at least $h-2$. Thus, for $h\geq 3$, we can write the following recurrence relation:
$$
n(h)=1+n(h-1)+n(h-2)
$$
This is the Fibonacci sequence, which is exponential. More specifically: $n$ is clearly a strictly increasing function of $h$, since it's the sum of positive numbers. Thus, $n(h-1)>n(h-2)$, which allows us to say
$$\begin{align}
n(h)&>2\cdot n(h-2) \\
&>2^2\cdot n(h-2\cdot 2) \\
&>2^3\cdot n(h-2\cdot 3) \\
&\ \; \vdots \\
&>2^i\cdot n(h-2i)
\end{align}$$
We know $n(1), n(2)$, so we want to pick $i$ such that $h-2i=1$ or $h-2i=2$. This gives $i=\left\lceil\frac h2\right\rceil-1$. Substituting into our above inequality, we get
$$
\begin{align}
n(h)&>2^{\left\lceil\frac h2\right\rceil-1}\cdot n\left(h-2\left\lceil\frac h2\right\rceil-1\right) \\
&\geq 2^{\left\lceil\frac h2\right\rceil-1}\cdot n(1) \\
&>2^{\frac h2-1} & \text{(since $n(1)=1)$} \\
\lg n(h) &>\frac{h}{2}-1 & \text{(log both sides)}\\
h&<2\lg n(h)+2 \\ && \square
\end{align}
$$
Therefore, the height of an AVL tree of $n$ elements is at most $2\lg n+2=O(\lg n)$. 

## Insertion

We begin by normally inserting to $T$ as any other BST.

Adding a node $w$ to $T$ may imbalance all nodes on the path from the root to $w$, so after the initial insertion we must rebalance the tree.

We define the following:
- $z$: The unbalanced first node going up from $w$ to the root
- $y$: The child of $z$ with greater height
- $x$: The child of $y$ with higher height

We rebalance the subtree by calling the **trinode restructuring** function `Restructure()`. This temporarily relabels $x, y, z$ as $a, b, c$ such that an inorder traversal of $T$ would go to $a$ first, then $b$, then $c$. The restructuring then makes $b$ the root with $a$ and $c$ as its children. The children of $a$ and $c$ are the four previous children of $x, y, z$ that aren't $x, y$. 

This restructuring is called a **rotation**. If $b=y$, it is a **single rotation** and can be visualized as rotating $y$ over $z$. If $b=x$, it is a **double rotation** and can be visualized as rotating $x$ over $y$, then over $z$.

```
Input: Node x of BST T that has both parent y and grandparent z
Output: Tree T after trinode restructuring involving x, y, z

Restructure(x):
	Let (a, b, c) be a left-to-right (inorder) listing of x, y, z.
	Let (T0, T1, T2, T3) be a left-to-right listing of the four subtrees of x, y, z not rooted at x, y, z.

	Replace the subtree rooted at z with a subtree rooted at b.
	
	Let a be the left child of b and let T0, T1 be the left and right subtrees of a, respectively.
	
	Let c be the right child of b and let T2, T3 be the left and right subtrees of c, respectively.
```

**Runtime:** $O(1)$ (Noting that we must do the initial add in $O(\lg n)$ time)

Conceptually, we pull up the tall child of $x$ and push down the short child of $z$. Thus, at the end of `Restructure()` the nodes in the subtree rooted at $b$ are balanced. This *locally* restores height balance at $x, y, z$. But because $b$ replaces $z$, which was taller by 1 unit, all of $z$'s unbalanced ancestors become balanced. So `Restructure()` in fact balances the tree *globally*.

## Deletion

We also begin delete like any other BST, then rebalance the tree. Specifically, some node on the path from the root to $w$, the parent of the deleted node, may be imbalanced.

We define the following:
- $z$: The first unbalanced node going from $w$ to the root
- $y$: The taller child of $z$ (note that it is not an ancestor of $w$)
- $x$: The child of $y$ on the same side as $y$ (i.e., if $y$ is a left child, then $x$ is a left child, and if $y$ is a right child, then $x$ is a right child)

We then call `Restructure()`.

Since this restructuring may reduce the height of the subtree rooted at $b$ by 1, some ancestor of $b$ may also become unbalanced. Thus, we must continue going on the path from $w$ to the root and restructuring as necessary. This, however, will still only happen $O(\lg n)$ times, which maintains our runtime of $O(\lg n)$.
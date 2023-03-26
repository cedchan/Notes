>[!summary]+
>

## Introduction

>[!definition]
>A **disjoint-set data structure** maintains a collection $\mathcal S=\{S_1, S_2, \dots, S_k\}$ of disjoint synamic sets. Each set is identified by a representative $r\in S_i$. 
>
>For CIS 1210, we refer to this structure as **Union Find (UF)**.

Union Find supports the following operations:
- `MakeSet(x)`: Creates a new set whose only member (and thus representative) is $x$. Since sets are disjoint, $x$ must not be in any other set.
- `Union(x, y)`: Unions the two sets containing $x$ and $y$
- `Find(x)`: Returns a pointer the the representative of the set containing $x$. (Note that if $x$ and $y$ belong to the same set, `Find(x) == Find(y)`.)

In our implementation, we view each set as a directed tree in no particular order, where the root is the representative (the root is its own parent, all other edges point "up"). We then define the rank of each node to be the height of the tree rooted at that node. This turns out to only be an upper bound for [path compression](Union%20Find.md#Path%20Compression).

## Make Set

The implementation of MakeSet is straightforward:

```
MakeSet(x):
	parent[x] = x
	rank[x] = 0
```

**Time:** $O(1)$

## Find

We can find the representative of $x$'s set by tracing parent pointers up to the root.

```
Find(x):
	while x != parent[x] do
		x = parent[x]
	return x
```

**Time:** $O(h)$, where $h$ is the height of the tree.

The two different implementations of UF, by rank and path compression, come from this idea: that making the tree shallow increases efficiency. 

## Union by Rank

The idea of union by rank is that when we merge two trees, we make the root of one a child of the other. In this manner, to minimize the height of the tree, we let the larger of the two be the parent. Then, the rank of that node will increase only when the two trees are of equal height. In this case, it increases by 1 only.

```
Union(x, y):
	r_x = Find(x)
	r_y = Find(y)
	if r_x == r_y then
		return
	if rank(r_x) > rank(r_y) then
		parent[r_y] = r_x
	else
		parent[r_x] = r_y
		if rank[r_x] == rank[r_y] then
			rank[r_y]++
```

**Time:** $O(1)$

## Path Compression

We can make trees shallower by implementing a new Find. The idea is generally the same: we trace parent pointers to the root. But this time, if the parent of $x$ is not already the root, we recursively call Find on the parent and set the result to be the new parent of $x$. That is, we make $x$ and all the nodes traced back to the representative have the representative be their parent.

```
Find(x):
	if x != parent[x] then
		parent[x] = Find(parent[x])
	return parent[x]
```

**Time:** The amortized cost of Find and Union both drop to $O(1)$ from $O(\lg n)$ from this change.

(Proof of amortization in lecture notes.)

## Finding Connected Components

We can easily create connected components and check membership using UF.

First, we construct sets that consist of members of the same CC.

```
ConnectedComponents(G):
	for each v in V do
		MakeSet(v)
	for each e = (u, v) in E do
		if Find(u) != Find(v) then
			Union(u, v)
```

Then, we can check membership with

```
SameComponent(u, v):
	return Find(u) == Find(v)
```


>[!definition]
A **binary heap** is a **nearly complete binary tree**—i.e., a tree that is filled on all levels except possibly the lowest, which is filled from the left up to a certain point.
>
>Each node satisfies a heap property. There are two types:
>1. Max heap: $A[\text{parent}(i)]\geq A[i]$ (i.e., parents are always larger)
>2. Min heap: $A[\text{parent}(i)]\leq A[i]$ (i.e., parents are always smaller)

Heaps can be represented as arrays, where elements are read level by level, left to right. The indices of parents and children are thus given by

```
parent(i): return floor(i/2)
left(i): return 2i
right(i): return 2i + 1
```

Note that the size of the heap is not necessarily equal to the size of the array, so we store separate variables `A.heapsize` and `A.size` for these.

## Max-Heapify

For a max heap, the maxHeapify maintains the heap property. For an index $i$, it assumes the trees rooted at $\text{left}(i)$ and $\text{right}(i)$ follow the property. Then, it checks whether $i$ does, and if it doesn't (i.e., one of its children is larger), it switches the child with $i$. Finally, since the new tree rooted at the moved $i$ might not meet the property, it recursively calls itself on that new subtree.

```
maxHeapify(A, i):
	l = left(i)
	r = right(i)
	largest = i
	if l <= A.heapsize and A[l] > A[i]
		largest = l
	if r <= A.heapsize and A[r] > A[largest]
		largest = r
	if largest != i
		exchange A[i] with A[largest]
		maxHeapify(A, largest)
```

**Complexity:** $O(\lg n)$ time, or $O(h)$, where $h=\lg n$ is tree height.

## Building a Heap

Given an unsorted array $A[1..n], n=|A|$, we run maxHeapify on the nodes above right above the leaves and move toward the root. We start at the bottom because maxHeapify assumes the children's trees are max heaps.

```
buildMaxHeap(A):
	A.heapsize = A.length
	for i = floor(A.length / 2) downto 1
		maxHeapify(A, i)
```

Note that we start at the level above the leaves because maxHeapify will do nothing when called on a leaf.

### Correctness

The proof inductively shows that for every iteration of the for loop, the tree rooted at nodes $i+1$ to $n$ are all max heaps (i.e., it stays correct throughout the function).

**Base:** The leaves are trivially max heaps.

**Step:** The children of $i$ have indices greater than $i$. Thus by the hypothesis they are max heaps. Therefore maxHeapify is able to make $i$ a max heap as well.

**Termination:** The loop ends when $i=0$. Then all nodes are max heaps.

### Runtime

The tight bound uses the following points, for an $n$-element heap:
1. It has height $\lfloor \lg n\rfloor$
2. It has at most $\left\lceil\frac{n}{2^{h+1}}\right\rceil$ nodes at height $h$
3. maxHeapify uses $O(h)$ time

Then,
$$
T(n)=\sum_{n=0}^{\lfloor\lg n\rfloor}\left\lceil\frac{n}{2^{h+1}}\right\rceil O(h)=O\left(n\sum_{h=1}^{\lfloor\lg n\rfloor}\frac{h}{2^h}\right)=O\left(n\sum_{h=1}^\infty\frac{h}{2^h}\right)=O(n)
$$

## Heapsort

We can sort an array by building a heap from it, then since we know that the first element of the heap is always the max, we can put that in the right position, shrink the heap, and continue until the heap is empty.

```
heapsort(A):
	buildMaxHeap(A)
	for i = A.length downto 2
		exchange A[1] with A[i]
		A.heapsize = A.heapsize - 1
		maxHeapify(A, 1)
```

## Priority Queues

>[!definition]
>A **priority queue** is a data structure that maintains a set $S$ where each element has a key. It then has the following operations:
>1. $\text{insert}(S,x)$ inserts $x$ into $S$
>2. $\text{maximum}(S)$ returns the element of $S$ with the largest key
>3. $\text{extractMax}(S)$ remove and returns the element with the largest key
>4. $\text{increaseKey}(S,x,k)$ increases the value of $x$ to $k$ (assumes $k\geq \text{key}(x)$)
>
>The same can be applied for a min priority queue.

## Heap Maximum

The heap implementation of a priority queue's maximum is

```
heapMaximum(A):
	return A[1]
```

**Complexity:** $O(1)$ time

## Heap Extract Maximum

Similar to [Heapsort](Heaps.md#Heapsort), it swaps the first and last elements, then decreases the size of the heap by 1 (so that the new last element, a.k.a. the max, is not affected by the next step), then calls maxHeapify.

```
heapExtractMax(A):
	if A.heapsize < 1
		error
	max = A[1]
	A[1] = A[A.heapsize]
	A.heapsize = A.heapsize - 1
	maxHeapify(A, 1)
	return max
```

**Complexity:** $O(\lg n)$, from maxHeapify

## Heap Increase Key

It is sort of like the opposite method of maxHeapify: We take recursively go upward and swap the node with its parent until it is greater than all its children. This swap maintains the heap property for nodes below because the grandparent node is greater than its children.

```
heapIncreaseKey(A, i, k):
	if key < A[i]
		error
	A[i] = k
	while i > 1 and A[parent(i)] < A[i]:
		exchange A[i] with A[parent(i)]
		i = parent(i)
```

**Complexity:** $O(\lg n)$, for at most $h$ levels up.

## Heap Insert

We insert by creating a "dummy" leaf of value $-\infty$ at the end of the heap, then increase its value with heapIncreaseKey.

```
maxHeapInsert(A, k):
	A.heapsize = A.heapsize + 1
	A[A.heapsize] = -INFINITY
	heapIncreaseKey(A, A.heapsize, k)
```

**Complexity:** $O(\lg n)$ time


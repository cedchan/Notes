## Deterministic Quick Sort

The idea of deterministic quick sort is that we choose some pivot, then partition along that pivot: that is, sort the array such that all elements larger than the pivot are after the pivot, and all elements smaller than the pivot are before the pivot. Doing this recursively on each side of the array after partitioning, we eventually sort the whole array.

```
QuickSort(A[lo..hi]):
	if hi <= lo:
		return
	else:
		pIndex = floor((lo+hi)/2)
		loc = Partition(A, lo, hi, pIndex)
		QuickSort(A[lo..loc-1])
		QuickSort(A[loc+1..hi])
```

```
Partition(A, lo, hi, pIndex):
	pivot = A[pIndex]
	swap(A, pIndex, hi)
	left = lo
	right = hi-1
	while left <= right:
		if (A[left] <= pivot):
			left = left + 1
		else:
			swap(A, left, right)
			right = right - 1
	swap(A, left, hi)
	return left
```

The running time of the algorithm is given by 
$$T(n)=\begin{cases}
1 & n=1 \\
T(n-1)+cn & n\geq 2
\end{cases}$$
which simplifies to $\Theta(n^2)$. 

## Randomized Quick Sort

Instead of always chosing the same pivot, we randomly select a pivot.

>[!theorem]
>For any input array of size $n$, the expected number of comparisons made by randomized quick sort is $$2n\ln n+O(n)=\Theta(n\lg n)$$

*Proof.* We define the following:
- $y_1, y_2, \dots, y_n$: The elements of $A$ in sorted order
- $X$: The random variable denoting the total number of pairwise comparisons made
- $X_{i,j}$: The random variable denoting the total number of times elements $y_i, y_j$ are compared

Note the following:
- Comparisons are only done in `Partition`
- Two elements are compared iff one is a pivot

Let $X_{i,j}^k$ be an indicator random variable that is 1 if $y_i, y_j$ are compared on the $k$-th call to `Partition`. Then we have
$$X=\sum_{i=1}^{n-1}\sum_{j=i+1}^nX_i,j, \qquad X_{i,j}=\sum_kX_{i,j}^k$$
We then calculate ${\bf E}[X_{i,j}]$ by LOE
$${\bf E}[X_{i,j}]=\sum_k{\bf E}[X_{i,j}^k]=\sum_k\Pr[X_{i,j}^k=1]$$
Let $t$ be the iteration of the first `Partition` call in which some element in $y_i, y_{i+1}, \dots, y_j$ is used as a pivot. Note that $y_i, y_j$ are compared only when $k=t$, and never before and after.

Plugging this result into our previous expectation equation, we can eventually simplify to $2n\ln n+O(n)$.
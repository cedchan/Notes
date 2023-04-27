>[!definition]
>Given a sequence of numbers $a_1, a_2, \dots, a_n$, we say indices $i<j$ form an **inversion** if $a_i>a_j$. That is, if $a_i$ and $a_j$ are out of order.

## Algorithm

```
Input: Two sorted lists A and B
Output: A sorted list containing all elements in A and B as well as the number of inversions assuming all elements in A precede those in B

Merge-and-Count(A, B):
	L = []
	currA = 1
	currB = 1
	count = 0
	while currA <= A.length && currB <= B.length:
		a = A[currA]
		b = B[currB]
		if a < b:
			L.append(a)
			currA = currA + 1
		else:
			L.append(b)
			remaining = A.length - currA + 1
			count = count + remaining
			currB = currB + 1
	Once one list is empty, append the remainder of the other list to L

	return count and L
```

```
Input: A list L of n distinct numbers
Output: A sorted version of L as well as the number of inversions in L

Sort-and-Count(L):
	if n == 1:
		return 0 and L

	m = ceil(n / 2)
	A = L[1, ... , m]
	B = L[m + 1, ... , n]
	(r_A, A) = Sort-and-Count(A)
	(r_B, B) = Sort-and-Count(B)
	(r, L) = Merge-and-Count(A, B)

	return r_A + r_B + r and the sorted list L
```

## Runtime

`Merge-and-Count`'s running time is $O(n)$ because each `while` iteration takes constant time, and in each iteration, we add one element to the output that will never be seen again. 

Thus for `Sort-and-Count` we have the following recurrence:
$$T(n)=\begin{cases}2T\left(\frac n2\right)+O(n) & n>1 \\
1 & {\rm otherwise}\end{cases}$$

This is the same runtime as `MergeSort`, so we know it's equal $T(n)=O(n\lg n)$.
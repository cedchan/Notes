## Lower Bound on Sorting

**Question:** Does there exist a $o(n\log n)$ sorting algorithm?

Naturally, there are two answers to the question: yes or no. We can show the answer's yes by describing such an algorithm. Showing the answer is no proves more difficult. 

To show that a specific algorithm $ALG$ is not $o(n\log n)$ time, we must show $\exists A[1..n]$ such that $ALG(A)$ takes $\Omega(n\log n)$ steps.

>[!definition]
>The **comparison-based model** is an algorithm that can access the input array $A[1..n]$ via comparisons. 
>
>That is it can't directly read the array, but can ask questions like, Is $A[i]\geq A[j]$?

This is our **model of computation**—a sort of restriction on the "basic" things our algorithm can do.

>[!definition]
>A **decision tree** is a rooted binary tree with labels on the nodes and edges, where the labels on edges incident on the same parent node are different.

For this use, the labels on non-leaf nodes are "comparison questions" ($A[i]\geq A[j]?$) and the labels on leaf nodes are "outputs." Naturally, the labels on edges are "answers."

The execution of $ALG$ can thus be seen as a root-to-leaf path. When the algorithm is executed on different arrays, the comparisons will result in different answers, following a path.

It follows that the worst-case running time is the depth $h$ of the decision tree. We want to show, then, that $h=\Omega(n\log n)$.

We "augment" the array by adding additional information about the original array. Specifically, we mark the original position of each element. So if we have $A$ that is sorted into $B$, and we have $B[i]$ marked with $j$, then $A[j]=B[i]$. 

To be correct, any algorithm must be able to handle any arbitrary input, so it must handle all permutations of this auxiliary info (that is, all possible orderings). There are $n!$ such permutations, meaning that there must be $n!$ leaves. 

>[!claim]
>Any binary tree with $\geq n!$ leaves has depth $\Omega(n\log n)$. 

**Proof.** If we have depth $h$, then the number of leaves must be $\leq 2^h$. 
$$\begin{align}
\left(\frac n2\right)^\frac{n}{2}&\leq n! \\
\implies\frac n2\lg\frac n2&\leq h
\end{align}$$
The second line comes from plugging in the first line into our observation about the number of leaves.

## Linear Sorting

If we change our model of computation, we can achieve a faster running time.

**Input:** Array $A[1..n]$ of integers in the range $[1..R]$. 

**Output:** Sorted version of $A$. 

### Count Sort Algorithm

**Runtime:** $O(n+R)$

While technically linear, this is "cheating" in the sense that $R$ could be very large.

**Algorithm:** Create an auxiliary array $C$ of size $R$. Scan through $A$ and increment the corresponding slot in $C$. (That is, $C[A[i]]\gets C[A[i]]+1$, for each $i$).

Then a linear scan through $C$ can be used to fill in the sorted array $B$. 

### Radix Sort Algorithm

**Runtime:** $O(n)$ when $R=n^{100}$

To go from the count sort algorithm to the radix sort algorithm, we make some changes: First, instead of making $C$ a counter array, we make it an array of linked lists. Each linked list contain the actual elements of $A$, in the order they appear in $A$. 

Now when we produce $B$, we can directly place the elements in each linked list into the array. 

**Algorithm:** First, we write the numbers as base $k$. Then, to write a number $\leq R$ in base $k$, we need $\log_k R$ digits. Then we use the count sort algorithm on each "digit" of the input. 

The **principle of deferred decisions** allows us to not set a specific $k$ until after we complete the analysis of the algorithm. Then, we can maximize efficiency at the end.

We can think of our converted $A$ as a 2D array with $n$ rows and $\log_kR$ columns. We start by using count sort on the least significant (rightmost) digit. We know the range for each digit is $k$, so this takes $O(n+k)$ time. 

Doing this for each row, we get $O(n+k)\cdot O(\log_kR)=O(n+k)\cdot O\left(\frac{\log n}{\log k}\right)$. 

>[!warning]
>review


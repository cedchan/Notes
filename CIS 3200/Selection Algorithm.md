---
tags:
  - divide-and-conquer
---

>[!problem]
>**Input:** Array $A[1..n]$ and $k\in\mathbb [1..n]$
>**Output:** $k$, the $k$-th smallest element in $A$

## Simple Baselines

1. If $k=1$, this is the problem of finding the minimum, which can be done in $O(n)$ time.
	1. Generalizing to any $k$, we first find the $(k-1)$-th, then do it again without including it. This gives $O(kn)=O(n^2)$ time.
2. If we sort $A$ (we can do this in $O(n\log n)$ time), then we can answer any particular problem in $O(1)$ time.

It seems as though the fastest algorithm would sort the array first, but intuitively sorting—which must return an entire array—is more complex than the selection problem—which returns one. A linear-time selection algorithm can also help achieve $O(n\log n)$ running time for [deterministic quick sort](Archive/Spring%202023/CIS%201210/Quick%20Sort.md#Deterministic%20Quick%20Sort).

## Divide-and-Conquer Algorithm

**Approach:**
- Divide and conquer
- ${\rm S\small ELECT}(A, k)$ in $O(n)$ time

Let's say we partition $A$ into $L$ (left) and $R$ (right), around some pivot. There are three cases to consider:
1. $|L|=k-1$. Here, we simply output the pivot
2. $|L|\geq k$. Here, we run ${\rm S\small ELECT}(L, k)$
3. $|L|<k$. Here, we run ${\rm S\small ELECT}(R, k-|L|-1)$

**Runtime:** $T(n)$ is the maximum running time on an array of size $n$.
$$\begin{align}
T(n)&=O(n)+\begin{cases}
1 & |L|=k-1 \\
T(|L|)&|L|>k-1 \\
T(|R|) & |L|\leq k-1
\end{cases}
\end{align}$$
In the best case, when we choose the right pivot (the median), we get
$$\begin{align}
T(n)&=T\left(\frac n2\right)+O(n) \\
&=T\left(\frac n4\right)+c\frac n2+cn \\
&=T\left(\frac n8\right)+c\frac n4+c\frac n2+cn \\
&\quad\vdots \\
&=\sum_{h=1}^{\lg n}\frac{cn}{2^h} \\
&=cn\sum_{h=1}^{\lg n}\frac1{2^h} \\
&\leq 2cn \\
&=O(n)
\end{align}$$
If we choose a bad case, though—such as if our pivot is the minimum or the maximum—we'd instead have
$$\begin{align}
T(n)&=O(n)+\begin{cases}
1 & |L|=k-1 \\
T(|L|)&|L|>k-1 \\
T(|R|) & |L|\leq k-1
\end{cases} \\
&=O(n)+T(n-1) \\
&=cn+c(n-1)+T(n-2)\\
&\quad\vdots \\
&=O(n^2)
\end{align}$$
## Linear Algorithm

The key idea for achieving linear runtime is that we don't need the exact median to achieve the best-case runtime from above. So long the pivot is close enough to the median, we can achieve linear runtime.

Suppose our pivot satisfies the following: $|L|,|R|\geq \frac{3n}{10}$:
$$\begin{align}
T(n)&\leq O(n)+T\left(\frac{7n}{10}\right) \\
&=cn+T\left(\frac{7n}{10}\right) \\ 
&\leq cn+c\frac{7}{10}+T\left(\left(\frac{7}{10}\right)^2n\right) \\
&\quad\vdots\\
&\leq cn\underbrace{\sum_{h=0}^{\lg n}\left(\frac7{10}\right)^h}_{<10} \\
&\leq 10cn \\
&=O(n)
\end{align}$$
A problem remains: how do we ensure $|L|,|R|\geq\frac{3n}{10}$?

Let's say we divide $A$ into groups of 5.
1. Compute the median of each group, which takes $O(n)$ time.
2. Find the medan of the medians with recursion.
![](截屏2024-01-31%20下午4.37.30.png)
We know that each median, with the exception of the last group, is greater than or equal to 3 other elements (including itself, in the group of 5), and we know the median of medians is greater than $\frac12\cdot\frac n5$ of the medians. In total, we know the median of medians is greater than $\frac{3n}{10}$ elements.

Adding this computation time back into our recurrence, we have runtime
$$\begin{align}
T(n)&\leq O(n)+T\left(\frac7{10}\right)+O(n)+T\left(\frac n5\right)
\end{align}$$

### Substitution Method

>[!claim]
>Let $T(n)\leq O(n)+T\left(\frac7{10}\right)+O(n)+T\left(\frac n5\right)$.
>
>$$\exists c'>0\text{ s.t. } T(n)\leq c'n$$

**Proof.** We pick a large-enough $c'$ so that $T(m)<c'm$ for $m\leq n$. 

*Inductive Hypothesis:* $T(n)\leq c'n$.

*Base Case:* $T(1)=1$

*Inductive Step:* ${\rm IH}\implies T(n)<c'n$
$$\begin{align}
T(n)&\leq cn+T\left(\frac{7n}{10}\right)+T\left(\frac{n}{5}\right) \\
&\leq cn+c'\left(\frac{7n}{10}\right)+c'\left(\frac{n}{5}\right) \\
&\leq n\left(c+\frac{7c'}{10}+\frac{c'}{5}\right)
\end{align}$$
We pick $c'$ such that 
$$c+\frac{7c'}{10}+\frac{c'}{10}\leq c'$$
That is,
$$\begin{align}
c+\frac{7c'}{10}+\frac{c'}{5}=c+\frac{9c'}{10}&\leq c' \\
c&\leq\frac{c'}{10} \\
10c&\leq c'
\end{align}$$

>[!hint]
>When using the substitution method, the inductive hypothesis cannot be of the form $T(m)=O(\cdot), m<n$ because using big-$O$ talks about the limit behavior of the functions, so it's a tautology. Instead, we must use the form $\exists c'>0 \text{ s.t. } T(m)\leq c'\cdot f(n)$, where $f(n)$ is our predicted runtime.


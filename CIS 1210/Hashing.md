>[!summary]+
>**Motivation:** Given a universe of keys $U$, we want a data structure that efficiently supports `Insert(), Delete(), Search()`.
>
>[Direct Address Table](Hashing.md#Direct%20Address%20Table)
>- Array has one element per key
>- Lots of unused space
>**Complexity:** $O(1)$ time for all operations
>
>[Simple Uniform Hashing Assumption](Hashing.md#Simple%20Uniform%20Hashing%20Assumption)
>
>
>[Chaining](Hashing.md#Chaining)
>
>[Open Addressing](Hashing.md#Open%20Addressing)
>
>

--- 

**Motivation:** Given a universe of keys $U$, we want a data structure that efficiently supports `Insert(), Delete(), Search()`.

## Direct Address Table

We create a table with one element for each key in the universe. Then we can insert, delete, and search in worst-case $O(1)$ time.

The problem is that there is a lot of wasted space.

## Hashing

Instead, we create an array $T$ where the number of slots is much smaller than the size of the universe, and some function $h: U\rightarrow \mathbb [0..m-1]$ (where $m$ is the size of $T$) converts the keys into indexes of the array.

By the PHP, two keys must map to the same location, what is known as a **collision**. Resolving collisions is much of what hashing is about

### Chaining

One method is to store a LinkedList in each element of the array. Then, multiple values can be stored at the same index.

```
Insert(T, x)
	Add x to the head of T[h(x.key)]
```

**Time:** $O(1)$

```
Search(T, k)
	Go and find element with key 
```

**Time:** $O(n)$

```
Delete(T, x)
	Delete x from T[h(x.key)]
```

**Time:** $O(1)$

### Open Addressing

- All elements are stored in the table
- $\alpha\leq 1$
- To search or insert an element, we probe the table to find an empty spot

Before, $h: U \rightarrow [0..m-1]$. Now, $h: U\times[0..m-1]\rightarrow[0..m-1]$. The interval $[0..m-1]$ in the domain is the probe number.

```
Insert(T, x)
	i = 0
	repeat
		j = h(k, i)
		if T[j] is empty
			T[j] = k
			return
		else
			i++
	until i == m
```

```
Search(T, k)
	i = 0
	repeat
		j = h(k, i)
		if T[j] == k then
			return j
		else
			i++
	until i == m or T[j] is empty
```

>[!warning]
>This only works when there is no deletion because the search stops at the empty slot.
>
>One possible solution is inserting a dummy key wherever you delete.

## Simple Uniform Hashing Assumption

- $n$: # of elements in the hash table
- $m$: Size of the table $T$
- $\alpha=\frac{n}{m}$: Load factor

Each key is equally likely to be mapped to any of the $m$ slots independent of how the other keys are hashed.

### Unsuccessful Search

By the Simple Uniform Hashing Assumption, in expectation the time for an unsuccessful search is $O(1+\alpha)$.

**Proof:** Searching for key $k$.

$X$: r.v. denoting the amount of time needed to declare $k\notin T$.
$Y$: r.v. denoting the slot in the table that $h(k)$ is in.

$$
\begin{align}
	\mathbb{E}[X]&=\sum_i\Pr[Y=i]\cdot\mathbb{E}[X\mid Y=i] \\
	&=\sum_{i=0}^{m-1}\Pr[h(k)=i]\cdot\mathbb{E}[X\mid h(k)=i] \\
	&=\sum_{i=0}^{m-1}\frac{1}{m}\cdot\frac{n}{m} \\
	&=\boxed{\frac{n}{m}}=\alpha
\end{align}
$$
**Total time:** $\Theta(1+\alpha)$

### Successful Search

Let $a_1, a_2, \dots, a_n$ be the order in which the elements are inserted into $T$.

$Y$: r.v. denoting the element we are searching
$X$: r.v. denoting the amount of time needed to search for the element
$$
\begin{align}
	\mathbb{E}&=\sum_{i=1}^{n}\Pr[Y=i]\cdot\mathbb{E}[X\mid Y=i] \\
	&=\sum_{i=1}^n\frac{1}{n}\cdot\mathbb{E}\left[1+\sum_{j=i+1}^nZ_{ij}\right] \\
	&\text{(where $Z_{ij}=1$ if $i,j$ mapped to same value, 0 o.w.)} \\
	&=\sum_{i=1}^n\frac{1}{n}\left(1+\sum_{j=i+1}^n\mathbb{E}[Z_{ij}]\right) \\
	&=\sum_{i=1}^n\frac{1}{n}\left(1+\sum_{j=i+1}^n\frac{1}{m}\right) \\
	&=1+\frac{n}{m}-\frac{1}{nm}\sum_{i=1}^ni\leq 1+\alpha=O(1+\alpha)\\
	&\vdots \\
	&=1+\frac{\alpha}{2}-\frac{\alpha}{2n} \\
	&=\boxed{O(1+\alpha)}
\end{align}
$$
For most hashing tables, $n=O(m)$, which gives expected time $O(1)$

## Uniform Hashing Assumption

For any given key $k$, the prove sequence $\langle h(k,0), h(k,1),\dots,h(k,m-1)\rangle$ is equally likely to assume one of the $m!$ permutations of $\{0,1,\dots,m-1\}$.

## Hash Functions

### Division Method
$$h(k)=k\mod{m}$$
where $m$ is a prime not too close to a power of 2.

### Multiplication Method
$$
\begin{gathered}
0<A<1 \\
h(k)=\lfloor m(kA\mod 1)\rfloor
\end{gathered}$$
$A=\frac{\sqrt{5}-1}{2}$ works well in practice.


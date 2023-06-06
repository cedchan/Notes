
A bloom filter is like a set, but implemented probabilistically so as to save space.

>[!definition]
>Let us have a very large set $\mathcal U$, where $|\mathcal U|=u$. Let $\{x_1, x_2,\dots,x_n\}=S\subset \mathcal U$ such that $u \gg n$. A **bloom filter** supports the operations
>- `Insert(x)`: $S\leftarrow S\cup\{x\}$
>- `Query(x)`: is $x\in S$?
>
>Bloom filters can have false positives, but never false negatives. Deletion is not supported.

We store our $n$ entries in $k>1$ bit tables of size $2n$ each, each with its own [hash](Hashing.md) function $h_i$. We add an element by, for each hash table, setting the corresponding hashed value to 1. We then check membership by iterating through all hash tables. 

```
Insert(x):
	for i = 1 to k:
		B_i[h_i(x)] = 1
```

```
Query(x):
	for i = 1 to k:
		if B_i[h_i(x)] = 0:
			return 0
	return 1
```

## Probabilistic Analysis

The multiple hash tables decrease the probability of false positives (note that there can never be a false negative).

If $x\notin S$, 
$$\begin{align}
\Pr[\text{we output }x\in S]&=\Pr[\forall1\leq i\leq k, \exists y \text{ s.t. } h_i[y]=h_i[x]] \\
&\leq \prod_{i=1}^k\left[\sum_{y\in S}\Pr[h_i(y)=h_i(x)]\right] \\
&=\left(\frac{n}{m}\right)^k \\
&\leq (\frac12)^k
\end{align}$$
We solve for our bound on the error $\epsilon$.
$$\begin{align}
\left(\frac12\right)^k\leq \epsilon\\
k\geq \lg\frac1\epsilon
\end{align}$$
Thus, we use $O\left(\lg\frac1\epsilon\right)$ time and $O\left(n\lg\frac1\epsilon\right)$ space.
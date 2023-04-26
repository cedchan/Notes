>[!definition]
>A **minimum cut** is the smallest set of edges in an undirected graph such that the removal of these edges breaks the graph into two or more connected components.

Applications:
- Network reliability—how many connections can fail before 2 computers can't communicate anymore
- Clustering—cluster web pages (connected with hyperlinks) into related document groupings

## Randomized Approach

**Karger's algorithm** is a simple randomized approach that uses an operation called **edge contraction**, which randomly selects two vertices, combines them into a single vertex, and remove edges that connect them.

```
Input: An undirected graph G = (V, E)
Output: A set of edges in G that represent the minimum size cut-set in G

Min-Cut(G):
	for i = 1 to n - 2:
		Pick a remaining edge (u, v) in G uniformly at random
		Contract(u, v)

	return the edges between the remaining two vertices as the min-cut
```

The output of Karger's will always be some cut set of $G$, although it is not necessarily always the min-cut.

## Probabilistic Analysis

>[!theorem]
>The min-cut algorithm outputs a min-cut set with probability of at least $\frac{2}{n(n-1)}$.

*Proof.* Let $k$ be the size of some min-cut set $C$ that partitions $G$ into $S$ and $V\setminus S$. Notice that in each iteration, $C$ only survives—i.e., remains in the contracted graph—if the contracted edge is not a part of $C$. Thus, the min-cut algorithm is correct if it never chooses an edge in $C$.

We define the following:
- $E_i$: The event that the edge contracted in iteration $i$ is not in $C$
- $F_i=\bigcap_{j=1}^iE_j$: the event that no edge of $C$ was contracted within the first $i$ iterations

We thus want to find $\Pr[F_{n-2}]$ (the probability that we have not gotten an edge in $C$ when there are only 2 vertices left).

First we find $\Pr[E_1]=\Pr[F_1]$. The min-cut set has $k$ edges, so every vertex must have at least degree $k$. By Handshaking Lemma, the graph must have at least $\frac{nk}2$ edges. Thus at random, 
$$\Pr[E_1]=\Pr[F_1]\geq1-\frac{k}{\frac{nk}2}=1-\frac2n$$
Now we have $n-1$ nodes, but still a min-cut set of size $k$, and thus at least $\frac{k(n-1)}2$ edges. This gives
$$\Pr[E_2\mid F_1]\geq1-\frac{k}{\frac{k(n-1)}2}=1-\frac2{n-1}$$
Generalizing, we have
$$\Pr[E_i\mid F_{i-1}]\geq1-\frac{k}{\frac{k(n-i+1)}{2}}=1-\frac2{n-i+1}$$
Then, we can calculate our lower bound
$$\begin{align}
\Pr[F_{n-2}]&=\Pr[E_{n-2}\cup F_{n-3}]=\Pr[E_{n-2}\mid F_{n-3}]\cdot\Pr[F_{n-3}] \\
&=\Pr[E_{n-2}\mid F_{n-3}]\cdot\Pr[E_{n-3}\mid F_{n-4}]\cdot\, \dots\, \cdot\Pr[E_2\mid F_1]\cdot\Pr[F_1]\\
&\geq\prod_{i=1}^{n-2}\left(1-\frac{2}{n-i+1}\right)=\prod_{i=1}^{n-2}\frac{n-i-1}{n-i+1} \\
&=\frac{n-2}{n}\cdot\frac{n-3}{n-1}\cdot\frac{n-4}{n-2}\cdot\,\dots\,\cdot\frac35\cdot\frac24\cdot\frac13 \\
&=\frac2{n(n-1)}
\end{align}$$

### Reducing Error

To reduce the error probability, we can assume that min-cut is independently run $n(n-1)\ln n$ times, and the min-cut size across all runs is outputted. The following theorem demonstrates why.

>[!theorem]
>The probability of an incorrect output over $n(n-1)\ln n$ calls is at most $\frac1{n^2}$.

The probability of a non-optimal output is bounded by 
$$
\left(1-\frac2{n(n-1)}\right)^{n(n-1)\ln n}\leq e^{-2\ln n}=\frac1{n^2}\qquad\qquad\text{(from $1-x\leq e^{-x}$)}
$$

Thus, Karger's algorithm belongs to a class of algorithms known as Monte Carlo algorithms.

>[!definition]
>A **Monte Carlo algorithm** is a finite randomized algorithm that may produce an incorrect output within a certain probability. By repeatedly sampling executions of these algorithms sufficiently, the probability of an incorrect solution becomes almost negligible. 


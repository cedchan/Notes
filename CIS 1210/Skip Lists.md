>[!definition]
>A **skip list** is a randomized data structure of a similar form to a sorted linked list, but with the desirable properties of balanced binary search trees. It supports `Insert`, `Delete`, and `Search`.

The general idea of skip list is that it is a sorted linked list, but with multiple levels, where each level is a (hopefully) evenly distributed subset of the previous level. 

Consider a skip list of 2 levels, $L_1$ (bottom) and $L_2$. When we conduct a search, we go through $L_2$ first, then search the "skipped" elements in $L_1$ after we find the right bucket of $L_2$ (that is, the two elements of $L_2$ where our search item is in between). If we assume even distribution, the number of elements in each bucket will be $\frac{|L_1|}{|L_2|}$. This gives runtime $$|L_2|+\frac{|L_1|}{|L_2|}=|L+2|+\frac{n}{|L_2|}$$
Similarly for the case of 3 levels, we have runtime $$|L_3|+\frac{|L_2|}{|L_3|}+\frac{|L_1|}{|L_2|}=|L_3|+\frac{|L_2|}{|L_3|}+\frac{n}{L_2|} $$
This is minimized when every term is equal. Solving for 
$$|L_3|=\frac{|L_2|}{|L_3|}=\frac{n}{|L_2|}$$
gives $|L_3|=\sqrt[3]{n}$ for a search time of $3\sqrt[3]n$. Generalizing to $k$ levels, we get search time $k\sqrt[k]n$. Then, setting $k=\lg n$, we have $$\lg n(n^\frac1{\lg n})=\lg(2^{\lg n})^\frac1{\lg n}=2\lg n$$
which means we can use BST time for operations like `Search`. 

Unfortunately, insertion and deletion could mess up this order by removing the even distribution assumption, but we only need it to be approximately balanced to get fast search time. 

For skip lists, balancing is done by randomization. Every time an element is added to $L_i$, we toss a fair coin to decide whether it should also be added to $L_{i+1}$. Thus in expectation, half the elements should be in $L_{i+1}$. 

## Implementation

```
Search(x):
	v_l = element with key -INFINITY in L_l
	for i = l down to 2:
		Follow the down-link v_i to v_i-1
		Follow the right-links from v_i-1 until the key of an element is larger than x
		v_i-1 = largest element L_i-1 that is at most x
	return v_1
```

```
Insert(x):
	if Search(x) == x:
		return
	(v_l, v_l-1, ... , v_1) = elements in L_l, L_l-1, ... , L_1 with key values at most x
	Flip a fair coin until we get tails. Let f be the number of flips
	for i = 1 to min(l, f):
		Insert x in L_i
	if f > l:
		Create lists L_l+1, L_l+2, ... , L_f
		Add elements {-INFINITY, x} to L_l, L_l+1, ... , L_f
		Create L_f+1 containing -INFINITY
```

```
Delete(x):
	if Search(x) != x:
		return
	(v_l, v_l-1, ... , v_1) = elements in L_l, L_l-1, ... , L_1 with key values at most x
	for i = 1 to l:
		if v_i == x:
			Delete x in L_i
	while l >= 2 && L_l-1 contains only the element -INIFINITY:
		l = l - 1
```

## Analysis

Let an event happen with high probability (w.h.p.) if it occurs with a probability of at least $1-\frac1{n_c}$, for some constant $c\geq 1$.

We define the following:
- $x_1, x_2, \dots, x_n$: the elements added to the skip list
- $H_i$: the number of lists (levels) that $x_i$ belongs to. Since $H_i$ is a geometric random variable (until the first successful head flip) with parameter $\frac12$. Thus, ${\bf E}[H_i]=2$. 
- $H={\rm max}\{H_1, H_2, \dots, H_n\}$

>[!theorem]
>The space requirement for a skip list with $n$ elements is $O(n)$ in expectation.

*Proof.* Let $S$ be the random variable denoting the amount of space used by a skip list of $n$ elements. Including the sentinal keys ($-\infty$), we have 
$$\begin{align}
S&=O\left(\sum_{i=1}^nH_i\right) \\
{\bf E}[S]&=O\left(\sum_{i=1}^n{\bf E}[H_i]\right) & \text{(LOE)}\\
&=O\left(\sum_{i=1}^n2\right)\\
&=O(n)
\end{align}$$

>[!lemma] Lemma 1
>$\Pr[H\geq h]\leq \frac{n}{2^{h-1}}$

*Proof.*
$$\begin{align}
\Pr[H\geq h]&=\Pr\left[\bigcup_{i=1}^nH_i\geq h\right] \\
&\leq \sum_{i=1}^n\Pr[H_i\geq h] & \text{(using union bound)} \\
&=\sum_{i=1}^n\frac{1}{2^{h-1}} &\left(\Pr\left[{\rm failure}=\frac{1}{2}\right],\text{ $h-1$ times}\right) \\
&=\frac{n}{2^{h-1}}
\end{align}$$

>[!lemma] Lemma 2
>The expected number of levels in a skip list with $n$ elements is at most $\lceil \lg n \rceil + 3$. 

*Proof.* The number of levels is $H+1$ (the $1$ is for the level with only $-\infty$). Since $H$ is a non-negative random variable, we know that 
$$\begin{align}
{\bf E}[H]&=\sum_{h=1}^n\Pr[H\geq h] \\
&=\sum_{h=1}^{\lceil\lg n\rceil}\Pr[H\geq h]+\sum_{h\geq\lceil\lg n\rceil+1}\Pr[H\geq h] \\
&\leq\sum_{h=1}^{\lceil\lg n\rceil}1+\sum_{h\geq\lceil\lg n\rceil+1}\frac{n}{2^{h-1}} \\
&\leq\lceil\lg n\rceil+\sum_{h\geq\lceil\lg n\rceil+1}\frac{n}{2^{h-1}}  \\
&=\lceil \lg n\rceil+\frac{n}{2^{\lg n}}\sum_{i=0}^\infty \frac1{2^i} \\
&=\lceil\lg n\rceil+2
\end{align}$$
Thus the expected height is this at most this plus 1: $\lceil \lg n\rceil+3$.

>[!lemma] Lemma 3
>With high probability, a skip list with $n$ elements has $O(\lg n)$ levels.

*Proof.* From Lemma 1, we have 
$$\begin{align}
\Pr[H\geq2\lg n+1]&\leq\frac{n}{2^{2\lg n+1-1}} \\
&=\frac{1}{n}
\end{align}$$

>[!lemma] Lemma 4
>For any $0<r\leq n$, $$\sum_{i=0}^r\binom{n}{i}\leq\left(\frac{ne}{r}\right)^r$$

*Proof.* In a more convenient form,
$$\begin{align}
\sum_{i=0}^r\binom{n}{i}&=\left(\frac{n}{r}\right)^r\sum_{i=0}^r\binom{n}{i}\left(\frac{r}{n}\right)^r \\
&\leq \left(\frac{n}{r}\right)^r\sum_{i=0}^r\binom{n}{i}\left(\frac{r}{n}\right)^i \\
&\leq \left(\frac{n}{r}\right)^r\sum_{i=0}^n\binom{n}{i}\left(\frac{r}{n}\right)^i \\
&=\left(\frac{n}{r}\right)^r\left(1+\frac{r}{n}\right)^n & \text{(binomial theorem)} \\
&\leq\left(\frac{n}{r}\right)^re^{\frac{r}{n}n}& (\forall x, 1+x\leq e^x) \\
&=\left(\frac{ne}{r}\right)^r
\end{align}$$

>[!theorem]
>With high probability, in a skip list of $n$ elements, every search takes $O(\lg n)$ time.

*Proof.* We want to bound the total number of steps (right and down steps). We will start from the desired element $v_1$ and trace the search path backwards (going left and up).

We want to show that the total number of moves is at most $20\lg n$ with high probability.

Consider these events:
- $E$: total number of coin flips is $20 \lg n$ and our search hasn't ended
- $U$: total number of up moves is greater than $2\lg n$

We want to upper bound $\Pr[E]$. By Lemma 3, $\Pr[U]=\Pr[H>2\lg n]\leq \frac1{n}$.
$$\begin{align}
\Pr[E]&=\Pr[E\cap U]+\Pr[E\cap\overline{U}] \\
&\leq\Pr[U]+\Pr[E]\Pr[\overline{U}\mid E] \\
&\leq\frac1n+\Pr[\overline U \mid E]
\end{align}$$
Let $X$ be the random variable denoting the number of heads.
$$\begin{align}
\Pr[\overline U\mid E]&=\sum_{i=0}^{2\lg n}\Pr[X=i] \\
&=
\end{align}$$
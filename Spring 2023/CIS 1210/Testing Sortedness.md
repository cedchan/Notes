
**Problem:** Given an array $A$ of $n$ elements, we wish to determine if $A$ is sorted in non-decreasing order, i.e., $A[1]\leq A[2]\leq \dots\leq A[n]$.

This is easy to verify $O(n)$ time by sweeping through the array, but our goal now is to solve the problem in $o(n)$, *sublinear* time. This isn't possible, but we can get an approximate answer in sublinear time.

>[!definition]
>An array $A$ is $\varepsilon$-far if changing $\geq\varepsilon\cdot n$ elements in $A$ results in a sorted array, where $\varepsilon\in(0, 1)$.

>**Example.** Given an array $[13, 28, 3, 46, 79, 91, 14, 66, 100]$, the array is $\frac13$-far because we can change a third of the elements (at positions 3, 7, and 8) to get a sorted array.

We want to 
1. Output yes with a probability of $\geq\frac23$ if $A$ is sorted
2. Output no with a probability of $\geq\frac23$ if $A$ is $\varepsilon$-far from being sorted

## Boolean Array

We start with a simple "baby" case of a boolean array (i.e., with only 0s and 1s). Being sorted simply means that all the 0s appear before all the 1s. 

Suppose $A$ is $\varepsilon$-far. Then,
- $A$ must have $\geq\varepsilon\cdot n$ 0s
- $A$ must have $\geq\varepsilon\cdot n$ 1s

If not, then we could change $<\varepsilon\cdot n$ elements to get a sorted array, meaning $A$ is not $\varepsilon$-far.

We then define 2 sets:
- $Left_1$: set of the smallest $\varepsilon\cdot\frac{n}2$ indicies in $A$ that contain a 1
- $Right_0$: set of the largest $\varepsilon\cdot\frac{n}2$ indices in $A$ that contain a 0

>**Example.** Given $[0, 1, 1, 1, 0, 1, 0, 0, 1, 1]$ and $\varepsilon=\frac12$, we have $\varepsilon\cdot\frac{n}2=2$, so $Left_1=\{2, 3\}, Right_0=\{7, 8\}$.

>[!lemma] Lemma 1
>Let $i$ be the largest index in $Left_1$ and $j$ be the smallest index in $Right_0$. Then $i<j$.

*Proof.* AFC that $i>j$. Then there are $\varepsilon\cdot\frac{n}2$ 1s before $i$ and $<\varepsilon\cdot\frac{n}2$ 0s after $i$. We can thus change the 1s before $i$ to 0 and 0s after $i$ to 1 to sort the array in $<\varepsilon\cdot n$ changes, contradicting that $A$ is $\varepsilon$-far. 

### Algorithm

1. Sample $t$ indices $i_1, i_2, \dots, i_t$.
2. Query $A[i_1], A[i_2], \dots, A[i_t]$
3. If any pair of numbers is inverted ($i<j$ but $A[i]>A[j]$) then output no, otherwise yes.

>[!lemma] Lemma 2
>If $A$ is sorted then the probability that our algorithm outputs an incorrect answer is 0.

*Proof.* There can be no inversions in a sorted array.

>[!lemma] Lemma 3
>If $A$ is $\varepsilon$-far from being sorted, and $t\geq\frac2\varepsilon\ln\frac2\delta$, then $\Pr[{\rm incorrect}]\leq\delta$.

*Proof.* Consider these events:
- $E_L$: The event that we choose one sample from $Left_1$
- $E_R$: The event that we choose one sample from $Right_0$

If both $E_L$ and $E_R$ happen, by Lemma 1 we must find an inversion and output the correct answer. Thus we have
$$\begin{align}
\Pr[{\rm incorrect}]&\leq\Pr[\overline E_L\cup\overline E_R] \\
&\leq\Pr[\overline E_L]+\Pr[\overline E_R] \\
&=\left(1-\frac{\frac{\varepsilon\cdot n}{2}}{n}\right)^t+\left(1-\frac{\frac{\varepsilon\cdot n}2}n\right)^t \\
&\leq 2e^{-\frac{\varepsilon\cdot t}2} & (1+x\leq e^x)
\end{align}$$
Then, if we are allowed to be wrong with a probability of at most $\delta$, we require
$$\begin{align}
2e^{\frac{\varepsilon\cdot t}2}&\leq\delta \\
e^{\frac{\varepsilon\cdot t}2}&\geq \frac2\delta\\
\frac{\varepsilon\cdot t}2&\geq\ln\frac2\delta \\
t&\geq\frac2\varepsilon\ln\frac2\delta
\end{align}$$
Hence, if $t\geq\frac2\varepsilon\ln\frac2\delta$, then $\Pr[{\rm incorrect}]\leq\delta$.

### Runtime

The first two steps require $O(t)$ time. The last step can also be implemented in $O(t)$ time by computing the maximum index $i$ among sampled indices which are 0 and the minimum index $j$ among sampled 1s, and determining if $i>j$. Thus our runtime is $O(t)=O\left(\frac2\varepsilon\ln\frac2\delta\right)$.

**Note.** For constant $\varepsilon,\delta>0$ independent of $n$, the runtime is constant and not at all affected by the size of the input array. 

## General Case

For a general array, the simple algorithm doesn't work. Consider a $\frac23$-far array. To get the correct answer, it must sample at least two indices from the same block of size three. For this to happen, the size of the sampled set becomes $\Theta(\sqrt n)$

>[!danger] TODO
>Figure out above. (birthday paradox?)

>[!definition]
>A binary search of a number $a$ on array $A$ (sorted or unsorted) is termed **consistent** if it returns $a$.

That is, a binary search is consistent if it returns the desired value.

>[!lemma] Lemma 4
>Suppose binary search on $A[i]$ and $A[j]$ is consistent. If $i<j$, then $A[i]<A[j]$. 

*Proof.* Consider the first pivot $p$ between $i$ and $j$. Since the search on $A[i]$ is consistent, we have $A[i]\leq A[p]$. Similarly, since the search on $A[j]$ is consistent, $A[j]\geq A[p]$. Since we assume distinct elements, only one of the above relations can be equal. This gives $A[i]<A[j]$. 

### Binary Search Tester
1. Sample $i\in\{1, 2, \dots, n\}$
2. Do a binary search on $A[i]$
3. Output yes if the binary search is consistent and no otherwise

>[!lemma] Lemma 5
>The binary search tester outputs the wrong answer, no, with probability 0 whenever $A$ is sorted. It outputs the wrong answer, yes, with probability at most $1-\varepsilon$ whenever $A$ is $\varepsilon$-far. 

*Proof.* When $A$ is sorted, the algorithm clearly always outputs yes. 

Now suppose $A$ is $\varepsilon$-far. We define a set $C(A)=\{i_1,i_2,\cdot,i_t\}$ of all indices on which the binary search is inconsistent. Observe that $t\leq(1-\varepsilon)n$, as we can change $\varepsilon\cdot n$ of the elements and the $(1-\varepsilon)\cdot n$ unchanged elements would now be consistent.

Our algorithm outputs the wrong answer if we pick an element in $C(A)$, which we do with probability
$$\Pr[{\rm incorrect}]\leq\frac{(1-\varepsilon)n}n=1-\varepsilon$$

### Final Algorithm

We decrease the probability of an incorrect answer by repeatedly running the algorithm. 

1. Run binary search tester $k$ times independently
2. Output yes if all runs output yes and output no otherwise

#### Analysis

The correct answer case is trivial.

In the case where $A$ is $\varepsilon$-far, since we need every independent run to be correct,
$$\begin{align}
\Pr[{\rm incorrect}]&\leq(1-\varepsilon)^k \\
&\leq e^{-\varepsilon k} & (1+x\leq e^x)
\end{align}$$

Bounding this probability by $\delta$, we get
$$\begin{align}
e^{-\varepsilon k}&\leq \delta \\
e^{\varepsilon k}&\geq \frac1\delta\\
\varepsilon k&\geq \ln\frac1\delta \\
k&\geq\frac1\varepsilon\ln\frac1\delta
\end{align}$$

##### Runtime

Since our search runs $k$ times on array size $n$, our overall runtime is $O(k\lg n)$. 

Thus, we output the correct answer with probability $1-\delta$ in $O(k\lg n)$ time. 
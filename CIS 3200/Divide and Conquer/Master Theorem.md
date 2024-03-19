---
tags:
  - divide-and-conquer
---
Divide-and-conquer often have runtimes of the form
$$T(n)\leq aT\left(\frac nb\right)+f(n)$$
That is, we divide an input $n$ into $a$ subproblems of size $\frac nb$, and use $f(n)$ time to put those subproblems together.

The master theorem gives a quick way to evaluate such recurrence relations

>[!theorem] Master Theorem
>For a recurrence relation of the form $$T(n)\leq aT\left(\frac nb\right)+O(n^d)$$
>1. **Case 1:** $f(n)=n^d\ll n^{\log_ba}\iff d<\log_ba$. "Cost to recombine cheap"
>	$$T(n)=O(n^{\log_ba})$$
>2. **Case 2:** $f(n)=n^d\gg n^{\log_ba}\iff d>\log_ba$. "Cost to recombine expensive"
>	$$T(n)=O(n^d)$$
>3. **Case 3:** $d=\log_ba$. "Just right"
>	$$T(n)=O(n^d\log_bn)$$
>	
>That is,
>$$T(n)=\begin{cases}
O(n^{\log_ba}) & b^d<a \\
O(n^d) & b^d>a \\
O(n^d\log_bn) & b^d=a
\end{cases}$$

## Proof

To motivate the theorem, think about the recursive tree that is used in solving the problem. An input of size $n$ is split into $a$ groups of size $\frac nb$, which are each split into $a$ groups of size $\frac n{b^2}$, etc. At the first level, we do $f(n)$ work to combine, then $f\left(\frac nb\right)$, then $f\left(\frac n{b^2}\right)$, etc. 

It follows that at a level $i$, the cost of recursion is $a^if\left(\frac{n}{b}\right)$. How many levels are there? We have
$$\begin{align}
\frac{n}{b^h}&=1 & \text{(or generally a constant $c$)}\\
h&=\log_b n
\end{align}$$
Thus our total cost is given by
$$\begin{align}
T(n)&\leq \sum_{i=0}^ha_if(n)^d \\
&= \sum_{i=0}^ha_i\left(\frac n{b^i}\right)^d \\
&=n^d\sum_{i=0}^h\left(\frac a{b^d}\right)^i \\
\end{align}$$
Now the cases come into play. 

**Case 1.** $a>b^d$, the "recombine cost low" case
$$\begin{align}
T(n)&\leq n^d\sum_{i=0}^h\left(\frac a{b^d}\right)^i \\
&\leq O\left(n^d\left(\frac{a}{b^d}\right)^h\right) \\
&=O\left(n^d\left(\frac a{b^d}\right)^{\log_bn}\right) \\
&=O\left(\frac{n^da^{\log_bn}}{b^{d\log_bn}}\right) \\
&=O\left(\frac{n^dn^{\log_ba}}{b^{d\log_bb}}\right) \\
&=O(n^{\log_ba})
\end{align}$$

**Case 2.** $a< b^d$, the "recombine cost high" case
$$\begin{align}
T(n)&\approx n^d\sum_{i=0}^h(0.999\dots)^i \\
&\leq n^d\sum_{i=0}^\infty(0.999\dots)^i \\
&=O(n^d)
\end{align}$$

**Case 3.** $a=b^d$, the "just right" case
$$\begin{align}
T(n)&=n^d\sum_{i=0}^h1^i\\
&=n^d(h+1)\\
&=O(n^d\log_bn)
\end{align}$$

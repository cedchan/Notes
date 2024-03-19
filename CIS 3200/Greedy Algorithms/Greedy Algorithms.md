---
tags:
  - greedy-algorithms
---
With greedy algorithms, the algorithmic description is typically straightforward. It's the analysis that proves more difficult—this is, in some ways, the opposite of divide-and-conquer or [dynamic programming](Dynamic%20Programming.md) algorithms.

Like in dynamic programming, greedy algorithms as a top-level question. But instead of exploring all possibilities, greedy algorithms seek to directly answer the top-level question.

When formulating a greedy algorithm, it's helpful to first try out several examples and try to break your algorithm, since besides vague intuition, the only way to truly check your algorithm is to rigorously prove it.

## Exchange Argument

To prove the correctness of greedy algorithms, we typically use the **exchange argument**. We do this by proving a particular lemma:

>[!lemma]
>Let $G$ be the solution produced by you with ${\rm A\small LG}$ and let ${\rm O\small PT}$ be the true optimal solution.
>$$\begin{align}
>\exists k\geq 0\text{ s.t. } G &\text{ agrees with O{\small PT} on $k$ decisions}\implies \\
>&\exists {\rm O\small PT}' \text{ that is optimal but agrees on $k+1$ decisions}
\end{align}$$




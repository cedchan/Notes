---
tags:
  - greedy-algorithms
---
>[!problem]
>**Input:** Start times $s_1, \dots, s_n$ and end times $e_1, \dots, e_n$.
>
>**Output:** Maximum number of performers such that they don't overlap.

Note that this is like the [weighted activity selection](Weighted%20Activity%20Selection.md) problem, except we are just trying to maximize the number of performers and assume they all pay the same amount.

**Algorithm:** 
1. Sort according to finish times
2. Pick first, cancel intersections
3. Recurse on remainder

## Analysis

>[!lemma]
>From the [exchange argument](Greedy%20Algorithms.md#Exchange%20Argument), assume by IH, if $\exists {\rm O\small PT}$ that agrees with $k$ performers in $G$, then there exists $\widetilde{\rm O\small PT}$ such that 
>1. It's feasible
>2. $|\widetilde{\rm O\small PT}|=|{\rm O\small PT}|$
>3. It agrees with the greedy algorithm on $k+1$ performers.

**Proof.** Consider the interval $(s_{k+1},e_{k+1})$, which $G$ chooses but ${\rm O\small PT}$ doesn't, as well as the performer $t^*$ that ${\rm O\small PT}$ chooses but $G$ does not. Since $G$ chose intervals in sorted order, it must be true that there is no other interval starting or ending in $(e_k, e_{k+1})$ (if there were, then $G$ would've chosen that interval). Thus, no interval in ${\rm O\small PT}$ overlaps with the range $(e_k, e_k+1)$, so we can safely add $t_{k+1}$ to ${\rm O\small PT}$ and remove $t^*$. That is,
$$\widetilde{\rm O\small PT}=({\rm O\small PT}\setminus \{t^*\})\cup\{t_{k+1}\}$$
From above, we know that $\widetilde{\rm O\small PT}$ is feasible. Further, we can trivially see that $|\widetilde{\rm O\small PT}|=|{\rm O\small PT}|$, and that it is closer to $G$.
$$\tag*{$\square$}$$

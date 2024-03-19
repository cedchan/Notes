---
tags:
  - greedy-algorithms
---
>[!problem]
>**Input:** Sequence of tasks $t_1, \dots, t_n\in\mathbb R_{\geq0}$; time budget $T$.
>
>**Output:** Maximize number of tasks completed within time $T$.

Written as an optimization problem:
- **Solution Space:** All subsets of tasks.
- **Objective function:** $S=\text{set of tasks chosen}$. $f(S)=|S|$.
- **Constraint:** $\sum_{i\in S}t_i\leq T$

**Algorithm:** Pick the shortest times first until you hit your budget. (Implication: Sort first, then pick.)

## Analysis

We use the [exchange argument](Greedy%20Algorithms.md#Exchange%20Argument) to prove correctness. 

Consider the sorted sequence of tasks $$\begin{gather}
t_1\leq t_2\leq \dots\leq t_m\leq t_{m+1}\le\dots\leq t_n\\
G=T-t_{m+1}<\sum_{\ell=1}^mt_\ell\leq T\\
{\rm O\small PT}=[t_1,\dots, t_k]
\end{gather}$$
>[!lemma]
>Assume for induction that ${\rm O\small PT}$ contains $t_1,\dots,t_k$.
>
>$\implies \widetilde{\rm O\small PT}$ such that
>1. Feasible
>2. $|\widetilde{\rm O\small PT}|=|{\rm O\small PT}|$
>3. $\widetilde{\rm O\small PT}$ contains $t_1, \dots, t_{k+1}$.

**Proof.**

*Case 1:* ${\rm O\small PT}$ contains $t_{k+1}$. Set $\widetilde{\rm O\small PT}={\rm O\small PT}$. 
$$\tag*{$\square$}$$
*Case 2:* ${\rm O\small PT}$ doesn't contain $t_{k+1}$ but greedy does. This implies that ${\rm O\small PT}$ chose some $t^*$ after $t_{k+1}$. 
$$\widetilde{\rm O\small PT}=({\rm O\small PT}\setminus\{t^*\})\cup\{t_{k+1}\}$$
$t_{k+1}$ is feasible because it appears before $t^*$ in our sorted list, meaning that it's no greater than $t^*$, so removing $t^*$ and adding $t_{k+1}$ won't increase the cost of $\widetilde{\rm O\small PT}$. 
$$\tag*{$\square$}$$




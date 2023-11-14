## Big-O Notation

>[!definition]
>Given two functions $f$ and $g$ over natural numbers, $g$ is said to be an **asymptotic upper bound** of $f$, $f(n)=O(g(n))$, if there exist constants $c$ and $n_0$ such that for all $n\geq n_0$, $f(n)\leq cg(n)$. 
>
>In set notation, $$O(g(n))=\{f\mid \exists c, n_0 \in \mathbb R\text{ s.t. } \forall n\geq n_0, f(n)\leq cg(n)\}$$

That is, intuitively, $f$ is bounded by $g$ for larges values of $n$. It is the worst case.

>**Example.** TM for Palindromes.
>
>Briefly, the TM for palindromes marked symbols on the left end and the corresponding symbols on the right side, going one at a time, back and forth, checking that the two ends are equivalent.
>
>The question is, how many TM transitions are executed as a function of the length of the input $n$. 
>
>In this case, we go back and forth across the tape at most $n$ times, where each traversal takes $n$ steps at most. This gives a time complexity of $O(n^2)$.
>
>In an ordinary program, we would be able to check $A[i]=A[j]$ in constant time, rather than having to move the head from cell $i$ to $j$ (taking $n$ steps). This means that the true time complexity of the problem should be $O(n)$ (and in fact, it is $\Theta(n)$). 

## The Class P

>[!definition]
>A language $A$ belongs to the **class P** if there exists a single-tape deterministic halting TM $M$ such that
>1. $M$ decides $A$ (that is, $L(M)=A$)
>2. Time complexity of $M$ is $O(n^k)$, for some constant $k$

In other words, P is the class of problems that are solvable in polynomial time.

### Choice of Machine Model

Recall the **Church-Turing thesis**:

>[!theorem] Thesis
>If a program on a modern computer can solve a problem, so can a TM.

There exists a similar thesis for the class P:

>[!theorem] Thesis
>
>If a problem can be solved by a deterministic program on a modern computer with polynomial time complexity, then it belongs to P (i.e., it can be solved by a standard TM in polynomial time).

We can show this by demonstrating that for a given deterministic model, converting it into a TM will only increase complexity by a polynomial factor.

### Two-Tape TM

One of the first examples we used previously of a more general model was the [two-tape TM](Generalized%20Turing%20Machines.md#Two-Tape%20Turing%20Machines). Recall that the transformation from a two-tape TM $M$ to a standard TM $M'$ involved combining the two tapes into a single tape, marking the beginning of the "second" subtape and the head of both tapes. Then in each step of the two-tape TM $M$, the standard TM $M'$ would more the head to the markers sequentially and operate accordingly.

Suppose now that $M$ has complexity of $O(f(n))$. Since the additional overhead we add to $M'$ is moving between the two heads, we increase the complexity of $M$ by at most a factor of $O(n)$. This results in an overall complexity of $O(n\cdot f(n))$, and we know the product of polynomials remains a polynomial, so $n\cdot f(n)$ is polynomial. 

## Examples

### Reachability in Directed Graphs

**Problem:** Given a directed graph $G$ and vertices $s$ and $t$, check if there is a path from $s$ to $t$ in $G$.
$${\rm PATH}=\{\langle G,s,t\rangle\mid G\text{ is a directed graph and there is a path }s \rightsquigarrow t\}$$
$$\begin{align}
\hline
&{\rm Reach}=\{s\} \\
&{\rm Unexplored}=\{s\} \\
&\text{{\bf while} Unexplored $\neq\emptyset$}\\
&\quad \text{Remove a vertex $v$ from Unexplored} \\
&\quad\quad \text{{\bf foreach} edge $(v, u)$} \\
&\quad\quad\quad \text{{\bf if }$u\notin{\rm Reach}$ {\bf then} } \\
&\quad\quad\quad\quad{\rm Reach}={\rm Reach}\cap\{u\}\\
&\quad\quad\quad\quad{\rm Unexplored}={\rm Unexplored}\cap\{u\}\\
&\text{{\bf if } $t\in{\rm Reach}$ {\bf then} ACCEPT {\bf else} REJECT} \\
\hline
\end{align}$$

This is solvable in polynomial time since each edge is considered at most once.

### Clique Problem

$${\rm CLIQUE}=\{\langle G, k\rangle\mid \text{$G$ is an undirected graph and contais a clique of size $k$}\}$$
$$\begin{align}
\hline
&\text{{\bf for all} subsets $U$ of $V$ {\bf do}}\\
&\quad\text{{\bf if} $|U|=k$ {\bf then}}\\
&\quad\quad\text{Check if $G$ has an edge between every $u, v\in U$} \\
&\quad\quad\text{{\bf if} so {\bf then} stop and ACCEPT} \\
&{\rm REJECT} \\
\hline
\end{align}$$

This gives time complexity $O(n^22^n)$, so we can't conclude that the problem is in P. It doesn't, however, prove that it isn't in P.

### Equivalence of DFAs

$${\rm EQ_{DFA}}=\{\langle A,B\rangle\mid\text{$A$ and $B$ are DFAs and $L(A)=L(B)$}\}$$

1. Construct $A^\complement$ that accepts $L(A)^\complement$. Construct $A'$ that accepts the intersection $L(A^\complement)\cap L(B)$
2. If $L(A')$ is not empty, stop and reject.
3. Construct $B^\complement$ that accepts $L(B)^\complement$. Construct $B'$ that accepts the intersection $L(B^\complement)\cap L(A)$
4. If $L(B')$ is not empty, stop and reject
5. Accept

This is solvable in polynomial time. 

### Equivalence of NFAs

$${\rm EQ_{NFA}}=\{\langle A,B\rangle\mid\text{$A$ and $B$ are NFAs and $L(A)=L(B)$}\}$$

One approach is to use subset construction to convert $A, B$ into DFAs, then run the previous algorithm. Subset construction takes exponential time, so this algorithm doesn't show that this problem is in P.

### Membership Test for NFAs

$${\rm A_{NFA}}=\{\langle M, w\rangle\mid\text{$M$ is an NFA and $M$ accepts $w$}\}$$
1. Construct DFA $M'$ using subset construction that accepts $L(M)$
2. Check if $M'$ accepts $w$ by executing it step by step.

**Complexity:** $M'$ has $2^n$ states, and step 2 is polynomial. Thus the overall complexity is exponential.

#### A Polynomial Algorithm

Instead of constructing the entire DFA, maintain a set of possible states.

$$\begin{align}
\hline
&S\gets\{q_0\} \\
&\text{{\bf for all} $\sigma\in w$ {\bf do}} \\
&\quad S\gets\{q'\mid \exists q\in S\text{ s.t. }q'\in\Delta(q,\sigma)\}\\
&\text{Check if $S$ contains a final state}\\
\hline
\end{align}$$
The time complexity of this algorithm is $O(n|w|)$, where $n$ is the number of states.

## Closure Properties of P

### Closure Under Intersection

>[!theorem]
>The class P is closed under intersection.

**Proof.** Suppose $A_1, A_2$ are languages in P. We want to show that $A_1\cap A_2$ is also in P.

Because both are in P, there must be deciders $M_1, M_2$ with complexities $O(n^{k_1}), O(n^{k_2})$ that solve $A_1, A_2$, respectively.

Thus, the decider for $A_1\cap A_2$ can simply be constructed by running $M_1$, then running $M_2$, giving a terminating program with overall complexity $O(n^{k_1}+n^{k_2})$, which is polynomial.

Union and complement similarly follow.
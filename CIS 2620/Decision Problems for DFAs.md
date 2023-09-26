>[!definition]
>**Decision problems** for DFAs take in a [DFA](Deterministic%20Finite%20Automata%20(DFA).md) and analyze its behavior. Such problems are typically solvable when the input is a DFA (or [NFA](Nondeterministic%20Finite%20Automata.md) or [regular expression](Regular%20Expressions.md)). 
>
>The algorithm that solves this problem is a general program—that is, not a DFA itself.

>**Example.** 
>- States: $\{\text{A, B, C, D, E, F, G, H, I, J, K, L}\}$
>- $\Sigma=\{0, 1\}$
>- Initial state $A$
>- Accepting states $\{\text{D, J}\}$
>- Transition function:
>
>	| State | A | B | C | D | E | F | G | H | I | J | K | L |
>	|-|-|-|-|-|-|-|-|-|-|-|-|-|
>	| $δ(\_,0)$ | B | G | D | A | B | D | L | H | K | I | B | F |
>	| $δ(\_,1)$ | A | I  | G  | K | E | C | H | C | L | J | A | E |
>	
>Questions to ask:
>- Given $M$, what is $L(M)$?
>- Is $L(M)$ an empty set?
>- Given $M$ and $M'$, are they equivalent (i.e., $L(M)=L(M')$)?

## Membership Problem

**Problem:** Given DFA $M$ and an input string $w$, is $w\in L(M)$?

**Solution:**
$$\begin{align}
\hline
&\textbf{Membership Algorithm}\\
\hline
&\text{Initialize state of $M$ to its initial state} \\
&\text{\textbf{for each} symbol in $w$} \\
&\text{\quad Update the state by applying transition function} \\
&\text{\textbf{if} the state at the end is in $F$} \\
&\text{\quad $w\in L(M)$} \\
&\text{\bf else} \\
&\quad w\notin L(M) \\
\hline
\end{align}$$
**Complexity:** $O(|w|)=O(n)$
## Emptiness Problem

**Problem:** Given a DFA $M$, is $L(M)$ non-empty? Does $M$ accept any string?

**Solution:** We note that this is the same as any graph reachability problem. That is, we compute a set of reachable states.

>[!algorithm]
>$$\begin{align}
\hline
&\textbf{Emptiness Algorithm} \\
\hline
&\text{Reach $\leftarrow$ \{$q_0$\}} \\
&\text{\textbf{repeat}} \\
&\text{\quad\textbf{if} $\exists q\in $ Reach, $\sigma\in\Sigma$ s.t. $q'=\delta(q, \sigma)\notin$ Reach} \\
&\text{\quad\quad Reach $\leftarrow$ Reach $\cup$ \{$q'$\}} \\
&\text{\textbf{until} Reach doesn't change} \\
&\text{\textbf{if} Reach $\cap$ $F\neq\emptyset$} \\
&\text{\quad $L(M)$ is non-empty} \\
&\text{\textbf{else}} \\
&\text{\quad $L(M)$ is empty} \\
\hline
\end{align}$$

**Complexity:** $O(n)$ (runs once for each state)
## Emptiness of Intersection

**Problem:** Given DFAs $M, M'$, is there a string that they both accept? Is the intersection of $L(M), L(M')$ non-empty?

**Solution:**
1. Construct the product machine $N$ that accepts the intersection of the two languages. (Recall: state of $N$ = (state of $M$, state of $M'$).)
2. [Check](Decision%20Problems%20for%20DFAs.md#Emptiness%20Problem) if $L(N)$ is non-empty

**Complexity:** $N$ has $|M|\cdot|M'|=O(n^2)$ states, so we run in $O(|N|)=O(n^2)$ time.
## Equivalence Problem

**Problem:** Given DFAs $M, M'$, are they equivalent? That is, is it the case that $L(M)=L(M')$?

**Solution:**
>[!error]
>He didn't say lol

## Minimization Problem

**Problem:** Given a DFA $M$, find an equivalent DFA with the least number of states.

**Solution:** 

>[!definition]
>Consider DFA $M=(Q, \Sigma, q_0, F, \delta)$. Two states $q, q'$ are **distinguishable** if there exists a string $w$ such that only one of $\delta^*(q, w), \delta^*(q', w)$ is in $F$. 

**Claim:** Distinguishable states cannot be merged unless they cannot be reached from the initial state.

**Algorithm:**
1. Compute the set of states that are reachable from $q_0$ (e.g., through a [BFS](Graph%20Traversals.md#Breadth-First%20Search%20(BFS)) or [DFS](Graph%20Traversals.md#Depth-First%20Search%20(DFS))) and remove the rest.
2. Compute the set of distinguishable state-pairs (pairs of accepting and non-accepting states). That is, $$D=\{(q, q')\mid q\in F\oplus q\in F\}$$
3. Merge equivalent (indistinguishable) states$$\begin{align}
\hline
&\text{\bf repeat} \\
&\quad D\leftarrow D\cup\{(q, q')\mid \exists\sigma \text{ s.t. } (\delta(q,\sigma), \delta(q', \sigma) \in D\} \\
&\text{\textbf{until} $D$ doesn't change} \\
\hline
\end{align}$$Suppose $δ(q, σ)=p$ and $δ(q’, σ)=p’$. If string $w$ distinguishes states $p$ and $p’$, then the string $σ.w$ takes exactly one of $q$ and $q’$ to a final state, so distinguishes them.

**Correctness:** Only distinguishable pairs are added to $D$. If a pair of states is distinguishable, then it gets added to $D$ (proof in lecture notes).

**Complexity:** The algorithm runs $n$ iterations, with $O(n^2)$ time, although there is a more complicated $O(n)$ solution

### Definition of Minimal DFA

>[!definition]
>The minimal DFA for a given $M$, denotes $\mathrm{Minimal}(M)$ is defined as follows:
>- States: Partitions of $R$ (by notion of distinguishability)
>- Initial state: Partition $P$ containing the original $q_0$
>- Final states: Partition $P$ is final if it contains a final state of $M$
>- Transition function: If $δ(q, σ)=q’ \in M$ and state $q$ is in partition $P$ and state $q’$ is in partition $P’$ then $δ’(P, σ)=P’$ in $\mathrm{Minimal}(M)$

### Properties of Minimal DFA

All states are distinguishable, so this is the smallest number of states that the DFA can have.

All equivalent DFAs will share the same minimal DFA. That is, the minimal DFA is unique. (Of course, there can be different labels, but the DFAs will be structurally equivalent.)

The minimal DFA is **canonical**, meaning that it depends only on the language it accepts.
## Introduction

Consider TM $M$ such that $L(M)=\{w\mid M \text{ halts on } w \text{ in its accepting state}\}$

>[!definition]
>A language $A$ is **recognizable**, or equivalently **recursively enumerable (RE)**, if there exists a TM $M$ such that $L(M)=A$.

This is a weaker notion than [decidability](Turing%20Machines.md#Recursive%20Languages), which requires that $M$ be halting. That is, decidability implies recognizability, but not vice versa.

That is $$\mathrm{regular} \subset \mathrm{decidable} \subset \mathrm{decidable} \subset\mathrm{all}$$

> **Problem:** Given a multi-variable polynomial with integer coefficients ,are there integer values for the variables that make the polynomial 0?
> 
> One plausible strategy is brute force: try all combinations of variables until something works. The question is, if you haven't found a solution, when do you stop trying combinations?
> 
> Let $\mathrm{HILBERT10}=\{p(x_1, x_2, \dots, x_n)\mid\exists c_1, c_2, \dots, c_n\in \mathbb Z \text{ s.t. } p(c_1, c_2, \dots, c_n)=0\}$
> 
> Program $P$ to solve $\mathrm{HILBERT10}$:
> $$\begin{align}
 \hline
 &k\leftarrow0 \\
 &\textbf{repeat} \\
 &\quad\text{{\bf for all} vectors }[c_1, c_2, \dots,c_n] \text{ with $-k\leq c_i\leq k$} \\
 &\quad\quad\text{{\bf for each} i} \\
 &\quad\quad\quad\text{{\bf if} $p(c_1,c_2,\dots,c_n)=0$ {\bf then} STOP and ACCEPT}\\
 &\quad k\leftarrow k+1 \\
 \hline
 \end{align}$$
> **Claim:** If the input polynomial belongs to $\mathrm{HILBERT10}$, then $P$ stops and accepts. Otherwise, we may continue computing forever. 
> 
> Here, the problem is **recognizable** because $L(P)=\mathrm{HILBERT10}$.

## Closure

### Closure Under Union

The idea is that we simultaneously run both machines and stop if either accepts the input. Since TMs can't do parallel computation, we simulate this by alternating between the TMs.
$$\begin{align}
\hline
&\text{Copy $w$ to both tapes}\\
&\textbf{repeat} \\
&\quad\text{Execute one transition of $M_1$ on Tape 1} \\
&\quad\text{{\bf if} $M_1$ accepts {\bf then} ACCEPT} \\
&\quad\text{Execute one transition of $M_2$ on Tape 2} \\
&\quad\text{{\bf if} $M_2$ accepts {\bf then} ACCEPT} \\
\hline
\end{align}$$

### Closure under Intersection

The key idea here is that if $w$ is in $A_1\cap A_2$, then both $M_1$ and $M_2$ will halt. 
$$\begin{align}
\hline
&\text{Execute $M_1$ on $w$} \\
&\text{{\bf if} $M_1$ stops and accepts {\bf then}} \\
&\quad\text{Execute $M_2$ on $w$} \\
&\quad\text{{\bf if} $M_2$ stops and accepts {\bf then} ACCEPT {\bf else} REJECT} \\
&\text{{\bf else} REJECT} \\
\hline
\end{align}$$

### Closure Under Complementation

>[!theorem]
>Recognizable languages are **not** closed under complementation.

Consider the solution we used for [recursive languages](Recursive%20Languages.md#Closure#Closure%20Under%20Complement), where we flip $q_a$ and $q_r$.

On a given input $w$, consider the following:
1. If $M$ stops and accepts $w$, then $\overline M$ stops and rejects $w$
2. If $M$ stops and rejects $w$, then $\overline M$ stops and accepts $w$
3. If $M$ loops forever, then so does $\overline M$

Thus, unless $M$ is halting we can't say that $L(M)=\overline{L(\overline M)}$.

### Closure Under Concatenation

A string $w$ belongs to $A_1.A_2$ if $w$ can be split into two parts $u.v$ such that $u\in A_1,v\in A_2$.

Again, the idea here is that we run several machines in parallel.
$$\begin{align}
\hline
&k\leftarrow \mathrm{length}(w) \\
&\textbf{repeat} \\
&\quad\text{{\bf for} $i=0$ to $k$} \\
&\quad\quad\text{Execute $M_1$ on prefix of $w$ with $i$ symbols} \\
&\quad\quad\text{{\bf if} $M_1$ accepts {\bf then}} \\
&\quad\quad\quad\text{Execute $M_2$ on suffix of $w$ with $k-i$ symbols} \\
&\quad\quad\quad\text{{\bf if} $M_2$ accepts {\bf then} STOP and ACCEPT} \\
&\quad\quad\text{{\bf else} REJECT} \\
&\quad n\leftarrow n+1\\
\hline
\end{align}$$

$M$ is halting, and $L(M)=A_1.A_2$

## Unrecognizability

### Countable Sets

Recall the set of natural numbers $\mathbb N=\{1, 2, 3, \dots\}$.

>[!definition]
>A set $S$ is **countable** if there exists a one-to-one function $f:S\rightarrow \mathbb N$.

>**Examples.**
>- All finite sets 
>- The set $\mathbb Z$ of integers also is (e.g., enumerating as 0, +1, -1, +2, -2, +3, -3, ...)
>- $\mathbb N^2$. In general, if $S, S'$ are both countable, so is $S\times S'$
>- Set of all strings $\Sigma^*$: Enumerate by length
>- Set of all Turing machines: Yes, since they can be encoded as strings
>- Set of recognizable languages: Recognizable languages can be encoding with Turing machines

### Uncountable Sets

>**Example.** $2^{\mathbb N}$, the set of all subsets of $\mathbb N$ (the powerset of $\mathbb N$). 
>
>Suppose $2^{\mathbb N}$ is countable. Consider the enumeration $S_1, S_2, S_3, \dots$. Define the following subset of $\mathbb N: S_d=\{i\mid i\notin S_i\}$. 

Similarly, the set of all languages over an alphabet is uncountable.

### Counting Turing Machines

>[!definition]
>A **characteristic vector** is an infinite vector of $0/1$s, where the $i$-th element is $1$ if $w_i\in A$ and $0$ otherwise. 

Note that we can number all strings $w_i\in\Sigma^*$ because $\Sigma^*$ is countable. Similarly, because Turing machines can be counted, we can create an infinite matrix $C$, where the $i$-th row is the characteristic vector of $M_i$. That is, $C_{ij}=1\iff$ $M_i$ accepts $w_j$.

### Diagonalization Construction

Consider the infinite vector of diagonal entries of $C$. Flip all its bits. The language $A_d=\{w_i\mid w_i\notin L(M_i)\}$, which corresponds to this flipped diagonal vector, is unrecognizable. 


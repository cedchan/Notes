---
Date:
---
## Product Construction

>**Example.** $A_1=\{w\mid w\text{ ends with a}\}, \Sigma=\{\text{a, b}\}$. $M_1:$
>![](Pasted%20image%2020230914121039.png)
>$A_2=\{w\mid w\text{ contains at least one b}\}$. $M_2:$
>![](Pasted%20image%2020230914121138.png)
>**Goal:** Construct DFA $M$ that accepts $w$ iff both $M_1$ and $M_2$ accept $w$.
>
>$M$ should simultaneously execute $M_1$ and $M_2$, maintaining both states: $(\text{state of }M_1, \text{state of }M_2)$.
>![](Pasted%20image%2020230914121645.png)

>[!idea]
>**Given:** DFAs $M_1=(Q_1, \Sigma, q_{01}, F_1, \delta_1), M_2=(Q_2, \Sigma, q_{02}, F_2, \delta_2)$
>**Goal:** Construct DFA $M$ that accepts $w$ iff $M_1$ and $M_2$ both accept $w$.
>
>- Set of states of $M: Q=Q_1\times Q_2$
>	- $|Q|=|Q_1|\cdot|Q_2|$
>	- This is optimal (that is, the product machine must have this many states)
>- Initial state of $M: q_0=(q_{01}, q_{02})$
>- Transition function of $M: \delta((q_1, q_2), \sigma)=(\delta_1(q_1, \sigma), \delta_2(q_2, \sigma))$
>- Set of final states of $M: F=F_1\times F_2$

## Closure of Regular Languages

Below, we show that the class of regular languages is closed under several operations. For each, it suffices to show that there exists a DFA $M$ such that $L(M)$ is equal to the result of operating on any two regular languages.
### Closure under Intersection

>[!theorem]
>The class of regular languages is closed under intersection.

That is, if two languages $A_1, A_2$ are both regular, then so is their intersection.

**Proof.** Consider regular languages $A_1, A_2$. 

By definition of regular languages, there exists DFAs $M_1, M_2$ such that $L(M_1)=A_1, L(M_2)=A_2$. 

Using product construction, construct DFA $M$ such that $L(M)=$ the intersection of $L(M_1)=A_1$ and $L(M_2)=A_2$. By definition (since we have a DFA), $A_1\cap A_2$ is regular. 

### Closure under Union

>[!theorem]
>The class of regular languages is closed under union.

**Proof.** Consider two regular languages $A_1, A_2$.

By definition of regular languages, there exists DFAs $M_1, M_2$ such that $L(M_1)=A_1, L(M_2)=A_2$. 

Let $M_1=(Q_1, \Sigma, q_{01}, F_1, \delta_1), M_2=(Q_2, \Sigma, q_{02}, F_2, \delta_2)$.
- Set of states of $M: Q=Q_1\times Q_2$
- Initial state of $M: q_0=(q_{01}, q_{02})$
- Transition function of $M: \delta((q_1, q_2), \sigma)=(\delta_1(q_1, \sigma), \delta_2(q_2, \sigma))$
- Set of final states of $M: F=\{(q_1, q_2)\mid q_1 \in F_1, \lor q_2 \in F_2\}=(F_1\times Q_1)\cup (Q_2 \times F_2)$

$M$ accepts $w$ iff both $M_1$ and $M_2$ do.

### Closure under Complementation

>[!definition]
>The **complement** of a language $A$ is defined as
>$$\sim A=\{w\mid w\notin A\}$$

>[!theorem]
>The class of regular languages is closed under complementation.

**Proof.** If $M=(Q, \Sigma, q_0, F, \delta)$, than the DFA for $\sim A$ is simply $(Q, \Sigma, q_0, Q\setminus F, \delta)$.

### Concatenation of Languages

>[!definition]
>The **concatenation** of languages is defined as follows:
>$$A_1.A_2=\{u.v \mid u\in A_1 \land v \in A_2\}$$

That is, the concatenation of languages contains all strings that can be split into a string from one language and one from the other.

>**Example.** $\Sigma=\{\text{a, b, c}\}, A_1=\{w\mid w\text{ ends with a}\}, A_2=\{w\mid w\text{ contains only b's}\}$. What is $A_1.A_2$?
>
>$A_1.A_2$ is the set of strings $w$ such that there is an $\mathrm a$ symbol followed by only $\mathrm b$'s. 

>**Example.** $A=\{w\mid \text{``ACC" is a substring of }w\}=\Sigma^*.\{\text{ACC}\}.\Sigma^*$

>[!theorem]
>The class of regular languages is closed under concatenation.

**Proof.** Given input $w$, $M$ needs to check if it is possible to split $w$ into two parts such that the first is accepted by $M_1$ and the second is accepted by $M_2$.

Intuitively, we follow $M_1$ first, then at some point jump to the starting point of $M_2$. The challenge is knowing whether to switch at an accepting state of $M_1$ or continue acting like $M_1$. 

The solution is elegant: add $\varepsilon$-transitions from all final states of $M_1$ to the initial state of $M_2$. 

More formally: Let $M_1=(Q_1, \Sigma, q_{01}, F_1, \delta_1), M_2=(Q_2, \Sigma, q_{02}, F_2, \delta_2)$. We will construct our $\varepsilon$-NFA $M$ as follows:
- Set of states: $Q=Q_1 \cup Q_2$
- Initial state: $q_0 = q_{01}$
- Set of final states: $F=F_2$
- Transition function: $$\begin{align}
\Delta(q, \sigma)&=\begin{cases}
\{\delta_1(q,\sigma)\} & q\in Q_1 \\
\{\delta_2(q, \sigma\} & \text{o.w.}
\end{cases} \\
\Delta(q, \varepsilon)&=\begin{cases}
\{q_{02}\} & q\in F_1 \\
\emptyset & \text{o.w.}
\end{cases}
\end{align}$$
### Prefix Operation

Recall the definition of the [prefix operation](Deterministic%20Finite%20Automata%20(DFA).md#Strings#String%20Operations).

>[!definition]
>$$\mathrm{Prefix}(A)=\{u\mid \exists v \text{ s.t. } u.v \in A\}$$
>That is, the set of prefixes of all strings in $A$.

>**Example.** $A=\{w\mid w\text{ ends in a}\}$.
>
>$\mathrm{Prefix}(A)=\Sigma^*$

>[!theorem]
>If $A$ is regular, then so is $\mathrm{Prefix}(A)$.

**Proof.** Let $M$ be a DFA for $A$. We want to construct an automaton $M'$ that accepts $\mathrm{Prefix}(A)$.

Consider DFA $M'$:
- Same states, initial state and transitions as $M$
- A state $q$ is accepting in $M'$ if there is a path from $q$ to some accepting state of $M$

## Shuffle Operation

>[!definition]
>A string $u$ is a **shuffle** of $w$ if $u$ can be obtained by permuting symbols in $w$.
>$$\mathrm{Shuffle}(A)=\{u\mid \exists w\in A \text{ s.t. } u \text{ is a shuffle of }w\}$$

>**Example.** Shuffles of $011=\{011,101,110\}$

DFA's are **not** closed under the shuffle operation.
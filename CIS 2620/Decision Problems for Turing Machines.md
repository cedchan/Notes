## Problems about DFAs
### Acceptance Problem for DFAs

**Problem:** Given a DFA $M$ and an input string $w$, does $M$ accept $w$?

First we need a way to encode a DFA $M$ as a string. Let $\langle M, w\rangle$ be an input pair, where $\langle M\rangle$ is the string encoding of $M$ and the same applies for $w$.

We can now define out language as follows:
$$A_{\rm DFA}=\{\langle M,w\rangle \mid M \text{ is a DFA}\}$$
This language is halting:
1. Check if the input is well-formed and indeed encodes a DFA $M$.
2. If not, stop and reject
3. If so, execute $M$ on $w$ and check if $M$ ends up in an accepting state
4. If so, stop and accept, else reject

>[!note]
>The machine that solves this problem, $P$, is *not* a DFA, but is rather a TM. It is [decidable](Recursive%20Languages.md) (it's halting), but not [regular](Deterministic%20Finite%20Automata%20(DFA).md#Formal%20Languages#Regular%20Languages).

### Emptiness Problem for DFAs
$$E_{\rm DFA}=\{\langle M\rangle \mid M\text{ is a DFA and $L(M)$ is empty}\}$$
**Problem:** Is this language decidable?

The halting TM $P$ for $E_{\rm DFA}$:
1. First check if the input is well-formed and indeed encodes a DFA $M$
2. If not, stop and reject
3. If so, compute set of states of $M$ that are reachable from its initial state
4. If this set contains some accepting state of $M$, stop and reject ($M$ does accept some strings)
5. Else stop and accept (language of $M$ is empty)

### Equivalence Problem for DFAs

$$EQ_{\rm DFA}=\{\langle M,M'\rangle\mid \text{$M$ and $M'$ are DFAs and $L(M)=L(M')$}\}$$

Recall the algorithm for checking DFA equivalence:
$L(M)=L(M')$ iff
1. $L(M)\cap L(M')^\complement=\emptyset$
2. $L(M)^\complement\cap L(M')=\emptyset$

The same applies for NFAs, regex, etc.

## Problems about Turing Machines

We can similarly encode a TM $M$ with $\langle M\rangle$, which contains the states, tape symbols, and transitions.

### Syntactic Problems about TMs
$$A=\{\langle M\rangle \mid\text{$M$ is a TM and $M$ has 10 states}\}$$
$A$ is decidable because it can be counted from the encoding.

$$\mathrm{SyntacxCorrectC}=\{\langle P\rangle\mid \text{$P$ is a syntactically correct C program}\}$$
```c
int num = 5;
float value = 10.45;
float bigNum;
bignum = num + value;
```

### Semantic Problems about TMs
$$\begin{align}
A_{\rm TM}&=\{\langle M, w\rangle\mid \text{$M$ is a TM and accepts $w$}\} \\
E_{\rm TM}&=\{\langle M\rangle\mid \text{$M$ is a TM and $L(M)=\emptyset$}\} \\
EQ_{\rm TM}&=\{\langle M, M'\rangle\mid \text{$M, M'$ are equivalent TMs}\} \\
\end{align}$$
As it turns out, these problems are **not** decidable.

#### Membership Problems for TMs
$$A_{\rm TM}=\{\langle M, w\rangle\mid \text{$M$ is a TM and accepts $w$}\}$$
A machine $U$ to solve this problem must simulate the execution of $M$ on $w$. 
![](Pasted%20image%2020231024124237.png)
$$\begin{align}
\hline
&{\bf repeat} \\
&\quad\text{Find transition on Tape1 that matches state on Tape 4 and} \\ &\quad\quad\text{symbol read by Head 2 on Tape 2} \\
&\quad\text{Update state on Tape 3, symbol at Head 2 on Tape 2, and} \\ &\quad\quad\text{move Head 2} \\
&\quad\text{{\bf if} state of $M$ on Tape 3 equals $q_a$ {\bf then} stop and accept} \\
&\quad\text{{\bf if} state of $M$ on Tape 3 equals $q_r$ {\bf then} stop and reject}\\
\hline
\end{align}$$

## Universal Turing Machines

>[!definition]
>A **universal Turing machine** $U$ as a TM that takes in an input that is also a TM.
>
>Given $\langle M\rangle$ and $w$ as inputs, $U$ maintains state and tape content of $M$ on its tapes and updates them step-by-step by applying transitions of $M$.
>
>In modern terminology, $U$ is an interpreter for Turning machines, and can itself be implemented as a Turing machine.

$L(U)$ is defined as:
1. If $M$ accepts $w$, then $U$ accepts $\langle M,w\rangle$
2. If $M$ rejects $w$, then $U$ rejects $\langle M,w\rangle$
3. If $M$ does not halt on $w$, then $U$ does not halt on $\langle M,w\rangle$

**Claim:** $L(U)=A_{\rm TM}=\{\langle M,w\rangle\mid M\text{ is a TM and accepts } w\}$
Hence, $A_{\rm}$ is recognizable ($U$ is not halting, so can't say decidable)

>[!theorem]
>$A_{\rm TM}$ is undecidable.

**Proof.** Assume for contradiction that $A_{\rm TM}$ is decidable. Then, there exists a halting TM $H$ such that $L(H)=A_{\rm TM}$.

Given input $\rangle M,w\langle$, if $M$ accepts $w$, $H$ stops and accepts $\rangle M, w\langle$. Otherwise, it rejects $w$.

Since $H$ exists, then so must $D$, where $D$ flips the output of $H$ and only requires one input.
![](Pasted%20image%2020231024130043.png)
Now, we ask, does $D$ accept $\langle D\rangle$?

$L(D)=\{\langle M\rangle\mid M\text{ is a TM that doesn't accept }\langle M\rangle\}$

By construction, $\langle D\rangle\in L(D)$ iff $D$ is a TM that doesn't accept $\langle D\rangle$.

Thus $\langle D\rangle\in L(D)\iff \langle D\rangle\notin L(D)$. Contradiction. 

Intuitively, this tells us that if a machine is universal (i.e., can simulate other machines), then its own behavior can't be analyzed by other machines. That is, a machine can't tell if it is itself making an error, sech as entering an infinite loop.


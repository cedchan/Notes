## Encoding Problems
### Strings

>[!definition]
>An **alphabet** $\Sigma$ is a finite set of symbols used for encoding

>**Example.** $\Sigma=\{a, b\}$

>[!definition]
>A **string** $w$ over an alphabet $\Sigma$ is a finite sequence of symbols in $\Sigma$.
>
>$\Sigma^*$ denotes the set of all strings over $\Sigma$.

>**Examples.** $\Sigma=\{a, b\}$
>- $\varepsilon$: empty string (i.e., length 0)
>- $abb$

#### String Operations
- **Concatenation $(.)$:** Given strings $u, v$, $u.v$ denotes their concatenation.

- **Prefix:** A string $u$ is a prefix of string $w$ if there exists a string $v$ such that $w=u.v$ ($\exists v \text{ s.t. } w=u.v \implies u$ is a prefix of $w$)

>[!note]
>This means that a string of length $k$ will have $k+1$ prefixes (consider $\varepsilon$).

- **Suffix:** A string $u$ is a suffix of string $w$ if there exists a string $v$ such that $w=v.u$.

- **Substring:** A string $u$ is a substring of string $w$ if there exist strings $v$ and $v'$ such that $w=v.u.v'$

>[!warning]
>Because substrings can have repeats, the "number" of substrings is really an upper bound.

### Languages

>[!definition]
>A **language** $A$ over an alphabet $\Sigma$ is a set of strings over $\Sigma$. That is, $A\subseteq\Sigma^*$.

Decision problems can be encoded as a language $A$ and a string $w$ where we ask whether $w\in A$.

>**Example.** Determine whether a document contains all the vowels.
>
>$\Sigma=$ All English text characters
>$w$: The text document
>Let $count(w, \sigma)$ denote the number of times $\sigma$ appears in $w$.
>$$\begin{align}
A_1&=\{w\mid\text{each of the vowels a, e, i, o, u occurs at least once in } w\} \\
A_1&=\{w\mid count(w, \mathrm{a})>0 \land count(w, \mathrm e)>0 \land count(w, \mathrm i)>0 \land \\
&\qquad count(w, \mathrm o)>0 \land count(w, \mathrm u)>0 \}
\end{align}$$

>**Example.** Problem: Given the graph of Facebook friends connections, find the person with the highest number of connections.
>
>$\Sigma=\{0, 1, \#\}$ (nodes are represented in binary, with $a\#b$ denoting an edge $(a, b)$)
>$A_3=\{w\mid w \text{ encodes a graph over } n \text{ people such that person } k \text{ has the highest number of connections}\}$

## Automata

>[!definition]
>An **automaton** $M$ for a language $A$ reads an input string $w$ from left to right, one symbol at a time. Then, $M$ accepts or rejects $w$ as part of $A$.

### Finite-State Automata

>[!definition]
>A **finite-state automaton** $M$ has some fixed (finite) number of states. One of these states is initial. For each state, $M$ specifies a transition to another state based on the symbol being read.
>
>Some states are marked as **accepting states**. If $M$ ends on an accepting states, it accepts $w$. Otherwise, it rejects $w$.

>**Example.** Construct an automaton for $A=\{w\mid w\text{ contains an even number of a's}\}$, where $\Sigma=\{\text{a, b}\}$
>![](Pasted%20image%2020230831125214.png)

>**Example.** Construct an automaton for $A=\{w\mid w\text{ ends with a}\}$, where $\Sigma=\{\text{a, b}\}$
>![](Pasted%20image%2020230831125626.png)

>**Example.** Construct an automaton for $A=\{w\mid w\text{ contains the substring ``ACC"}\}$, where $\Sigma=\{\text{A, C, G, T}\}$
>![](Pasted%20image%2020230831130018.png)
>Precisely describe the set of strings $w$ such that the machine is in state $q_2$ after reading $w$: $\{w\mid w \text{ doesn't contain the substring ``ACC" and ends with ``AC"}\}$.

>**Example.** Construct an automaton for $A=\{w\mid count(w, \text{a})=count(w, \text b)\}$, where $\Sigma=\{\text{a, b}\}$.
>![](Pasted%20image%2020230831130423.png)
>Since the number of states you need is unbounded, it can't be represented with a finite-state automaton.

>**Example.** Construct an automaton for $A=\{w\mid \text{decimal number corresponding to } w \text{ is divisible by 3}\}$, where $\Sigma=[0..9]$.
>
>We can use the trick that if the sum of a number's digits is divisible by 3, then the number is divisible by 3. We can further simplify by representing each digit modulo 3. 
>![](Pasted%20image%2020230831131249.png)

### Formal Definition

>[!definition]
>A **deterministic finite automaton (DFA)** $M$ consists of 
>- a finite set $Q$ of states
>- a finite alphabet $\Sigma$
>- a state $q_0 \in Q$ called the initial state
>- a subset $F\subseteq Q$ called accepting states
>- a transition function $\delta: Q\times\Sigma\rightarrow Q$ (if $M$ reads symbol $\sigma$ in state $q$, the resulting state is $\delta(q, \sigma)$)
>
>$L(M)$ is the set of strings $w$ over $\Sigma$ that $M$ accepts (i.e., the language of the machine).

The **syntax** of a DFA includes its states, alphabet, transitions, initial state, and accepting states. Syntactic questions include: How many states does $M$ have?

The **semantics** of a DFA is the mathematical set that captures what it computes/solves—that is, its language $L(M)$. Semantic questions include: Is $w$ in $L(M)$? Is $L(M)$ finite?
## Extended Transition Function

Let $M=(Q, \Sigma, q_0, F, \delta)$ be a DFA

$\delta: Q \times \Sigma \rightarrow Q$ is a **one-step** transition function:
- Maps a state and a single symbol to a state
- $\delta(q, \sigma)$: If $M$ starting in state $q$ reads a symbol $\sigma$, where will it be?

$\delta^*: Q\times \Sigma^*\rightarrow Q$ is a **multi-step** transition function:
- Maps a state and a string $w$ to a state
- $\delta^*(q, w)$: If $M$ starting in state $q$ processes the entire string $w$, where will it be?

### Inductive Definition

How do we define $\delta^*$ in terms of $\delta$?

>[!definition] 
>A string $w$ is either the empty string $\varepsilon$ or is of the form $x\sigma$, where $x$ is a string (of length one shorter than $w$) and $\sigma$ is a symbol.$$\begin{align}
\delta^*(q, \varepsilon)&=q \\
\delta^*(q, x\sigma)&=\delta(\delta^*(q, x), \sigma)
\end{align}$$
>

Above, the first clause says how strings of length 0 are processed and second says how strings of length $n+1$ are processed by relying on processing of strings of length $n$.

>**Example.** $$\begin{align}
\delta^*(q, ab) &= \delta(\delta^*(q, a), b)) \\
&=\delta(\delta(\delta^*(q, \varepsilon),a),b) \\
&=\delta(\delta(q,a),b)
\end{align}$$
## Formal Languages

>[!definition]
>Let $M=(Q,\Sigma,q_0,F,\delta)$ be a DFA. $M$ accepts $w$ if $\delta^*(q_0, w) \in F$. 
>$$L(M)=\{w\mid\delta^*(q_0,w) \in F\}$$

>**Examples.** 
>**1.** If $F=Q$, what is $L(M)$? 
>$\Sigma^*$
>**2.** If $F$ is the empty set $\emptyset$, what is $L(M)$? 
>Empty set of strings $\emptyset$
>**3.** If $F=\{q_0\}$, what is $L(M)$?
>$L(M)$ contains the empty string $\varepsilon$, but can't say much more
### Regular Languages

>[!definition]
>A language $A$ is **regular** if there exists a DFA $M$ such that $L(M)=A$. That is, the problem encoded by $A$ can be solved by a finite-state automaton.

## Proving Correctness

How do you prove $M$ is correct—that is, that $M$ accepts a string $w$ iff $w \in A$?

>**Example.** $\Sigma=\{\text{a, b}\}, A=\{w\mid\mathrm{count}(w,\mathrm a) \text { is even}\}$. Prove the correctness of our DFA $M$:
>![](Pasted%20image%2020230831125214.png)
>
>To prove: For all strings $w$, $M$ accepts $w$ iff $\mathrm{count}(w, \mathrm a)$ is even
>To prove: For all strings $w$, $\delta^*(q_0, w)=q_0$ iff $\mathrm{count}(w, \mathrm a)$ is even
>
>>[!solution]+
>>**Proof.** Induction on string length/structure
>>
>>***Base Case:*** Prove the claim for $w=\varepsilon$.
>>
>>There are no $\mathrm a$'s, which is an even number, so the DFA is correct.
>>
>>***Inductive case:*** Assume the claim holds for an arbitrary string $x$. Prove the claim for $w=x.\sigma$, where $\sigma\in \Sigma=\{\text{a, b}\}$.
>>
>>$\delta^*(q_0, x)$ can be $q_0$ or $q_1$, and $\sigma$ can be $\mathrm a$ or $\mathrm b$. We thus have 4 cases: 
>>
>>*Case 1*: $\delta^*(q_0, x)=q_0$ and $\sigma=\mathrm b$
>>By IH, $\mathrm{count}(x, \mathrm a)$ is even. We want to show $\delta^*(q_0, x.b)=q_0$ iff $\mathrm{count}(x.b, a)$ is even. $$\begin{align}
\delta^*(q_0, x.\mathrm b)&=\delta(\delta^*(q_0, x), \mathrm b) & \text{(by defn. of } \delta^*) \\
&=\delta(q_0, \mathrm b) & (\text{assumes }\delta^*(q_0, x)=q_0) \\
&=q_0 & \text{(by definition of transition func.)}
\end{align}$$
>>Adding $\mathrm b$ to a string doesn't change the number of $\mathrm a$'s, so $\mathrm{count})x.\mathrm b, \mathrm a)=\mathrm{count}(x, \mathrm a)$, which is even in this case.

>**Example.** Prove the correctness of this DFA that checks if a string has at least 2 $\mathrm a$'s.
>![](Pasted%20image%2020230905124452.png)
>
>>[!solution]- Failed Solution
>>**Proof.** Induction on string $w$.
>>
>>***Base Case:*** Show $\delta^*(q_0, \varepsilon)=q_2$ iff $2\leq \mathrm{count}(\varepsilon,\mathrm a)$.
>>$\delta^*(q_0, \varepsilon)=q_0$ by definition of $\delta^*$. $\mathrm{count}(\varepsilon, \mathrm a)=0$, and we land on $q_0$, which is correctly not accepted.
>>
>>***Induction Step:*** Assume from IH that $\delta^*(q_0, x)=q_2$ iff $2\leq \mathrm{count}(x,\mathrm a)$. Show for $\sigma\in\Sigma$ that $\delta^*(q_0, x.\sigma)=q_2$ iff $2\leq\mathrm{count}(x.\sigma,\mathrm a)$.
>>
>>*Case 1:* $\delta^*(q_0, x)=q_0$ and $\sigma=\mathrm a$
>>By IH, $2 > \mathrm{count}(x, \mathrm a)$. Show $\delta^*(q_0, x.\mathrm a)=q_2$ iff $2\leq \mathrm{count}(x.\mathrm a, \mathrm a)$. 
>>
>>The proof fails! $\mathrm{count}(x, \mathrm a)=1$ and $\delta^*(q_0, x)=q_0$ is consistent with our assumptions. Then, $\mathrm{count}(x.\mathrm a, \mathrm a)=2$, but $\delta^*(q_0, x.\mathrm a)=\delta(q_0, \mathrm a)=q_1$. Claim doesn't hold. 
>>
>>We must either prove intermediate lemmas about how we arrive in $q_0$ or make a stronger claim.
>
>>[!solution]+
>>Stronger Claim: $$\delta^*(q_0, w)=\begin{cases}
q_0 & \text{if } \mathrm{count}(w, \mathrm a)=0\\
q_1 & \text{if } \mathrm{count}(w, \mathrm a)=1\\
q_2 & \text{if } 2\leq\mathrm{count}(w, \mathrm a)
\end{cases}$$
>>***Base Case:*** $w=\varepsilon$.
>>
>>$\delta^*(q_0, \varepsilon)=q_0$. There are no $\mathrm a$'s, so we're correct.
>>
>>***Inductive Case:*** Assuming 
>>
>>$$
\delta^*(q_0, x)=\begin{cases}
q_0 & \text{if } \mathrm{count}(w, \mathrm a)=0\\
q_1 & \text{if } \mathrm{count}(w, \mathrm a)=1\\
q_2 & \text{if } 2\leq\mathrm{count}(w, \mathrm a)
\end{cases}$$
>>show 
>>$$\delta^*(q_0, x.\sigma)=\begin{cases}
q_0 & \text{if } \mathrm{count}(w, \mathrm a)=0\\
q_1 & \text{if } \mathrm{count}(w, \mathrm a)=1\\
q_2 & \text{if } 2\leq\mathrm{count}(w, \mathrm a)
\end{cases}$$
>>*Case 1*: $\delta^*(q_0, x)=q_0$ and $\sigma=\mathrm a$. $$\begin{align}
\mathrm{count}(x, \mathrm a)&=0 & \text{(by IH)}\\
\mathrm{count}(x.\mathrm a, \mathrm a)&=1 \\
\delta^*(q_0, x.\mathrm a)&=\delta(q_0, \mathrm a) & (\text{by defn. of }\delta^*)\\
&=q_1 & (\text{by defn. of } \delta)
\end{align}$$
>>Five remaining cases are similar.

>**Example.** Prove the correctness of our DFA $M$ for $A=\{w\mid w\text{ contains the substring ``ACC"}\}$, where $\Sigma=\{\text{A, C, G, T}\}$
>![](Pasted%20image%2020230831130018.png)
>
>>[!solution]+
>>**Proof.** 
>>***IH:*** $$\delta^*(q_0, w)=\begin{cases}
q_3 & \text{if $w$ contains the substring ``ACC"} \\
q_2 & \text{if $w$ contains the substring ``ACC" and ends with ``AC"} \\
q_1 & \text{if $w$ contains the substring ``ACC" and ends with ``A"} \\
q_0 & \text{otherwise}
\end{cases}$$ 

## A Lower Bound on the States

There can be multiple DFAs that solve the same problem. How do we know what the minimum number of states needed for a DFA is?

>**Example.** $\Sigma=\{\text{a, b}\}, A_2=\{w \mid \text{2nd symbol in }w\text{ is a}\}$
>
>One correct DFA:
> ![](Pasted%20image%2020230907120740.png)
> Another correct DFA with fewer states:
> ![](Pasted%20image%2020230907120812.png)
> In this case, 4 is the minimum number of states needed, but how do we prove this?

### Distinguishable Strings

>[!definition]
>Two strings $u, b$ are **distinguishable** with respect to a language $A$ if there exists a string $w$ such that only one of $u.w$ and $v.w$ is in $A$. 

Note that this definition is language-dependent, but not machine-dependent.

>**Example.** $A=\{w \mid \text{2nd symbol in }w\text{ is a}\}$
>
>- $\varepsilon$ and $\mathrm a$
>	Yes, because with $w=\mathrm a$, $\varepsilon.\mathrm a \notin A, \mathrm{a.a} \in A$
>- $\mathrm a$ and $\mathrm b$
>	No, because for all $w$, $\mathrm a.w \in A \iff \mathrm b.w \in A$
>- $\mathrm{ab}$ and $\mathrm{ba}$
>	Yes, because $\mathrm{ab}.\varepsilon \notin A, \mathrm{ba.\varepsilon} \in A$

>[!lemma]
>If $M$ accepts $A$ and string $u$ and $v$ are distinguishable w.r.t. $A$, then $\delta^*(q_0, u)\neq \delta^*(q_0, v)$.

**Proof.** 
We will use a proof by contradiction. Suppose $\delta^*(q_0, u)=\delta^*(q_0, v)=q$ for two distinguishable strings $u, v$. By definition, there is a string $w$ such that only one of $u.w, v.w$ is in $A$. But the states of $u.w$ and $v.w$ are equal ($\delta^*(q_0, u)$, so $M$ accepts both or rejects both. This is a contradiction.

>[!lemma]
>If $S=\{w_1, w_2, \dots, w_k\}$ is a set of $k$ pairwise distinguishable strings, then every DFA for $A$ must have at least $k$ states.

**Proof.**
Suppose $M$ is a DFA such that $L(M)=A$. Consider the states $\delta^*(q_0, w_1), \delta^*(q_0, w_2), \dots, \delta^*(q_0, w_k)$. By the previous lemma, all these states must be distinct. It follows that require at least $k$ states.

>**Example.** A parametric example: $\Sigma=\{\text{a, b}\}$. For each number $k$, $A_k=\{w\mid k\text{-th symbol in } w \text{ equals a}\}$. How many states are necessary and sufficient to accept $A_k$ as a function of $k$?
>
>>[!solution]+
>>For each $k$, define DFA $M_k$. $Q=\{q_0, q_1, \dots, q_{k-1}, q_a, q_r\}$.
>>Initial state is $q_0$, accepting states are $\{q_a\}$.
>>Transition function: $\delta(q_i, \sigma)=q_{i+1}$ for $i=[0..k-2]$ for $\sigma\in\{\text{a, b}\}$.$$\begin{gather}
\delta(q_{k-1}, a) =q_a, \delta(q_{k-1}, b)=q_r  \\
\delta(q_a, \sigma)=\delta(q_r, \sigma)=q_r \text{ for $\sigma\in\{\text{a, b}\}$}
\end{gather}$$
>>For each $k$, $L(M)=A_k$. This shows that $k+2$ states are sufficient. 
>>
>>Now we prove $k+2$ states are necessary. Consider the set of $k+2$ strings $\{\varepsilon, \mathrm b, \mathrm b^2, \dots, \mathrm b^k, \mathrm a^k\}$. We must show that every pair of strings in this set is distinguishable. That is, that $\forall i, j \in [0, k] \text{ s.t. } i < j, u=\mathrm b^i, v=\mathrm b^j$ are distinguishable. 
>>
>>To do this, we choose $w$ so that only one of $u.w, v.w$ is in $A_k$. One solution is $w=\mathrm b^{k-j-1}\mathrm a$. That is, the longer string will be padded with $\mathrm b$'s until the $k$-th symbol, which is an $\mathrm a$. Thus, $v\in A_k$, but since $u$ is not even $k$ symbols long, $u\notin A_k$.
>>
>>It remains to show that $\forall i\in [0, k], \mathrm b^i, \mathrm a^k$ are distinguishable. We can trivially choose $w=\varepsilon$. $\mathrm a^k$ is already in the language while none of the others are, since they contain no $\mathrm a$'s

>**Example.** $\Sigma=\{\text{a, b}\}, A^k=\{w\mid k\text{-th symbol from end in }w\text{ equals a}\}$. Prove that DFA for $A^k$ must have at least $2^k$ states.
>
>>[!solution]+
>>Set of strings: $\{\text{a, b}\}^k$ (that is, all strings of length $k$). Consider two distinct strings in this set: $u=c_1c_2\dots c_k, v=d_1d_2\dots d_k$. We want to prove that $u$ and $v$ are distinguishable—that is, find a string $w$ such that exactly one of $u.w, v.w$ is in $A^k$.
>>
>>Since $u\neq v$, there is necessarily an index $i$ such that $c_i\neq d_i$—one is $\mathrm a$ while the other is $\mathrm b$. Thus, if we add $w$ of length $i-1$ (such that $i$ is the $k$-th symbol from the end), only one of $u.w, v.w$ is in $A^k$.


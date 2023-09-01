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

## Regular Languages

>[!definition]
>A language $A$ is **regular** if there exists a DFA $M$ such that $L(M)=A$. That is, the problem encoded by $A$ can be solved by a finite-state automaton.





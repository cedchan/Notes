## Introduction

The [automata](Deterministic%20Finite%20Automata%20(DFA).md) that we've studied can solve regular languages, but can't be generalized to more complex problems. Turing machines are another class of machines that are **universal**—that is, they can solve any problem that a computer can solve.

The input of a Turing machine is called the **tape**: a sequence (or array) of cells, each of which holds a symbol. The tape acts like the memory of a modern computer, and initialized to the input string, with blanks _ to the right.

A TM has finitely many states $Q$, like a DFA, one of which is the initial $q_0$. The **head** of a TM points to a specific tape cell (like an array index). The head is initialized to the left-most tape cell.

The transition of a TM is based on the current state and symbol of the head, and can do the following
- Overwrite current symbol
- Move left or right
- Update state

(Note that it can go back and forth in one transition.)

>**Example.** Design a TM to accept the set of palindromes. Tape alphabet $\Gamma=\{\text{a, b, \_, \#}\}$.
>
>![](Pasted%20image%2020231005124441.png)

## Syntax

>[!definition]
>A **Turing Machine** $M$ consists of:
>- A finite set $Q$ of states
>- Initial state $q_0 \in Q$
>- Accepting state $q_a \in Q$
>- Rejecting state $q_r\neq q_a \in Q$
>- Tape alphabet $\Gamma$
>- Input alphabet $\Sigma \subset \Gamma$
>- Blank symbol $\_ \in \Sigma, \notin \Gamma$
>- Transition function $\delta: Q\times\Gamma\rightarrow Q\times\Gamma\times\{\text{L, R}\}$
>	$$\delta(q, \sigma)=(q',\gamma,\text{L/R})$$ 
>	means that in state $q$, when the current tape cell contains $\sigma$, then write $\gamma$, move left/right, and go to state $q'$
>
>$M$ can be written as a tuple: $M=(Q, q_0, q_a, q_r, \Gamma, \Sigma, \_, \delta)$. 

Note that the input to $M$ is a string $w\in\Sigma^*$.

As soon as $M$ lands in $q_a$ or $q_r$, it is immediately accepted/rejected.

### Possible Outcomes

There are 4 possible outcomes a TM can have on an input $w$
1. State becomes an accepting state: $M$ accepts $w$
2. State becomes a rejecting state: $M$ rejects $w$
3. From left-most cell, $M$ wants to move left: $M$ rejects $w$
4. $M$ goes into an infinite loop

>[!definition]
>A Turing machine $M$ is said to be **halting** if for every input $w$, the execution of $M$ is finite/terminating. That is, it doesn't neter infinite loops.

### Formalizing Executions

>[!definition]
>The **configuration** of a machine is all the information needed to determine future behavior. Specifically, it would be the state, contents of tape, and position of head.

The configuration $C$ can be written succinctly and precisely as a triple of this information. 

>[!error]
>fill this in
## Recursive Languages

>[!definition]
>A language $A$ is **decidable**, or equivalently **recursive** if there exists a halting Turing machine $M$ such that $L(M)=A$. That is, there is a TM $M$ that given an input $w$, if $w$ is in $A$ halts in the accepting state and otherwise halts in the rejecting state.

Decidable problems are "solvable."

>[!lemma]
>Regular languages are decidable.

You can see this by continually moving right until the end. Then, when we hit $\_$, we accept/reject based on whether the state is in $F$.

>**Example.** $\mathrm{PRIMES}=\{0^p\mid p\text{ is a prime number}\}$
>
>>[!solution]+
>>$$\begin{align}
\hline
&\textbf{High-level Algorithm}\\
\hline
&\text{\bf if } p = 0 \lor p = 1 \textbf{ then } \text{accept} \\
&\text{\bf else } \\
&\quad i\leftarrow 2 \\
&\quad \textbf{while }i<p: \\
&\quad\quad\text{\textbf{if} $p$ is a multiple of $i$ \textbf{then} stop and accept}\\
&\quad\quad i\leftarrow i+1 \\
&\quad \text{accept} \\
\hline
\end{align}$$
>>From a high level, we look at the remaining $0$s, increasing the number of $1$s by one each time, to check if the number is divisible by any number. 
>>
>>1. Check if input is $\varepsilon$ or $0$. If so, accept.
>>2. If not, add $\#$ at the beginning and replace the first two $0$s with $1$s.
>>3. Check if remaining number of $0$s is divisible by 2. If so, stop and reject, else change first $0$ to $1$.
>>4. Check if remaining number of $0$s is divisible by 3. If so, stop and reject, else change next $0$ to $1$, and so on.
>>
>>To check if the number of $0$'s is divisible by the number of $1$s, repeatedly subtract the number of $1$s from the number of $0$s. For each $1$ find a corresponding $0$ and change it to $\mathrm y$. If no $0$ is found, answer is NO, otherwise YES.
>>
>>See slides for step-by-step.
>>![](Pasted%20image%2020231010123447.png)


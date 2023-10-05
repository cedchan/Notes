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







## Introduction

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

## Closure

### Closure Under Intersection

Given two decidable languages $A_1$ and $A_2$, there exist halting TMs $M_1$ and $M_2$ such that $L(M_1)=A_1$ and $L(M_2)=A_2$. 

Consider the following TM $M$, given input $w$:
$$\begin{align}
\hline
&\text{Execute $M_1$ on $w$}\\
&\text{{\bf if} $M_1$ accepts {\bf then}}\\
&\quad\text{Execute $M_2$ on $w$} \\
&\quad\text{{\bf if} $M_2$ accepts {\bf then} ACCEPT {\bf else} REJECT}\\
&\text{{\bf else} REJECT}\\
\hline
\end{align}$$
$M$ is a halting TM, and $L(M)=A_1\cap A_2$.

### Closure Under Union

Given two decidable languages $A_1$ and $A_2$, there exist halting TMs $M_1$ and $M_2$ such that $L(M_1)=A_1$ and $L(M_2)=A_2$. 

Consider the following TM $M$, given input $w$:
$$\begin{align}
\hline
&\text{Execute $M_1$ on $w$}\\
&\text{{\bf if} $M_1$ accepts {\bf then} ACCEPT}\\
&\text{{\bf else}}\\
&\quad\text{Execute $M_2$ on $w$} \\
&\quad\text{{\bf if} $M_2$ accepts {\bf then} ACCEPT {\bf else} REJECT}\\
\hline
\end{align}$$
$M$ is a halting TM, and $L(M)=A_1\cup A_2$.

### Closure Under Complement

Decidable languages are closed under complementation. We can do this by just switching $q_a$ and $q_r$.

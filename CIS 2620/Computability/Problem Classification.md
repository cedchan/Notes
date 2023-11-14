
**Problem:** Given a problem $A$, decide if it is (1) [decidable](Recursive%20Languages.md), (2) [recognizable](Recognizable%20Languages.md) but undecidable, or (3) [unrecognizable](Recognizable%20Languages.md#Unrecognizability).

**Upper bound techniques:**
- To show $A$ is decidable, find a halting TM/program for it
- To show $A$ is recognizable, find a TM/program that accepts it

How to show A is undecidable or unrecognizable:
- Use of closure properties
- Technique of problem reduction

## Combining Two Recognizers

>[!theorem]
>If a language $A$ and its complement $A^\complement$ are both recognizable, then both must be decidable.

Suppose $A$ and $A^\complement$ to be recognizable. Then there is a TM $M$ for $A$ and another TM $M'$ for $A^\complement$. 

To get a halting TM for $A$, we can run $M$ and $M'$ in parallel. Specifically, first copy the input string to both tapes, then repeat the following:
1. Execute one transition of $M$ on Tape 1;
 2. If $M$ stops and accepts, stop and accept;
 3. Execute one transition of $M’$ on Tape 2;
 4. If $M’$ stops and accepts, stop and reject

## Halting Problem for TMs
$$\mathrm{HALT_TM}=\{\langle M, w\rangle\mid \text{$M$ is a TM and $M$ halts on $w$}\}$$
Is this problem decidable, recognizable-but-undecidable, or unrecognizable?

>[!lemma] Claim 1
>$\mathrm{HALT_TM}$ is recognizable.

Consider the following TM $R$:
$$\begin{align}
\hline
&\text{Given input $\langle M, w\rangle$,} \\
&\quad\text{{\bf if} $\langle M\rangle$ doesn't encode a TM {\bf then} stop and reject} \\
&\quad\text{Execute $M$ step-by-step on inpyt $w$} \\
&\quad\text{{\bf if} $M$ stops and accepts, {\bf then} stop and accept $\langle M, w\rangle$} \\
&\quad\text{{\bf if} $M$ stops and rejects, {\bf then} stop and reject $\langle M, w\rangle$} \\
\hline
\end{align}$$

>[!lemma] Claim 2
>We know $\mathrm{A_TM}=\{\langle M, w\rangle\mid M\text{ accepts }w\}$ is undecidable.
>
>Undecidability of $\mathrm{A_TM}$ implies undecidability of $\mathrm{HALT_TM}$.

The technique here is reducing one problem into another. This is known as **language/problem reduction**.

We want to show that $\mathrm{A_TM}$ reduces to $\mathrm{HALT_TM}$. That is, that we can construct a TM for $\mathrm{A_TM}$ using a "black box" TM for $\mathrm{HALT_TM}$.

Consider a halting TM $H$ that solves $\mathrm{HALT_TM}$. Let $T$ solve $\mathrm{A_TM}$:
$$\begin{align}
\hline
&\text{{\bf if} $\langle M\rangle$ doesn't encode a TM {\bf then} reject} \\
&\text{Execute $H$ on input $\langle M, w\rangle$} \\
&\text{{\bf if} $H$ rejects {\bf then} reject} \\
&\text{{\bf else} execute $M$ on input $w$}\\
&\text{{\bf if} $M$ accepts {\bf then} accept {\bf else} reject}\\
\hline
\end{align}$$
Here, we've shown that if $\mathrm{HALT_TM}$ is decidable, then $\mathrm{A_TM}$ is decidable. Then the contrapositive is true: if $\mathrm{A_TM}$ is undecidable, then $\mathrm{HALT_TM}$ is undecidable.

## Non-Emptiness Problem for TMs
$$\mathrm{NE_TM}=\{\langle M\rangle\mid \text{$M$ is a TM and $L(M)\neq\emptyset$}\}$$
Given a TM, we want to check if there exists a string that it accepts.

Is this problem decidable, recognizable-but-undecidable, unrecognizable?

>[!lemma] Claim 1
>$\mathrm{NE_TM}$ is recognizable.

Given a TM $M$,
1. Find a string $w$
2. Check if $M$ accepts $w$

There are infinite (but countably many) choices for $w$. The execution of $M$ on any given string may not be halting.

Consider a matrix where the columns represents the number of steps, and the rows represent unique strings.

| |1|2|3|4|$\dots$|
|-|-|-|-|-|-|
|$w_1$|||||
|$w_2$|||||
|$w_3$|||||
|$w_4$|||||
|$\,\, \vdots$|||||

We want to find if $M$ accepts any string, so we can execute $M$ on all strings in parallel, and stop if any gets accepted. Then, we want to find whether there exists $i, j$ such that $M$ accepts string $w_i$ in $j$ steps.

More precisely,
$$\begin{align}
\hline
&k\gets1 \\
&\textbf{repeat} \\
&\quad\text{{\bf for} i = 1 {\bf to} $k$}\\
&\quad\quad \text{Simulate $M$ on $w_i$ for $k$ steps} \\
&\quad\quad\text{{\bf if} $M$ accepts {\bf then} accept} \\
&\quad k\gets k+1 \\
\hline
\end{align}$$

>[!lemma] Claim 2
>$\mathrm{NE_TM}$ is undecidable.

Again, we show this with problem reduction. Specifically, we want to show that $\mathrm{NE_TM}$ is decidable $\implies$ $\mathrm{A_TM}$ is decidable. Otherwise, given a halting TM $R$ for $\mathrm{NE_TM}$, construct a halting TM $T$ for $\mathrm{A_TM}$.

Given a TM $M$, define $M'$ such that $M$' accepts some input exactly when $M$ accepts $w$.
$$\begin{align}
\hline
&\text{Given an input $x$}\\
&\quad\text{Execute $M$ on $w$}\\
&\quad\text{{\bf if} $M$ accepts $w$ {\bf then} accept $x$}\\
\hline
\end{align}$$
For every input $x$, $M'$ accepts $x$ exactly when $M$ accepts $w$. Claim: If $M$ accepts $w$, then $L(M')=\Sigma^*$. Else $L(M')=\emptyset$. 

Consider a halting TM $R$ that solves $\mathrm{NE_TM}$. Define the following TM $T$ with input $\langle M,w\rangle$:
$$\begin{align}
\hline 
&\text{{\bf if} $\langle M\rangle$ doesn't encode a TM {\bf then} reject}\\
&\text{Construct the description $\langle M'\rangle$ as follows:} \\
&\quad\text{``Given an input $x$}\\
&\quad\quad\text{Execute $M$ on $w$}\\
&\quad\quad\text{{\bf if} $M$ accepts $w$ {\bf then} accept $x$"}\\
&\text{Execute $R$ on $\langle M'\rangle$}\\
&\text{{\bf if} $R$ accepts {\bf then} accept {\bf else} reject}\\
\hline
\end{align}$$
Here, we've shown that if $\mathrm{NE_TM}$ is decidable, then so is $\mathrm{A_TM}$.

## Emptiness Problem for TMs
$$\mathrm{E_TM}=\{\langle M\rangle\mid \text{$M$ is a TM and $L(M)=\emptyset$}\}$$

>[!lemma] Claim
>$\mathrm{E_TM}$ is unrecognizable.

Suppose for contradiction that $\mathrm{E_TM}$ is recognizable. Then so is $(\mathrm{NE_TM})^\complement$. We know that if a language and its complement are recognizable, then both must be decidable, contradicting that $\mathrm{NE_TM}$ is undecidable.

## Example Problem
$$P=\{\langle M\rangle\mid\text{$M$ is a TM and $L(M)\cap0^*=\emptyset$}\}$$
Given a TM, check that it doesn't accept any string with only $0$s. Is this problem decidable, recognizable-but-undecidable, or unrecognizable.

Consider the complement $P^\complement$. Given TM $M$ accepts some string with only $0$s. 

>[!lemma] Claim
>$P^\complement$ is recognizable but undecidable. It follows that $P$ is unrecognizable.

The proof that $P^\complement$ is recognizable is straightforward. Simultaneously run the machine on different inputs of the form $0^n$ and accept if $M$ accepts.

Showing undecidability can be done with problem reduction. We can actually use the same $M'$ reduction from the [non-emptiness problem](Problem%20Classification.md#Non-Emptiness%20Problem%20for%20TMs).
$$\begin{align}
\hline 
&\text{{\bf if} $\langle M\rangle$ doesn't encode a TM {\bf then} reject}\\
&\text{Construct the description $\langle M'\rangle$ as follows:} \\
&\quad\text{``Given an input $x$}\\
&\quad\quad\text{Execute $M$ on $w$}\\
&\quad\quad\text{{\bf if} $M$ accepts $w$ {\bf then} accept $x$"}\\
&\text{Execute $R$ on $\langle M'\rangle$}\\
&\text{{\bf if} $R$ accepts {\bf then} accept {\bf else} reject}\\
\hline
\end{align}$$


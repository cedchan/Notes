### Why Nondeterminism?

There are two main reasons that justify the usage of nondeterministic finite automata:

**Studying models of computation:** 
- NFAs are great for studying computation
- Mathematically well-defined syntax and semantics
- Valid mathematical question: how does construction impact computation power

**Useful concept:**
- Useful in translating regular expressions
- Critical to NP-complete problems

## Definition

>[!definition]
>A **nondeterministic finite automate (NFA)** $M$ consists of:
>- a finite set $Q$ of states
>- a finite alphabet $\Sigma$
>- an initial state $q_0 \in Q$
>- a subset of accepting states $F\subseteq Q$
>- a transition function $\Delta: Q\times\Sigma\rightarrow2^Q$, where $2^Q$ denotes the power set of $Q$

>[!definition]
>**Nondeterministic transition function** $\Delta$ maps a state and a symbol to a set of states: after processing symbol $\sigma$ in state $q$, the next state is chosen from the set $\Delta(\sigma, q)$.
>
>NFA $M$ accepts a string $w$ iff there exists at least one successful execution of $M$ on $w$. 

When there are multiple paths available, how does the machine know which path to take?

One answer is that if only one of the paths can lead to success, we choose that. In actual implementation, we have no way, however, of knowing which path will lead to success, so we need to try all possibilities by maintaining the set of possible states.
## Visualizing NFAs

Because there is more than one path for a given input on an NFA, we must use different ways of representing what happens to an input on NFAs. Primarily we will look at using trees and sets.

>**Example.**
>![](Pasted%20image%2020230912121637.png)
>On input $\text{aabb}$, represented as a tree of possible states:
>![](Pasted%20image%2020230912122102.png)
>$L(M)=\{w\mid \text{second to last symbol of } w \text{ is a}\}$

>**Example.** $\Sigma=\{\text{A, C, G, T}\}$
>![](Pasted%20image%2020230912121727.png)
>Nondeterministic transition function $\Delta$: $Q\times \Sigma \rightarrow 2^Q$.
>
>On input $\text{ACTACCGA}$, represented with set of states after each symbol:
>$$\begin{align}\{q_0\} \stackrel{\mathrm A}{\rightarrow} \{q_0, q_1\} \stackrel{\mathrm C}{\rightarrow} \{q_0, q_2\} \stackrel{\mathrm T}{\rightarrow} \{q_0\} &\stackrel{\mathrm A}{\rightarrow} \{q_0, q_1\} \stackrel{\mathrm C}{\rightarrow} \{q_0, q_2\} \\ &\stackrel{\mathrm C}{\rightarrow} \{q_0, q_3\} \stackrel{\mathrm G}{\rightarrow} \{q_0, q_3\} \stackrel{\mathrm A}{\rightarrow} \{q_0, q_1, q_3\}\end{align}$$
>Input is accepted if the set of possible states at the end contains some accepting state.

## Using NFAs

>**Example.** Draw an NFA that accepts $\{w\mid \text{third last symbol of } w \text{ equals a}\}$
>
>>[!solution]+
>>Recall that a DFA for this language must have 8 states
>>![](Pasted%20image%2020230912123545.png)

>**Example.** Parametric
>For each $k$, let $A^k=\{w\mid k\text{-th symbol from end equals a}\}$. How many states does an NFA accepting $A^k$ need?
>
>$k+1$ states.

### When Not to Use NFAs

>**Example.** Draw an NFA that accepts $A=\{w\mid \mathrm{count}(w, \mathrm a) \text{ is even}\}$
>A DFA for this problem:
>![](Pasted%20image%2020230831125214.png)
>In this case, there isn't a simpler NFA (although this DFA is also an NFA), so our ability to move to multiple states is not helpful

### When to Use NFAs

>**Example.** Draw NFA for $\{w \mid w \text{ contains ``ACC" as a substring}\}$
>![](Pasted%20image%2020230912130209.png)
>In this case, we an NFA is the best choice because we don't know when the substring will begin.

## Determinization (Subset Construction)

Consider $A=\{w\mid \mathrm{count}(w, \mathrm a)=\mathrm{count}(w, \mathrm b)\}$. We know $A$ is not regular—that is, it cannot be solved by a DFA. The question is, can we solve the problem with an NFA? 

As it turns out, we can't. More generally, *any NFA can be represented with a DFA*. NFAs are *not* more "expressive" than DFAs. 

>[!idea]
>We can make any NFA into a DFA. This process is called **determinization** or **subset construction**.

We can represent NFAs as DFAs by having the nodes in our DFA represent sets of states.

>**Example.** 
>![](Pasted%20image%2020230912130217.png)
>DFA:
>![](Pasted%20image%2020230912130637.png)
>All possible subsets of $\{q_0, q_1, q_3, q_4\}$ will suffice to cover all states.

### Formal Procedure

Let $M=(Q, \Sigma, q_0, F, \Delta)$ be an NFA.

**Goal:** To construct a DFA $M'$ such that $M'$ accepts $w$ iff $M$ accepts $w$. (That is, $L(M)=L(M')$.)

- A state of $M'$ is a set of states of $M$: $Q'=2^Q$
	- This means that if $M$ has $k$ states, then $M'$ has $2^k$ states
- The initial state $q'_0$ of $M'$ is $\{q_0\}$
- A state is accepting for $M'$ if it contains an accepting state of $M$: $F'=\{S \mid S\cap F \neq \emptyset\}$
- Transition function of $M'$: $\delta'(S, \sigma)=\bigcup\limits_{q\in S}\Delta(q, \sigma)$

This algorithm allows us to easily convert an NFA into a DFA automatically.

## NFAs with $\varepsilon$-transitions

>[!definition]
>$\varepsilon$ transitions are those that can be taken with no input. 

>**Example.** 
>![](Pasted%20image%2020230914125543.png)
>If we consider an input $\mathrm{aac}$, we'd follow these states: 
>$$q_0\stackrel{\mathrm a}{\rightarrow}q_0\stackrel{\mathrm a}{\rightarrow}q_0\stackrel{\varepsilon}{\rightarrow}q_1\stackrel{\varepsilon}{\rightarrow}q_2\stackrel{\mathrm c}{\rightarrow}q_2$$
>The above NFA will accept strings that have any number of $\mathrm a$'s (including $0$), followed by any number of $\mathrm b$'s and any number of $\mathrm c$'s.

>[!idea]
>$\varepsilon$-NFAs have the following:
>- Transition function: $\Delta: Q\times (\Sigma \cup \{\varepsilon\})\rightarrow 2^Q$
>- Transitions do not increase expressiveness ($\varepsilon$-NFAs can still be represented as DFAs)


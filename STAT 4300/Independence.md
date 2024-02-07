## Definition

>[!definition]
>Events $A$ and $B$ are **independent** if
>$$\Pr(A\cap B)=\Pr(A)\cdot\Pr(B)$$
>
>If $\Pr(A)>0, \Pr(B)>0$, the following are equivalent definitions:
>- $A$ and $B$ are independent
>- $\Pr(A\mid B)=\Pr(A)$
>- $\Pr(B\mid A)=\Pr(B)$

An intuitive but provable result is that if $A$ and $B$ are independent, their complements are as well (as are $A$ and $B^\complement$, etc.).

## Independence of Three Events

>[!definition]
>Events $A, B, C$ are **(mutually) independent** if 
>- $\Pr(A\cap B)=\Pr(A)\cdot\Pr(B)$
>- $\Pr(A\cap C)=\Pr(A)\cdot\Pr(C)$
>- $\Pr(B\cap C)=\Pr(B)\cdot\Pr(C)$
>- $\Pr(A\cap B\cap C)=\Pr(A)\cdot\Pr(B)\cdot\Pr(C)$

The fourth condition is required intuitively because telling us about $B$ and $C$ together should still not tell us about $A$. Specifically, independence implies:
- Pairwise independence
- $A\cap B$ is independent of $C$
- $A^\complement\cap B$ is independent of $C$
- $A\cup B$ is independent of $C$
- etc.

### Union of Events

>[!claim]
>$A, B, C$ being independent $\implies A\cup B$ is independent of $C$

**Proof.** Want to show $\Pr([A\cup B]\cap C)=\Pr(A\cup B)\cdot\Pr(C)$. We use the distributive property of sets: $(A\cup B)\cap C=(A\cap C)\cup(B\cap C)$.
$$\begin{align}
\Pr([A\cap C]\cup [B\cap C])&=\Pr(A\cap C)+\Pr(B\cap C)-\Pr([A\cap C]\cap[B\cap C]) \\
&=\Pr(A\cap C)+\Pr(B\cap C)-\Pr(A\cap B\cap C) \\
&=\Pr(A)\cdot\Pr(C)+\Pr(B)\cdot\Pr(C)-\Pr(A)\cdot\Pr(B)\cdot\Pr(B) \\
&=\Pr(C)\cdot[\Pr(A)+\Pr(B)-\Pr(A)\cdot\Pr(B)] \\
&=\Pr(C)\cdot[\Pr(A)+\Pr(B)-\Pr(A\cap B)] \\
&=\Pr(C)\cdot\Pr(A\cup B)
\end{align}$$
## Conditional Independence

Intuitively, "events $A$ and $B$ are (conditionally) independent, given $E$" means that if we know $E$, knowing about $A$ doesn't tell us more about $B$.

>[!definition]
>Events $A$ and $B$ are **conditionally independent**, given event $E$, if
>$$\Pr(A\cap B\mid E)=\Pr(A\mid E)\cdot\Pr(B\mid E)$$
>
>If $\Pr(A, E)>0, \Pr(B, E)>0$, the following are equivalent:
>- $\Pr(A\mid B,E)=\Pr(A\mid E)$
>- $\Pr(B\mid A,E)=\Pr(B\mid E)$

Note that conditional independence doesn't imply independence, and vice versa.

>**Example.** Suppose you're playing two games of chess online with the same opponent. Your opponent can be either Lisa or Bart, but you don't know which one.
>
>Define the following events:
>- $W_1$: You win game 1
>- $W_2$: You win game 2
>- $L$: Lisa is your opponent
>
>Now assume:
>- $\Pr(L)=0.5$
>- $\Pr(W_1\mid L)=\Pr(W_2\mid L)=0.1$
>- $\Pr(W_1\mid L^\complement=\Pr(W_2\mid L^\complement)=0.9$
>- $W_1$ and $W_2$ are conditionally independent, given $L$
>- $W_1$ and $W_2$ are conditionally independent, given $L^\complement$
>
>Show $\Pr(W_2\mid W_1)\neq\Pr(W_2)$. That is, that conditional independence doesn't imply independence.
>
>>[!solution]-
>>$$\begin{align}
\Pr(W_2)&=\underbrace{\Pr(W_2\mid L)}_{0.1}\cdot\underbrace{\Pr(L)}_{0.5}+\underbrace{\Pr(W_2\mid L^\complement)}_{0.9}\cdot\underbrace{\Pr(L^\complement)}_{0.5} \\
&=0.5 \\
\Pr(W_2\mid W_1)&=\frac{\Pr(W_1\cap W_2)}{\underbrace{\Pr(W_1)}_{0.5}} \\
\Pr(W_1\cap W_2)&=\Pr(W_1\cap W_2\mid L)\cdot\underbrace{\Pr(L)}_{0.5}+\Pr(W_1\cap W_2\mid L^\complement)\cdot\underbrace{\Pr(L^\complement)}_{0.5} \\
&=\frac12\Pr(W_1\mid L)\cdot\Pr(W_2\mid L)+\frac12\Pr(W_1\mid L^\complement)+\Pr(W_2\mid L^\complement) \\
&=0.41 \\
\Pr(W_2\mid W_1)&=\frac{0.41}{0.5}=0.82 \\
&\neq 0.5
\end{align}$$

>**Example.** There's two events that can trigger a fire alarm:
>- $F$: There's a fire in the apartment
>- $M$: Someone's microwaving popcorn
>
>Assume $F$ and $M$ are independent.
>
>Let $A$ be the event that the fire alarm is triggered.
>
>Are $F$ and $M$ conditionally independent, given $A$?
>- $\Pr(F\mid M^\complement, A)=1$
>- $\Pr(F\mid A)$ is presumably less than 1

>[!hint]
>In summary:
>
$$\begin{align}

\end{align}$$
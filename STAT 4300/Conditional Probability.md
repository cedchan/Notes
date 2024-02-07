## Definition

Suppose $A$ and $B$ are events and $\Pr(B)>0$.

>[!definition]
>The **conditional probability** of $A$, given $B$, is $$\Pr(A\mid B)=\frac{\Pr(A\cap B)}{\Pr(B)}$$

Phrases that mean the same thing include:
- the probability of $A$, given $B$,
- the probability of $A$, conditional on $B$

Note that $A\mid B$ is not an event. The idea here is that $\Pr(\cdot)$ is like an overloaded function: we can add a potentially infinite number of additional parameters.

### Conditional Multiplication Rule

Again, suppose $A$ and $B$ are events and $\Pr(B)>0$.

>[!theorem]
>$$\Pr(A\cap B)=\Pr(B)\cdot\Pr(A\mid B)$$

It follows that if $\Pr(A)>0$ as well, we can say that
$$\Pr(A\cap B)=\Pr(B)\cdot\Pr(A\mid B)=\Pr(A)\cdot\Pr(B\mid A)$$
### Multiple Events

The condition can also be multiple events, typically denoted by a comma: $\Pr(A\mid B, C)$. This is equivalent as saying their intersection: $\Pr(A\mid B\cap C)$. This holds in general: $\Pr(A, B, C)=\Pr(A\cap B\cap C)$.

We can extend the multiplication rule to multiple events:

>[!theorem]
>$$\Pr(A, B, C)=\Pr(A)\cdot\Pr(B\mid A)\cdot\Pr(C\mid A, B)$$

**Proof.** 
$$\begin{align}
\Pr(A\cap B\cap C)&=\Pr([A\cap B]\cap C) \\
&=\Pr(A\cap B)\cdot\Pr(C\mid A, B) \\
&=\Pr(A)\cdot\Pr(B\mid A)\cdot\Pr(C\mid A, B)
\end{align}$$

## Bayes's Rule

From the [conditional multiplication rule](Probability%20and%20Counting.md#Conditional%20Probability#Conditional%20Multiplication%20Rule), we can easily find Bayes's Rule:

>[!theorem]
>If $\Pr(A)>0$ and $\Pr(B)>0$,
>$$\Pr(A\mid B)=\frac{\Pr(A)\cdot\Pr(B\mid A)}{\Pr(B)}$$

### Extra Conditioning

>[!theorem]
>If $\Pr(A, E)>0, \Pr(B,E)>0$, $$\Pr(A\mid B,E)=\frac{\Pr(B\mid A,E)\cdot\Pr(A\mid E)}{\Pr(B\mid E)}$$

## Law of Total Probability (LOTP)

The law of total probability is a "divide and conquer" result.

### Simple Case

Let $A$ be an event such that $0<\Pr(A)<1$. This implies that $\Pr(A)>0$ and $\Pr(A^\complement)>0$.

Then, for any event $B$:
$$\Pr(B)=\Pr(B\mid A)\cdot \Pr(A)+\Pr(B\mid A^\complement)\cdot\Pr(A^\complement)$$
**Proof.**
$$\begin{align}
B&=(B\cap A)\cup(B\cap A^\complement)\\
\implies\Pr(B)&=\Pr(B\cap A)+\Pr(B\cap A^\complement) \\
&=\Pr(B\mid A)\cdot\Pr(A)+\Pr(B\mid A^\complement)\cdot\Pr(A^\complement)
\end{align}$$

### General Case

>[!definition]
>$A_1, A_2, \dots, A_n$ are a **partition** of the sample space $S$ iff these events are all pairwise disjoint and their union is $S$. That is,
>$$\forall i, j\in[n], A_i\cap A_j=\emptyset$$ and $$S=\bigcup_{i\in [n]}A_i$$
>
>In other words, $A_1, \dots, A_n$ are mutually exclusive and **collectively exhaustive** (union is $S$).

This allows us to define the general LOTP:

>[!theorem]
>If $\forall i, \Pr(A_i)>0$, then
>$$\Pr(B)=\sum_i\Pr(B\mid A_i)\cdot\Pr(A_i)$$

>**Example.** 1% of all students are infected with Whartonitis. A test for infection results in positive or negative. The test has a false-positive rate of 1% and a false-negative rate of 1%. Suppose we test a random student and the result is positive. What is the probability that the student actually has Whartonitis?
>
>>[!solution]-
>>Translating the assumptions into symbols:
>>- Let $I$ be the event that the student is infected, and $T_+$ be the event they test positive. 
>>- $\Pr(I)=0.01$
>>- $\Pr(T_+\mid I^\complement)=0.01$
>>- $\Pr(T_+^\complement\mid I)=0.01$
>>
>>We want to find $\Pr(I\mid T_+)$.
>>$$\begin{align}
\Pr(I\mid T_+)&=\frac{\Pr(I\cap T_+)}{\Pr(T_+)} \\
&=\frac{\Pr(T_+\mid I)\cdot \Pr(I)}{\Pr(T_+)} \\
\end{align}$$
>>From the assumptions, we can find that $\Pr(T_+\mid I)=0.99$. Thus,
>>$$\begin{align}
\Pr(T_+\mid I)\cdot\Pr(I)&=(0.99)(0.01) \\
\Pr(T_+)&=\Pr(T_+\mid I)\cdot\Pr(I)+\Pr(T_+\mid I^\complement)\cdot\Pr(I^\complement) \\
&=(0.99)(0.01)+(0.01)(0.99) \\
\Pr(I\mid T_+)&=\boxed{\frac12}
\end{align}$$
>>The unintuitive result found here is known as the **base rate fallacy**.

## Conditional Probability Functions

We can show that if $\Pr(\cdot)$ obeys the rules of a non-naive "valid probability function" and $B$ is an event with $\Pr(B)>0$, then $\Pr(\cdot\mid B)$ also obeys the rules.

Why is this useful? It implies that all the properties of probability functions also apply to $\Pr(\cdot\mid B)$. For example, the complement rule holds: $\Pr(A^\complement\mid B)=1-\Pr(A\mid B)$.

### Proof of Validity

>[!theorem]
>Conditional probability functions are [valid probability functions](Probability%20and%20Counting.md#"Non-Naive"%20Probability#).

**Proof.** 
- Assume $\Pr(\cdot)$ obeys the non-naive definition and $B$ is an event with $\Pr(B)>0$.
- Let $g(A)=\Pr(A\mid B)$.

We want to prove that $g(\cdot)$ obeys the non-naive definition. First, we show $0\leq g(A)\leq 1$.
$$\begin{align}
g(A)&=\frac{\Pr(A\cap B)}{\Pr(B)} \\
0&\leq\Pr(A\cap B) \\
\Pr(A\cap B)&\leq \Pr(B) & \text{(since $A\cap B\subseteq B$)}
\end{align}$$
The last two lines give us our result.

Now, we prove that $g(\emptyset)=0$ and $g(S)=1$. 
$$\begin{align}
g(\emptyset)&=\frac{\Pr(\emptyset\cap B)}{\Pr(B)} \\
&=\frac{\Pr(\emptyset)}{\Pr(B)} \\
&=0 \\
g(1)&=\frac{\Pr(A\cap B)}{\Pr(B)} \\
&=\frac{\Pr(B)}{\Pr(B)} \\
&=1
\end{align}$$

Lastly, and taking slightly more work, we show that if $A_1, A_2, \dots$ are disjoint events, then $g(A_1\cup A_2\cup \dots)=g(A_1)+g(A_2)+\dots$.

$$\begin{align}
g(A_1\cup A_2\cup\dots)&=\frac{\Pr([A_1\cup A_2\cup\dots]\cap B)}{\Pr(B)} \\
[A_1\cup A_2\cup \dots]\cap B&=(A_1\cap B)\cup (A_2\cap B)\cup\dots \\
\end{align}$$
The second line is a countable union of disjoint events, and since $\Pr(\cdot)$ obeys countable additivity, we can say 
$$\begin{align}
{\rm LHS}&=\frac{\Pr(A_1\cap B)+\Pr(A_2\cap B)+\dots}{\Pr(B)}
\end{align}$$

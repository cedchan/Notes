## What is Probability?
### Types of Uncertainty 

>[!definition]
>**Aleatory** uncertainty is inherent in the data (e.g., how probable an event is).
>
>**Epistemic** uncertainty comes from a model's confidence.

### Two Schools of Thought

>[!idea]
>In the **Frequentest (objectivist)** view, the probability of Event A is the long-run proportion of replications of an experiment in which Event A occurs. That is, $$\lim_{n\to\infty}\frac{\text{\# of reps w/ Event A}}{\text{\# of reps}}$$
>
>In the **Bayesian (subjectivist)** view, probability is a subjective degree of belief on a scale from 0 to 100%. In this view, beliefs can be updated when we get new information.

### Experiments

>[!definition]
>In probability theory, an **experiment** is a procedure whose result may be uncertain until after the procedure is performed.
>
>Experiments have a set of **possible outcome**. When they finish, there's a unique **actual outcome**.

### Sample Space

>[!definition]
>The **sample space** $S$ (or $\Omega$) of an experiment is the set of possible outcomes.
>
>An **event** $A$ is a subset of the sample space $S$. We say that $A$ **occurs** if the actual outcome is an element of $A$. 

Note that $\emptyset$ also satisfies the definition of an event. But it's impossible for none of the possible outcomes to occur, so the probability of the empty set event must be 0. Similarly. The sample space itself is an event with probability 1.

### Defining Probability

>[!definition]
>Under the "naive" assumptions that all outcomes are equally likely and that the sample space $S$ is finite (a corollary of the first assumption), the probability of an event $A\subseteq S$ is just
>$$\Pr\nolimits_{\rm naive}(A)=\frac{|A|}{|S|}$$

Some implications of this definition include:
- $\Pr\nolimits_{\rm naive}(A)\in[0,1]$
- Probability of the complement $A^\complement$ is $1-\Pr\nolimits_{\rm naive}(A)$

## Set Theory Review

### DeMorgan's Laws

>[!theorem]
>
>$$(A\cup B)^\complement=A^\complement\cap B^\complement$$
>And similarly for intersections
>$$(A\cap B)^\complement=A^\complement\cup B^\complement$$

**Proof.** 
$$\begin{align}
x\in(A\cup B)^\complement&\iff x\notin(A\cup B) \\
&\iff\lnot(x\in A \lor x\in B) \\
&\iff x\notin A \land x\notin B \\
&\iff x\in A^\complement \land x\in B^\complement \\
&\iff x \in (A^\complement \cap B^\complement)
\end{align}$$
And for the second law,
$$\begin{align}
(A^\complement\cup B^\complement)^\complement&=(A^\complement)^\complement\cap(B^\complement)^\complement \\
&=A\cap B \\
A^\complement \cup B^\complement&=(A\cap B)^\complement & \text{(taking complement of both sides)}
\end{align}$$

## Combinatorics Review

### Birthday Paradox

**Problem:** Suppose we have 23 people in a room. What's the probability that two or more of them have the same birthday?

**Assumptions:**
- Leap years don't exist
- All 365 days (no Feb. 29) are equally likely
- Birthdays are independent

$A^\complement$ is the set of possible outcomes in which everyone has a different birthday. 

## Combinations

How many ways to choose $k$ out of $n$ items, when order doesn't matter?

$$\binom{n}{k}=\frac{n(n-1)\cdots(n-k+1)}{k!}=\frac{n!}{k!(n-k)!}$$

## "Non-Naive" Probability

What if our previous [assumptions](Probability%20and%20Counting.md#What%20is%20Probability?#Defining%20Probability) about probability don't hold? We define some concepts to resolve this.

>[!definition]
>A **probability space** consists of a sample space $S$, and a **probability function** $P$ that has the following:
>- Input: Any event $A\subseteq P$
>- Output: A real number $\Pr(A)\in[0,1]$
>  
> In addition, $P$ must satisfy the following axioms:
> - $\Pr(\emptyset)=0$ and $\Pr(S)=1$
> - If events $A_1, A_2, \dots, A_3$ are disjoint, then
> $$\Pr\left(\bigcup_{j=1}^\infty A_j\right)=\sum_{j=1}^\infty\Pr(A_j)$$

The second axiom is known as **countable additivity**. To motivate this axiom, we discuss a weaker rule called **finite additivity**:
$$\Pr\left(\bigcup_{j=1}^n A_j\right)=\sum_{j=1}^n\Pr(A_j)$$
Countable additivity implied finite additivity.

### Properties of Probability

The **complement rule** holds from the naive definition.

>[!theorem]
>$$\Pr(A^\complement)=1-\Pr(A)$$

**Proof.** $A$ and $A^\complement$ are disjoint events by definition. Thus, by the second axiom, $\Pr(A\cup A^\complement)=\Pr(A)+\Pr(A^\complement)$. We know $\Pr(A\cup A^\complement)=P(S)=1$. With some algebra, we get our result.

>[!theorem]
>$$A\subseteq B\implies \Pr(A)\leq\Pr(B)$$

>[!theorem] 
>The **Principle of Inclusion Exclusion (PIE)** is
>$$\Pr(A\cup B)=\Pr(A)+\Pr(B)-\Pr(A\cap B)$$


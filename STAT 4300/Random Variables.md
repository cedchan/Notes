## Definitions

>[!definition]
>Informally, a random variable is a **numerical** summary of the outcome of an experiment.
>
>More precisely, given an experiment with sample space $S$, a **random variable** is a function that maps each possible outcome $s\in S$ to a real number.

Thus, we can define events involving random variables as sets such as $$\{s\in S\mid Y(s)\geq 4\}$$
Customarily this is shortened to notation like $$Y\geq 4$$
A random variable is **discrete** if there exists a countable set of values $V$ such that $$\Pr(X\in V)=1$$
That is, that 
$$\Pr(\{s\in S\mid X(s)\in V\})$$

>[!note]
>A set is **countably infinite** if there exists a bijection (one-to-one correspondence) from the set to $\mathbb N$. 

>[!definition]
>If $X$ is a discrete random variable, then the countable set of values $x$ such that $\Pr(X=x)>0$ is called the **support** of $X$.

### Indicator Random Variables

>[!definition]
>For an event $A$, the **indicator random variable** $I_A$ equals 1 if $A$ occurs and is 0 otherwise.

Then, if $0<\Pr(A)<1$, $I_A\sim{\rm Bern}(p)$ where $p=\Pr(A)$. From there, it's simple to show that $\mathbb E(I_A)=p$, which combined with [linearity of expectation](Expectation.md#Linearity%20of%20Expectation), can be useful for proving the expectation of different distributions. This is known as the **fundamental bridge**.

>**Example.**  Suppose we have a group of $n$ people. Assume the following:
>- Feb. 29 is not a possible birthday
>- For each person, the 365 possible birthdays are equally likely
>- The $n$ birthdays are independent
>
>Let $X$ be the number of distinct birthdays among the $n$ people. What is $\mathbb E(X)$?
>
>>[!solution]-
>>We solve this using (1) the fundamental bridge, (2) linearity of expectation, and (3) the complement rule.
>>
>>Let $X_i, i\in[0..365]$ be an indicator random variable that is 1 if at least one person's birthday is day $i$ and 0 otherwise. Clearly, $X=\sum_{i}X_i$. 
>>
>>Then, we use linearity of expectation to solve:$$\begin{align}
\mathbb E(X_i)&=\Pr(X_i=1) \\
&=1-\left(\frac{364}{365}\right)^n \\
\mathbb E(X)&=\mathbb E\left(\sum_{i=1}^{365}X_i\right) \\
&=\sum_{i=1}^{365}\mathbb E(X_i) \\
&=\sum_{i=1}^{365}\left[1-\left(\frac{364}{365}\right)^n\right] \\
&=365\left[1-\left(\frac{364}{365}\right)^n\right]
\end{align}$$

## Probability Mass Functions

>[!definition]
>A **probability mass function (PMF)** of a discrete random variable $X$ is the function $p_X$ given by $p_X(u)=\Pr(X=u)$. 

The key difference between the PMF and distribution is that the PMF takes in a number, while the distribution takes in a set of numbers. 

## Distributions

>[!definition]
>The **distribution** of a random variable $X$ specifies the probabilities of all possible sets of values for $X$.
>
>More formally, it's a function that takes in a set of values and outputs the probability that $X$ lies in that set. That is, $f:\mathcal P(\mathbb R)\mapsto[0,1]$. So for $V\subseteq \mathbb R$,$$f(V)=\Pr(X\in V)$$

>**Example.** Flip a coin 5 times.
>- $X$: No. heads
>- $Y$: No. tails
>- $\Pr(X\in V)=\Pr(Y\in V)$ for any set of values $V\subseteq[0..5]$
>
>Though $X$ and $Y$ have the same distribution, they'll never be equal (since there's an odd total and $X+Y=5$).

## Cumulative Distribution Functions

Another way to uniquely specify the distribution of a random variable is the cumulative distribution function (CDF). Note that while PMFs are only defined for discrete random variables, CDFs are defined for all random variables.

>[!definition]
>The **cumulative distribution function (CDF)** of a random variable $X$ is a function $F_X$ given by  $$F_X(u)=\Pr(X\leq u)$$ 
>
>Note that the subscript is sometimes dropped and we just write $F$.

All CDFs $F$ obey the following:
- Non-decreasing: $u_1\leq u_2\implies F(u_1)\leq F(u_2)$
- Right-continuous: $\forall a\in \mathbb R, \lim_{u\downarrow a}F(u)=F(a)$
- $\lim_{u\to -\infty}F(u)=0$
- $\lim_{u\to\infty}F(u)=1$

## Functions of Random Variables

Recall that a random variable $X$ is a function from the sample space $S$ to $\mathbb R$. 

>[!definition]
>Given
>- $S$, the sample space for an experiment
>- $X$, a random variable
>- $g$, a function $\mathbb R\mapsto\mathbb R$
>
>$g(X)$ is defined to be the random variable that maps each possible outcome $s\in S$ to the real number $g(X(s))$. That is, $g(X)=g\circ X$.
>
>Similarly, we can define a function that maps multiple random variables to a real number, such as $h(X, Y)=h(X(s), Y(s))$.

>**Examples.**
>- $X^2$
>- $2X$
>- $g(X)$
>- $X+Y$

>**Example.** Roll a 6-sided die once.
>- Let $X$ be the number shown
>- Let $Y=2X$
>- $\Pr(X=u)=\frac16$ for $u\in[1..6]$
>- Doubling the PMF would suggest $\Pr(Y=u)=\frac13$, for $u\in[1..6]$.
>
>This is **incorrect**. We can see this in a couple of ways. First, the support is incorrect. We would expect that it be $\{2, 4,\dots,12\}$. We can also observe that the sum of $\Pr(Y=u)$ for all $u$ does not add up to 1.

## Independence

>[!definition]
>Random variables $X$ and $Y$ are **independent** if $\forall x,y\in\mathbb R$
>$$\Pr(X\leq x, Y\leq y)=\Pr(X\leq x)\cdot\Pr(Y\leq y)$$

Intuitively, "$X$ and $Y$ are independent" means that knowing the value of $X$ doesn't tell us about the value of $Y$. This implies that if $X,Y$ are independent, $X>0$ and $Y>0$ are also independent events, $X>2, Y<4$ are independent, etc.

>[!theorem]
>If $X$ and $Y$ are independent, then any function of $X$ is independent of any function of $Y$.

For example,$$X\perp Y\implies X^2\perp Y^2$$
However, it's important to note that 
$$X^2\perp Y^2\centernot\implies X\perp Y$$
We illustrate this as follows. Consider 
$$\begin{align}
X&=\begin{cases}1&{\rm Heads} \\
-1&{\rm Tails}\end{cases}\\
Y&=X+1 \\
&=\begin{cases}
2 & \text{if H}\\
0 & \text{if T}
\end{cases}
\end{align}$$
Clearly, $X\not\perp Y$ (in fact, $X$ entirely determines $Y$). Then, if we square both, we have
$$\begin{align}
X^2&=1\\
Y^2&=\begin{cases}
4 & \text{if H} \\
0 & \text{if T}
\end{cases}
\end{align}$$
Since, $X^2$ is always $1$, $X^2\perp Y^2$. This is because the squaring function is not one-to-one.

### Independence of Discrete Random Variables

>[!theorem]
>If $X$ and $Y$ are discrete random variables, the following statements are equivalent:
>1. $X$ and $Y$ are independent.
>2. $\Pr(X=x,Y=y)=\Pr(X=x)\cdot\Pr(Y=y)$ for all $x$ in the support of $X$ and all $y$ in the support of $Y$. 
>3. $\Pr(Y=y\mid X=x)=\Pr(Y=y)$ for all $x$ in the support of $X$ and all $y$ in the support of $Y$.
>4. $\Pr(X=x\mid Y=y)=\Pr(X=x)$ for all $x$ in the support of $X$ and all $y$ in the support of $Y$.

### Independence of Many Random Variables

(Mutual) independence implies pairwise independence, but pairwise independence doesn't imply (mutual) independence.

>[!theorem]
>Random variables $X_1,\dots,X_n$ are **mutually independent** if
>$$\Pr\left(\bigcap_{i=1}^nX_i\leq x_i\right)=\prod_{i=1}^n\Pr(X_i\leq x_i)$$
>for all $x_i\in\mathbb R$.

## Independent and Identically Distributed

>[!theorem]
>Random variables $X_1,\dots,X_n$ are **independent and identically distributed (i.i.d.)** if
>- $X_1, \dots, X_n$ are independent, and
>- $X_1, \dots, X_n$ all have the same distribution.

This is equivalent to saying they all have the same CDF, since CDFs uniquely identify distributions. For discrete random variables, it's also equivalent to saying they have the same PMF.

>**Example.** Flip a coin $n$ times. Let $X_i=1$ if the $i$-th flip is heads, and $0$ otherwise. $X_1,\dots,X_n$ are i.i.d.


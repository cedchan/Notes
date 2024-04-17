## Definition

Intuitively, the expectation of a discrete random variable $X$ is just a weighted average of the possible values of $X$. For example, if $X$ is the number shown on a 6-sided die, since all values are equal, $\mathbb E(X)=(1+2+3+4+5+6)/6=3.5$. 

>[!definition]
>If $X$ is a discrete random variable with $n$ possible values $x_1,\dots,x_n$, then the **expectation** of $X$ is
>$$\mathbb E(X)=\sum_{j=1}^nx_j\Pr(X=x_j)$$
>If $X$ has a countably infinite set of possible values $x_1,x_2,\dots$, then its expectation is
>$$\mathbb E(X)=\sum_{j=1}^\infty x_j\Pr(X=x_j)$$
>if the infinite series converges absolutely. Otherwise $\mathbb E(X)$ is undefined.

The series $\sum_{j=1}^\infty x_j\Pr(X=x_j)$ **converges absolutely** if the series of absolute values $$\sum_{j=1}^\infty |x_j|\Pr(X=x_j)$$converges to a finite limit. Absolute convergence guarantees that the expectation is finite and that its value won't change if we reorder the terms. 

>[!hint]
>$$X\sim{\rm Bernoilli(p)}\implies \mathbb E(X)=p$$

## Linearity of Expectation

>[!theorem]
>For any random variables $X$ and $Y$, we have
>- $\mathbb E(X+Y)=\mathbb E(X)+\mathbb E(Y)$
>- $\mathbb E(cX)=c\mathbb E(X)$ for any constant $c$

An easy corollary to show is that
$$\mathbb E(X+c)=\mathbb E(X) + c$$ for any constant $c$. 

>**Example.** Binomial expectation
>
>We know that the [PMF of the Binomial Distribution](Random%20Variables.md#Distributions#Bernoulli%20Distribution#PMF%20of%20the%20Binomial%20Distribution) is $$\Pr(X=k)=\binom nkp^k(1-p)^{n-k}$$
>so we could calculate expectation as $$\mathbb E(X)=k\binom nkp^k(1-p)^{n-k}$$
>But this requires many combinatorial tricks and is overall a painful process, so we can instead use linearity of expectation. 
>
>Observe that $$X=I_1+\dots+I_n$$
>where $I_j$ is an indicator random variable that is 1 if the $j$-th trial is true and 0 otherwise. Then, by linearity,
>$$\mathbb E(X)=\sum_{j=1}^n\mathbb E(I_j)$$
>Recalling that since each $I_j\sim{\rm Bern}(p)$, $\mathbb E(I_j)=p$, so $\mathbb E(X)=np$. 

>**Example.** Hypergeometric expectation. 
>
>Suppose $X\sim{\rm HGeom}(w,b,n)$. In our story, we let $X$ be the number of wine drinkers in a sample of size $n$ among $w$ wine drinkers and $b$ beer drinkers. Then,$$X=I_1+\dots+I_n$$where $I_j=1$ if the $j$-th sample member is a wine drinker and 0 otherwise. Then, each $I_j$ has $\Pr(I_j=1)=\frac{w}{w+b}$ since each person in the population is equally likely to be chosen. 
>
>By linearity, $\mathbb E(X)=\frac{nw}{w+b}$

## Expectation Via Survival Function

The [fundamental bridge](Random%20Variables.md#Definitions#Indicator%20Random%20Variables) is a version of the "Darth Vader rule."

>[!theorem]
>Let $X$ be a random variable in $\mathbb N$. Then,
>$$\mathbb E(X)=\sum_{n=1}^\infty\Pr(X\geq n)$$

## Law of the Unconscious Statistician (LOTUS)

Suppose $X$ is a discrete random variable and $Y=g(X)$, where $g:\mathbb R\mapsto \mathbb R$. By definition,
$$\mathbb E(g(X))=\mathbb E(Y)=\sum_yy\Pr(Y=y)$$
This works, but we'd have to calculate the PMF of $Y$ in order to solve this equation. LOTUS provides another method:

>[!theorem]
>$$\mathbb E(g(X))=\sum_xg(x)\Pr(X=x)$$

## Variance

>[!definition]
>The **variance** of a random variable $X$ is 
>$${\rm Var}(X)=\mathbb E([X-\mathbb E(X)]^2)$$

An equivalent formula, which is often misinterpreted as the definition of variance, is 
$${\rm Var}(X)=\mathbb E(X^2)-[\mathbb E(X)]^2$$
**Proof.**
$$\begin{align}
{\rm Var}(X)&=\mathbb([X-\mathbb E(X)]^2) \\
&=\mathbb E([X-c]^2)\\
&=\mathbb E(X^2-2cX+c^2) \\
&=\mathbb E(X^2)-2c\cdot\mathbb E(X)+c^2 \\
&=\mathbb E(X^2)-c^2 \\
&=\mathbb E(X^2-[\mathbb E(X)]^2
\end{align}$$

>**Example.** Bernoulli variance
>
>Note that $\mathbb E[X]=p$. Further note that $X^2=X$. 
>$$\begin{align}
{\rm Var}(X)&=\mathbb E[X^2]-\mathbb E[X]^2 \\
&=p-p^2\\
&=p(1-p)
\end{align}$$

>[!definition]
>The **standard deviation** of $X$ is 
>$${\rm SD}(X)=\sqrt{{\rm Var}(X)}$$

In applications, the standard deviation is typically easier to interpret than the variance. 

### Properties
1. ${\rm Var}(X)\ge0$. In fact, ${\rm Var}(X)>0$ unless $X$ is constant
2. ${\rm Var}(X+c)={\rm Var}(X)$
3. ${\rm Var}(cX)=c^2{\rm Var}(X)$
4. $X\perp Y\implies{\rm Var}(X+Y)={\rm Var}(X)+{\rm Var}(Y)$

### Variance of a Sum

Using [covariance](Joint%20Distributions.md#Covariance), we can create a general formula for the variance of the sum of two random variables.

>[!theorem]
>$$\Var(X+Y)=\Var(X)+\Var(Y)+2\Cov(X,Y)$$

**Proof.**
$$\begin{align}
\Var(X+Y)&=\E((X+Y-\E[X+Y])^2) \\
&=\E\paren{\paren{[X_\E(X)]+[Y-\E(Y)]}^2} \\
&=\underbrace{\E([X=\E(X)]^2)}_{\Var(X)}+\underbrace{\E([Y-\E(Y)]^2)}_{\Var(Y)}+2\underbrace{\E([X-\E(X)][Y-\E(Y)])}_{\Cov(X,Y)} \\
&\qed
\end{align}$$

**Corrollaries:**
- $\Var(X-Y)=\Var(X)+\Var(Y)-2\Cov(X,Y)$
- $X\perp Y\implies\Var(X+Y)=\Var(X)+\Var(Y)$
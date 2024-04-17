## Motivation

We've learned how to use PMFs, PDFs, and CDFs to find probabilities involving one random variable, but what about events involving two or more random variables. For example, if $H$ is tomorrow's high temperature and $L$ is tomorrow's low temperature, what is $\Pr(H>65,L<55)$?

We might also want to summarize relationships between two or more random variables.

Joint distributions allow us to do these things. 

### Discrete Joint Distributions

Joint distributions for discrete random variables serve as a building block for the continuous case. For discrete $X$ and $Y$, we'll define three types of PMFs.
- Joint PMF of $X$ and $Y$
- Marginal PMF of $X$ and $Y$
- Conditional PMF of $Y$, given $X=x$

Note that in the below definitions, we use two discrete random variables $X$ and $Y$. These definitions can easily be generalized to three or more random variables, though we don't show those formulas.

>[!definition]
>The **joint PMF** of discrete random variables $X, Y$ is the function $p_{X,Y}$ given by $$p_{X,Y}(x,y)=\Pr(X=x,Y=y)$$

>[!definition]
>The **marginal PMF** of $X$ for discrete random variables $X, Y$ is the function $p_X$ given by
>$$p_X(x)=\Pr(X=x)=\sum_{y\in{\rm support}(Y)}\Pr(X=x,Y=y)$$

**Properties:**
- This is the normal PMF of $X$
- We can derive the marginal PMFs of $X$ and $Y$ from their joint PMF, but not vice versa

>[!definition]
>For discrete random variables $X$ and $Y$, for each value $x$ in the support of $X$, the **conditional PMF** of $Y$, given $X=x$ is
>$$\Pr(Y=y\mid X=x)\frac{\Pr(X=x,Y=y)}{\Pr(X=x)}$$

**Properties:**
- The conditional PMF is viewed as a function of $y$
- This equation is simply the definition of conditional probability, but looking at $\Pr(Y=y)$ while holding some $x$ constant

## Joint CDF and PDF

The probability of an event involving $H$ and $L$ will be the volume under the the joint PDF. The volume is the double integral of the joint PDF over the relevant region.

>[!definition]
>The **joint CDF** of random variables $X$ and $Y$ is the function $F_{X,Y}$ given by $$F_{X,Y}(x,y)=\Pr(X\le x, Y\le y)$$
>Sometimes, the subscripts are dropped.

Then, similar to with the single-variable case, we can differentiate to get the PDF.

>[!definition]
>The **joint PDF** of continuous random variables $X$ and $Y$ is the derivative of their joint CDF with respect to $x$ and $y$:
>$$f_{X,Y}(x,y)=\frac{\partial^2}{\partial x\partial y}F_{X,Y}(x,y)$$

The properties of ordinary PDFs hold:
- Nonnegative: $f_{X,Y}(x,y)\ge0$
- Integrates to 1: $$\int_{-\infty}^\infty\int_{-\infty}^\infty f_{X,Y}(x,y)dxdy=1$$

### Finding Probabilities with Joint PDFs

We can use the joint PDF to find the probability of any region in the $XY$-plane:
- Rectangular regions: $$\Pr(-1\le X, 3\le Y\le4)=\int_{-1}^\infty\int_3^4f_{X,Y}(x,y)dxdy$$
	Note that this also allows us to get probabilities for single variables:
	$$\Pr(-1\le X\le 2)=\int_{-1}^2\int_{-\infty}^\infty f_{X,Y}(x,y)dxdy$$
- More generally, for any set $A\subseteq\mathbb R^2$,$$\Pr((X,Y)\in A)=\iint_Af_{X,Y}(x,y)dxdy$$

### Marginal PDF

>[!definition]
>The **marginal PDF** of $X$ is defined by integrating the joint PDF over all possible values of $Y$.
>$$f_X(x)=\int_{-\infty}^\infty f_{X,Y}(x,y)dy$$

### Conditional PDF

>[!definition]
>The **conditional PDF** of $Y$, given $X=x$ is
>$$f_{Y\mid X}(y\mid x)=\frac{f_{X,Y}(x,y)}{f_X(x)}$$
>again viewed as a function of $y$.

How do we condition on $X=x$ when $\Pr(X=x)=0$? The idea is to condition on $X\in[x - \frac{\Delta x}2,x+\frac{\Delta x}2]$, taking the limit as $\Delta x\to 0$. Then, when $\Delta x,\Delta y$ are small enough,
$$\Pr\paren{Y\in\middle[y-\frac{\Delta y}2,y+\frac{\Delta y}2\middle]\;\middle|\;X\in\middle[x-\frac{\Delta x}2,x+\frac{\Delta x}2\middle]}\approx f_{Y\mid X}(y\mid x)\cdot \Delta y$$

## Independence of Continuous Random Variables

>[!definition]
>Random variables $X$ and $Y$ are **independent** if $\forall x,y\in\mathbb R$,
>$$\Pr(X\le x, Y\le y)=\Pr(X\le x)\cdot\Pr(Y\le y)$$

Rewritten in terms of CDFs:
$$\Pr(X\le x,Y\le y)=F_X(x)\cdot F_Y(y)$$

>[!theorem]
>If $X$ and $Y$ are continuous with the joint PDF $f_{X,Y}$, then the following are equivalent:
>1. $X$ and $Y$ are independent
>2. $f_{X,Y}(x,y)=f_X(x)\cdot f_Y(y)$ for all $x,y\in\mathbb R$
>3. $f_{Y\mid X}(y\mid x)=f_Y(y)$ for all $y$ and all $x$ such that $f_X(x)>0$
>4. $f_{X\mid Y}(x\mid y)=f_X(y)$ for all $x$ and all $y$ such that $f_Y(y)>0$

### Factoring and Independence

>[!theorem]
>If the joint PDF of $X$ and $Y$ can be factored as $$f_{X,Y}(x,y)=g(x)\cdot h(y)$$
>for all $x,y\in\mathbb R$ and where $g$ and $h$ are nonnegative functions, then $X$ and $Y$ are independent.

This result can be useful when we don't know if $g$ and $h$ are the marginal PDFs of $X$ and $Y$. If $f_{X,Y}$ factors in this way, all we need to do to get the marginal PDFs is to rescale $g$ and $h$ so they both integrate to 1. 

>**Example.** Suppose my laptop has lifetime $T_1\sim\Expo(\lambda_1)$ and my phone has lifetime $T_2\sim\Expo(\lambda_2)$, where $T_1\perp T_2$. What is the probability that my laptop fails before my phone?
>
>>[!solution]-
>>We want to find $\Pr((T_1,T_2)\in A)$, where $A=\{(t_1,t_2)\in\mathbb R^2\mid 0<t_1<t_2\}$. That is,
>>$$\Pr((T_1,T_2)\in A)=\iint_Af_{T_1,T_2}(t_1,t_2)dt_1dt_2$$
>>Since $T_1\perp T_2$, $f_{T_1,T_2}(t_1,t_2)=f_{T_1}(t_1)\cdot f_{T_2}(y)$, so the above becomes
>>$$\iint_Af_{T_1}(t_1)\cdot f_{T_2}(t_2)dt_1dt_2=\iint_A\lambda_1e^{-\lambda_1t_1}\lambda_2e^{\lambda_2t_2}dt_1dt_2$$
>>To set up the bounds of integration over $A$, we can view this as nested loops. There are two options:
>>1. For $t_2=0\to \infty$
>>	1. For $t_1=0\to t_2$
>>2. For $t_1=0\to\infty$
>>	1. For $t_2=t_1\to\infty$
>>Using the first, we get
>>$$\int_0^\infty\int_0^{t_2}\lambda_1e^{-\lambda_1t_1}\lambda_2e^{\lambda_2t_2}dt_1dt_2$$
>>Evaluating the inner integral first, we get
>>$$\int_0^{t_2}\lambda_1e^{-\lambda_1t_1}\lambda_2e^{\lambda_2t_2}dt_1=\lambda_2e^{-\lambda_2t_2}\int_0^{t_2}\lambda_1e^{-\lambda_1t_1}dt_1$$
>>Note that the expression we are now integrating is the PDF of the exponential distribution with parameter $\lambda_1$, so it must integrate to the CDF at $t_2$. That is, it must be $F_{T_1}(t_2)=1-e^{-\lambda_1t_2}$. This gives the final expression
>>$$\lambda_2e^{-\lambda_2t_2}(1-e^{-\lambda_1t_2})$$
>>Now plugging this result into the outer integral, we have
>>$$\int_0^\infty\lambda_2e^{-\lambda_2t_2}(1-e^{-\lambda_1t_2})dt_2=\int_0^\infty\lambda_2e^{-\lambda_2t_2}dt_2-\int_0^\infty\lambda_2e^{-(\lambda_1+\lambda_2)t_2}dt_2$$
>>The first integral is the integral under the entire exponential distribution with parameter $\lambda_2$, so it must evaluate to 1. Similarly, we can manipulate the second integral to be $$\frac{\lambda_2}{\lambda_1+\lambda_2}\int_0^\infty(\lambda_1+\lambda_2)e^{-(\lambda_1+\lambda_2)t_2}dt$$
>>This too (at least the integral part) integrates a PDF over its whole support, so it must integrate to 1. This gives our final answer
>>$$\frac{\lambda_2}{\lambda_1+\lambda_2}$$

## 2D Law of the Unconscious Statistician (LOTUS)

>[!theorem]
>Let $g$ be a function from $\mathbb R^2$ to $\mathbb R$.
>
>If $X$ and $Y$ are discrete r.v.s, then $$\E(g(X,Y))=\sum_x\sum_yg(x,y)\Pr(X=x,Y=y)$$
>where the sum is taken over all possible values of $X$ and $Y$.
>
>If $X$ and $Y$ are continuous with joint PDF $f_{X,Y}$, then
>$$\E(g(X,Y))=\int_{-\infty}^\infty\int_{-\infty}^\infty g(x,y)f_{X,Y}(x,y)dxdy$$

## Expectation of Independent Variables

>[!theorem]
>If $X$ and $Y$ are independent r.v.s, then $$\E(XY)=\E(X)\E(Y)$$

**Proof.** By independence, $f_{X,Y}(x,y)=f_X(x)f_Y(y)$. By [2D LOTUS](Joint%20Distributions.md#2D%20Law%20of%20the%20Unconscious%20Statistician%20(LOTUS)), 
$$\E(XY)=\int_{-\infty}^\infty\int_{-\infty}^\infty xyf_X(x)f_Y(y)dxdy$$
The inside integral equals
$$yf_Y(y)\int_{-\infty}^\infty xf_X(x)dx$$
Clearly, the inner equation is just the definition of the expectation of $X$. This gives
$$\E(XY)=\int_{-\infty}^\infty yf_Y(y)\E(X)dy$$
Bringing out the constant, we have similarly the expectation of $Y$.
$$\E(XY)=\E(X)\int_{-\infty}^\infty yf_Y(y)dy=\E(X)\E(Y)\qed$$
>[!note]
>Importantly, the converse of this theorem does not necessarily hold. That is,
>$$X\perp Y\centernot\impliedby \E(XY)=\E(X)\E(Y)$$


## Covariance

The covariance between two random variables $X,Y$ are one possible summary of their relationship. Positive covariance means that when $X$ goes up $Y$ goes up, and negative covariance indicates the opposite—that $Y$ goes down.

In applied statistics, covariance plays the "behind the scene" role, serving as the baseline of **correlation**.

>[!definition]
>The **covariance** between random variables $X$ and $Y$ is defined as $$\Cov(X,Y)=\E([X-\E(X)][Y-\E(Y)]$$

### Properties

- $X\perp Y\implies \Cov(X,Y)=0$
- $\Cov(X,Y)=\Cov(Y,X)$
- $\Cov(X,c)=0$

>[!theorem]
>A handy equivalent formula is
>$$\Cov(X,Y)=\E(XY)-\E(X)\E(Y)$$

**Proof.** Let $\mu_X=\E(X), \mu_Y=\E(Y)$. Then,
$$\begin{align}
\Cov(X,Y)&=\E([X-\mu_X])[Y-\mu_Y]\\
&=\E(XY)-\mu_X\E(Y)-\mu_Y\E(X)+\mu_X\mu_Y \\
&=\E(XY)-\E(X)\E(Y) \\
&\qed
\end{align}$$
>[!theorem]
>$$\Var(X)=\Cov(X,X)$$

**Proof.**
$$\begin{align}
\Cov(X,Y) &=\E(XX)-\E(X)\E(X) \\
&=\E(X^2)-\E(X)^2 \\
&=\Var(X)\\
&\qed
\end{align}$$
>[!theorem] Bilinearity of Covariance
>1. $\Cov(aX,Y)=a\Cov(X,Y)$ for any constant $a$, and
>2. $\Cov(X+Y,Z)=\Cov(X,Z)+\Cov(Y,Z)$
>
>A corollary is that $\Cov(X+Y,Z+W)=\Cov(X,Z)+\Cov(X,W)+\Cov(Y,Z)+\Cov(Y,W)$.

### Correlation

>[!definition]
>The **correlation** between random variables $X$ and $Y$ is
>$$\Corr(X,Y)=\frac{\Cov(X,Y)}{\sqrt{\Var(X)\cdot\Var(Y)}}=\frac{\Cov(X,Y)}{\SD(X)\cdot\SD(Y)}$$
>if $\Var(X)>0,\Var(Y)>0$.

One of the benefits of correlation is that it is independent of units of measurement. Specifically, location-scale transformations have no effect on correlations:
$$\Corr(aX+b,cY+d)=\Corr(X,Y)$$ if $a>0,c>0$.

Another property of correlation is that it lies in the range $[-1, 1]$, where perfect correlation (i.e., $|\Corr(X,Y)|=1$) implies a perfect linear relationship.




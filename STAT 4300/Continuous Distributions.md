## Uniform Distribution

Intuitively, a random variable $U$ has the uniform distribution on $(a, b)$ if $U$ is a "completely random" number between $a$ and $b$. More precisely, that means that the PDF of $U$ is constant over the interval $(a, b)$, which is also its support.

>[!definition]
>A continuous random variable $U$ has the **Uniform distribution** on $(a, b)$ if its PDF is
>$$f(x)=\begin{cases}\displaystyle\frac1{b-a} & \text{if }a<x<b \\ 0 & \text{o.w.}\end{cases}$$
>We write $U\sim{\rm Unif}(a,b)$.
>
>The **standard uniform distribution** is ${\rm Unif}(0,1)$.

We can easily find that the CDF is
$$F(x)=\begin{cases}0& x<a \\
\displaystyle\frac{x-a}{b-a}&a<x<b\\
1 & x>b
\end{cases}$$

For the standard uniform distribution, it's even simpler:
- $f(x)=1$ for $0<x<1$ and $0$ otherwise
- $F(x)=x$ for $0<x<1$ and $0$ or $1$ otherwise

### Expectation and Variance

>[!summary]
>$$\begin{align}
>\mathbb E(w)&=\frac{a+b}2\\
>{\rm Var}(w)&=\frac{(b-a)^2}{12}
>\end{align}$$

With simple integration, we find for $U\sim{\rm Unif}(0,1)$ that $\mathbb E(U)=\frac{1}2$. Using LOTUS we find ${\rm Var}(U)=\frac1{12}$.

We could use integrals and the definition of expectation to find the mean and variance in the general case, but it's easier to use a location-scale transformation. 

If $U\sim{\rm Unif}(0,1)$ then let $W=a+(b-a)U$. We show that $W\sim{\rm Unif}(a,b)$ by showing that it has the correct CDF.
$$\begin{align}
F_W(w)&=\Pr(W\leq w) \\
&=\Pr(a+(b-a)U\leq w) \\
&=P\left(U\leq\frac{w-a}{b-a}\right) \\
&=F_U\left(\frac{w-a}{b-a}\right)\\
F_W(w)&=\begin{cases}
0 & w\leq a \\
\displaystyle\frac{w-a}{b-a}&a<w<b\\
1 & w\geq b
\end{cases}\\
&\tag*{$\square$}
\end{align}$$

Then, using linearity of expectation, we can say 
$$\mathbb E(W)=a+(b-a)\mathbb E(U)$$
We know $\mathbb E(U)=\frac12$, so
$$\mathbb E(W)=\frac{a+b}2$$
Similarly for variance,
$${\rm Var}(W)=(b-a)^2{\rm Var}(U)=\frac{(b-a)^2}{12}$$

### Universality of the Uniform

We can start with $U\sim{\rm Unif}(0,1)$ and transform $U$ into a random variable $X$ with any continuous distribution we want. This is also called **inverse transform sampling**.

Conversely, we can start with a continuous random variable $X$ and transform $X$ into a ${\rm Unif}(0, 1)$ random variable $U$. This is also called the **probability integral transform**. This is useful in statistical tests, etc.

>[!theorem]
>Let $F$ be a continuous<sup>1</sup> CDF that is strictly increasing on the support of the distribution. (Thus, $F$ is a bijection from the support to $(0,1)$ and has an inverse function $F^{-1}: (0,1)\to\mathbb R$.)
>
>If $U\sim{\rm Unif}(0,1)$, then $X=F^{-1}(U)$ is a random variable with CDF $F$.
>
><sup><small></sup>[1]: Without this assumption, we can transform the standard uniform distribution into a discrete distribution, but just not vice versa.</small>

**Proof.** 
- Let $F(x)$ be the CDF of $F$. We show that our derived CDF $F_X(x)=F(X)$.
- By definition, the CDF of $X$ is the function that maps $x\in \mathbb R$ to $\Pr(X\leq x)$. 
- $\Pr(X\le x)=\Pr(F^{-1}(U)\le x)$
- Applying $F$ to both sides of the equation (since $F$ is increasing), we have $$\Pr(F(F^{-1}(U)\le F(x))$$
- Since we know $U\sim{\rm Unif}(0,1)$, $\Pr(U\le F(x))=F(x)$.
$$\tag*{$\square$}$$

>**Example.** Universality with Rayleigh.
>
>The Rayleigh distribution has CDF $F(x)=1-e^{-x^2/2}, x>0$. Starting with $U\sim{\rm Unif}(0,1)$, how can we generate a random variable with the Rayleigh distribution?
>
>>[!solution]-
>>First, find $F^{-1}$:
>>- Let $u=F(x)=1-e^{-x^2/2}$ for $x>0$
>>- Solve for $x$ in terms of $u$: $x=\sqrt{-2\ln(1-u)}$
>>
>>Thus, $F^{-1}(U)=\sqrt{-2\ln(1-U)}$ has the Rayleigh distribution.

### Backward Direction

>[!theorem]
>
>Let $X$ be a random variable with a continuous CDF $F$ that is strictly increasing on the support of the distribution.
>
>Then, the random variable $F(X)$ has the ${\rm Unif(0,1)}$ distribution.

Some review
- $F:\mathbb R\to[0,1]$
- $F(x)$ is the probability that $X\le x, x\in\mathbb R$
- But $F(X)$ is not the probability that $X\le X$. Rather, it is meant as a function of a random variable.

## Normal Distribution

### Standard Normal Distribution

The Normal distribution is the most important distribution in statistics. By the Central Limit Theorem, under weak assumptions, if $X_1, \dots, X_n$ are i.i.d., the distributions of their sum and average approach the normal distribution as $n$ increases.

>[!definition]
>A random variable $Z$ has the **Normal distribution** with mean 0 and variance 1 (the **standard Normal distribution**) if its PDF is the function $\varphi$:
>$$\varphi(z)=\frac1{\sqrt{2\pi}}e^{-x^2/2}$$
>with support $(-\infty,\infty)$. We write $Z\sim\mathcal N(0,1)$.

The standard normal CDF doesn't have a nice closed-form expression. We call it $\Phi$:
$$\Phi(z)=\int_{-\infty}^z\varphi(t)dt=\int_{-\infty}^z\frac1{\sqrt{2\pi}}e^{-t^2/2}dt$$
#### Properties
- The PDF is symmetric: $\forall z\in\mathbb R, \varphi(z)=\varphi(-z)$
- Tail areas (probabilities) are symmetric: $\Phi(z)=1-\Phi(-z)$
	- E.g., $\Pr(Z\le-2)=\Pr(Z\ge2)$
- $Z\sim\mathcal N(0,1)\implies-Z\sim\mathcal N(0,1)$
	- **Proof.** $F_{-Z}(z)=\Pr(-Z\le z)=\Pr(Z\ge-Z)=1-\Pr(Z<-z)=1-\Phi(-z)=\Phi(z)$
- $\mathbb E(Z)=0$
- ${\rm Var}(Z)=1$

### General Normal Distribution

The general Normal distribution can be defined with its PDF, but we will first introduce it as a location-scale transformation of the standard Normal distribution.

>[!definition]
>If $Z\sim\mathcal N(0,1)$, then for any $\mu\in\mathbb R, \sigma>0$, we say that $X=\mu+\sigma Z$ has the **Normal distribution** with mean $u$, and variance $\sigma^2$. We write $X\sim\mathcal N(\mu,\sigma^2)$.

Then, $\mathbb E(X)=\mathbb E(\mu+\sigma Z)=\mu+\sigma\mathbb E(Z)=\mu$.

Similarly, ${\rm Var}(X)={\rm Var}(\cancel\mu +\sigma Z)=\sigma^2{\rm Var}(Z)=\sigma^2$

#### Standardization

Standardization converts a general Normal random variable to a standard Normal.

>[!definition]
>If $X\sim\mathcal N(\mu,\sigma^2)$, the **standardized version** (or $z$**-score**) of $X$ is
>$$Z=\frac{X-\mu}\sigma\sim\mathcal N(0,1)$$

It's important to note here that the denominator is the standard deviation $\sigma$ and not the variance $\sigma^2$.

#### PDF and CDF

Suppose $X\sim\mathcal N(\mu,\sigma^2)$. The CDF of $X$ is
$$F_X(x)=\Phi\left(\frac{x-\mu}\sigma\right)$$
**Proof.**
$$\begin{align}
F_X(x)&=\Pr(X\le x) \\
&=\Pr(\mu+\sigma Z\le x) \\
&=\Pr\left(Z\le\frac{x-\mu}\sigma\right) \\
&=\Phi\left(\frac{x-\mu}\sigma\right)
\end{align}$$

The PDF of $X$ is
$$f_X(x)=\varphi\left(\frac{x-\mu}\sigma\right)\frac1\sigma=\frac1{\sqrt{2\pi}\sigma}{\rm exp}\left(-\frac{(x-\mu)^2}{2\sigma^2}\right)$$
which follows from the chain rule.

>**Example.** Suppose $X\sim\mathcal N(-1,4)$. Find $\Pr(|X|<3)$.
>
>>[!solution]-
>>$$\begin{align}
\Pr(|X|<3)&=\Pr(-3<X<3) \\
\text{Let }Z&=\frac{X-\mu}{\sigma} \\&=\frac{X+1}2\\
X&=2Z-1 \\
\Pr(|X|<3)&=\Pr(-3<2Z-1<3) \\
&=\Pr(-1<Z<2) \\
&=\Phi(2)-\Phi(-1) \\
&\approx0.819
\end{align}$$
### 68-95-99.7% Rule

>[!theorem]
>If $X\sim \mathcal N(\mu,\sigma^2)$ then
>- $\Pr(\mu-\sigma<X<\mu+\sigma)\approx0.68$
>- $\Pr(\mu-2\sigma<X<\mu+2\sigma)\approx0.95$
>- $\Pr(\mu-3\sigma<X<\mu+3\sigma)\approx0.997$

These are probabilities that $X$ is within 1, 2, or 3 standard deviations of the mean.

This result can also be applied to $Z$:
- $\Pr(-1<Z<1)\approx0.68$
- $\Pr(-2<Z<2)\approx0.95$
- $\Pr(-3<Z<3)\approx0.997$

### Sum of Independent Normal Distributions

>[!theorem]
>Suppose
>- $X_1\sim\N(\mu_1,\sigma_1^2)$
>- $X_2\sim\N(\mu_2,\sigma_2^2)$
>- $X_1\perp X_2$
>  
>  Then, $X_1+X_2\sim\N(\mu_1+\mu_2,\sigma_1^2+\sigma_2^2)$.

**Proof.** Using [MGFs](Moment%20Generating%20Functions.md#Location-Scale%20Transformations),
$$\begin{align}
M_{X_1}(t)&=\exp\paren{\mu_1t+\frac12\sigma_1^2t^2} \\
M_{X_2}(t)&=\exp\paren{\mu_2t+\frac12\sigma_2^2t^2} \\
M_{X_1+X_2}(t)&=M_{X_1}(t)\cdot M_{X_2}(t) \\
&=\exp\paren{[\mu_1+\mu_2]t+\frac12[\sigma_1^2+\sigma_2^2]t^2}
\end{align}$$
The last expression is the MGF of the $\N(\mu_1+\mu_2,\sigma_1^2+\sigma_2^2)$ distribution. Therefore, $X_1+X_2\sim\N(\mu_1+\mu_2,\sigma_1^2+\sigma_2^2)$.
$$\qed$$

## Exponential Distribution
### Motivation

The Exponential distribution models the waiting time until the next "arrival" of some type of event:
- The waiting time until the next text message on a phone
- The next car accident in Philadelphia
- The next major earthquake in the world

From these examples, you can see that the Exponential distribution is closely related to the Poisson distribution, which models the number of arrivals in a given time period.

To take the last example: On average, there are 17 "major" earthquakes per year. Let $N_1$ be the total number of major earthquakes in the next year.

Recall that if $X\sim{\rm Pois}(\lambda)$, then $\mathbb E(X)=\lambda$, and for $k\in\mathbb N$, 
$$\Pr(X=k)=\frac{e^{-\lambda}\lambda^k}{k!}$$

We can model the distribution of $N_1$ as ${\rm Pois}(17)$. Similarly, let $N_t$ be the number of major earthquakes in the next $t$ years. Then, $N_t\sim{\rm Pois}(17t)$. Note that $t$ can be any positive real number. This is a continuous-time model.

Finally, let $T$ be the waiting time from now until the next major earthquake. We show that the CDF of $T$ is 
$$F_T(t)=\Pr(T\le t)=\Pr(N_t>0)=1-e^{-17t}$$ and the PDF of $T$ is
$$f_T(t)=17e^{-17t}, t>0$$

**Proof.** Note that $T\le t$ iff the wait time until the next quake is $\le t$ years. This is equivalent to saying that at least 1 quake occurs within the next $t$ years. That is, the probability that $T\le t$ is the same as the probability that $N_t>0$. This is the event that $N_t\ne0$, so its probability is $1-\Pr(N_t=0)$.

That is,
$$\Pr(N_t\ne0)=1-\Pr(N_t=0)=1-\frac{e^{-17}\lambda^{0}}{0!}=1-e^{-17}$$

### General Form

>[!definition]
>A random $X$ has **Exponential distribution** with parameter $\lambda>0$ if the PDF of $X$ is
>$$f(x)=\lambda e^{-\lambda x}$$
>for $x>0$ (and 0 otherwise). We write $X\sim{\rm Expo}(\lambda)$.
>
>$\lambda$ is often called the **rate** parameter (e.g., the expected number of earthquakes per year).
>
>The CDF is
>$$F(x)=1-e^{-\lambda x}$$
>for $x>0$.


Similar to the normal distribution, we can use scale transformations to switch between ${\rm Expo}(\lambda)$ and ${\rm Expo}(1)$. Specifically, 
1. If $X\sim\Expo(1)$, then $\frac{X}\lambda\sim\Expo(\lambda)$
2. If $Y\sim\Expo(\lambda)$, then $\lambda Y\sim \Expo(1)$

This result is easily shown using the distributions' CDFs.

### Expectation and Variance

If $X\sim\Expo(1)$, then $\E(X)=1$ and $\Var(X)=1$ 

Thus, if $Y\sim\Expo(\lambda)$, 
- $\E(Y)=\frac1\lambda$
- $\Var(Y)=\frac1{\lambda^2}$

### Memoryless

>[!definition]
>A distribution is **memoryless** if a random variable $X$ from that distributions atisfies
>$$\Pr(X\ge s+t\mid X\ge s)=\Pr(X\ge t)$$
>for all $s>0, t>0$.

Here's some intuition: suppose $X$ is the waiting time from today to the next major earthquake, and $X\sim\Expo(17)$. Now suppose the world doesn't have a major earthquake in the next 3 months. Does that make us due for an earthquake? Memorylessness tells us that this isn't the case. It turns out that if we've waiting a quarter of a year, the distribution of the additional waiting time $X-\frac14$ is identical to the original distribution. That is,
$$\Pr\left(X-\frac14\ge t\ \middle|\ X\ge\frac14\right)=\Pr(X\ge t)$$
for all $t>0$. 

In other words, it doesn't matter how long we've waited. An additional wait of length $t$ is just as likely now as it was when we started.

>[!theorem]
>The exponential distribution is memoryless.

**Proof.** Suppose that $X\sim \Expo(\lambda)$. Then, 
$$\begin{align}
\Pr(X\ge s+t\mid X\ge s)&=\frac{\Pr(X\ge s+t)}{\Pr(X\ge s)} \\
&=\frac{1-F_X(s+t)}{1-F_X(s)} \\
&=\frac{2^{-\lambda(s+t)}}{e^{-\lambda s}} \\
&=2^{-\lambda t} \\
&=\Pr(X\ge t)\\
&\qed
\end{align}$$

>[!note]
>As it turns out, the $\Expo(\lambda)$ distributions are the only memoryless continuous distributions.
>
>Further, while this is realistic for some waiting times, like radioactive decay, it's not for others, like human lifetimes.

## Multivariate Normal Distribution

### Motivation

The multivariate normal (MVN) is a [joint distributions](Joint%20Distributions.md) that generalizes the normal. The MVN distribution is important in statistical inference (e.g., confidence intervals, significance tests, etc.).

For example, suppose $\hat\beta_1,\dots,\hat\beta_7$ are the estimated coefficients of a regression model, and we need to approximate the distribution of $\hat\beta_3-\hat\beta_4$. 

### Definition

>[!definition]
>A **random vector** is a vector $(X_1,\dots,X_k)$ of random variables where the order is meaningful.

>**Example.** If $X,Y$ are random variables, $(X,Y)$ is a random 2-dimensional vector. 

>[!definition]
>A random vector $(X_1,\dots,X_k)$ have the **Multivariate Normal** joint distribution **(MVN)** if every linear combination of the $X_j$'s has a normal distribution.
>
>That is, for every $t_1,\dots,t_k$, $$t_1X_1+\dots+t_kX_k$$
>has a normal distribution or is constant.

There are a couple situations where the "constant" exception is required:
1. The coefficients are all zero: $0\cdot X_1+\dots+0\cdot X_k=0$.
2. We divide everyone into categories (e.g., each represents the proportion of people in a particular disjoint group). Then $X_1+\dots+X_k=1$.

The parameters of a MVN distribution are:
- The means of $X_1,\dots,X_k$
- The variances of $X_1,\dots,X_k$
- The covariances or correlations between each pair of random variables among $X_1,\dots,X_k$

The variance and covariance parameters are often listed in a $k\times k$ **covariance matrix**. 

Another definition of the MVN distribution is using its PDF:
$$f_{\bf X}(x_1,\dots,x_k)=\frac{\exp\left(-\frac12(\mathbf x-{\bf\mu})^\top\mathbf\Sigma^{-1}(\mathbf{x}-\mathbf\mu) \right)}{\sqrt{(2\pi)^k|\mathbf\Sigma|}}$$
where $\mathbf\Sigma$ is the covariance matrix and $\mu$ is the mean (note that it is a vector).
### Properties

>[!theorem]
>If $(X_1,\dots,X_k)$ is multivariate normal, then each of the individual random variables $X_j$ is normal. The converse is not necessarily true, however.

>**Example.** A non-example of the MVN
>
>Suppose $X\sim\N(0,1)$. Flip a coin, independently of $X$. Let $Y=X$ if heads, and $Y=-X$ if tails. Then, $Y\sim\N(0,1)$.
>
>Using LOTP, we can find the CDF of $Y$. 
>$$\begin{align}
F_Y(y)&=\Pr(Y\le y) \\
&=\Pr(Y\le y\mid H)\cdot\frac12+\Pr(Y\le y\mid T)\cdot\frac12 \\
&=\Pr(X\le y\mid H)\cdot\frac12+\Pr(-X\le y\mid T)\cdot\frac12 \\
&=\Pr(X\le y)\cdot\frac12+\Pr(X\le y)\cdot\frac12 \\
&=\Phi(y)\cdot\frac12+\Phi(y)\cdot\frac12 \\
&=\Phi(y)
\end{align}$$
>We now show that $(X,Y)$ is not MVN. Particularly, $X+Y$ is a non-normal linear combination of $X$ and $Y$. 
>$$\begin{align}
\Pr(X+Y=0)&=\Pr(X+Y=0\mid H)\cdot\frac12+\Pr(X+Y=0\mid T)\cdot\frac12 \\
&=\Pr(X=0\mid H)\cdot\frac12+\Pr(X-X=0\mid T) \\
&=0+1\cdot\frac12 \\
&=\frac12
\end{align}$$
>This implies that $X+Y$ doesn't follow the normal distribution because the probability of any value being any random variable being a particular value is 0.
>
>Aside: $X+Y$ is interesting because it's a hybrid between discrete and continuous. It has a massive probability of being a particular value, but the rest of the time it's similar to the normal.

>[!theorem]
>If $X_1,\dots,X_k$ are mutually independent normal random variables, then $(X_1,\dots,X_k)$ is multivariate normal.

**Proof.** Consider any linear combination $t_1X_1+\dots +t_kX_k$. The sum of independent normals is normal. 

>[!theorem]
>If $(X,Y)$ is bivariate normal and $\Cov(X,Y)=0$, then $X, Y$ are independent.


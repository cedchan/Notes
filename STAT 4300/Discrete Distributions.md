: ## Bernoulli Distribution

>[!definition]
>A random variable $X$ has the **Bernoulli distribution** with parameter $p\in (0,1)$ if $\Pr(X=1)=p$ and $\Pr(X=0)=1-p$ 
>
>We also say $X$ is distributed as Bernoulli with parameter $p$ and write $X\sim{\rm Bern}(p)$.

Note that the "Bernoulli distribution" is really a family of distributions, so it's important to specify $p$. 

### PMF of the Binomial Distribution

Consider the general case of $n$ trials. We want to find $\Pr(X=k)$ for any $k$. There are $\binom nk$ ways to choose $k$ slots among the $n$ trials. The probability of these $k$ options is $p^k(1-p)^{n-k}$. 

Thus, if $X\sim{\rm Bin}(n,p)$, then the PMF of $X$ is
$$\Pr(X=k)=\binom nkp^k(1-p)^{n-k}$$
for $k\in [0..n]$. 
## Hypergeometric Distribution

Suppose that in some population, each person drinks wine or beer (but not both).
- $w$: No. of wine drinkers
- $b$: No. of beer drinkers

We draw a random sample of size $n$ without replacement. Let $X$ be the number of wine drinkers in our sample. $X$ is said to have the **Hypergeometric distribution** with parameters $w, b,$ and $n$. That is, $X\sim{\rm HGeom}(w, b, n)$.

>**Example.** A forest has $N$ elk. Today, $m$ of the elk are captured, tagged, and released. At a later date, we randomly recapture $n$ of the $N$ elk. Let $X$ be the number of tagged elk in our recaptured sample.  What is the distribution of $X$?
>
>>[!solution]-
>>We argue that this problem is analogous to the wine/beer problem. $X\sim{\rm HGeom}(m,N-m,n)$.
### PMF of the Hypergeometric Distribution

Consider the event $X=k$.
$$k\mapsto\Pr(X=k)=\frac{\text{\# outcomes with $X=k$}}{\text{\# of possible outcomes}}$$

We can think of each possible sample of size $n$ (where order doesn't matter) as a possible outcome in our experiment. This yields a total of $\binom{w+b}{n}$ possible outcomes, all of which are equally likely. 

There are $\binom wk$ ways to choose the $k$ wine drinkers and $\binom{b}{n-k}$ ways to choose the $n-k$ beer drinkers. Thus,
$$\Pr(X=k)=\frac{\binom wk\binom{b}{n-k}}{\binom{w+b}n}$$
for integers $k$ with $0\leq k\leq w$ and $0\leq n-k\leq b$. 

## Geometric Distribution

Consider a sequence of independent Bernoulli trials, each with the same success probability $p\in(0,1)$. Assume that trials continue until the first success.

Let $X$ be the number of failures until the first success. Then $X$ has the **Geometric distribution** with parameter $p$. We can write $X\sim{\rm Geom}(p)$. 

>[!note]
>The "First Success" distribution includes the first success. That is, if $Y\sim{\rm FS}(p)$, then $Y=X+1$. 

### PMF of the Geometric Distribution

For any $k\geq 0$, 
$$\Pr(X=k)=(1-p)^kp$$
### Expectation of the Geometric Distribution

There are several proofs for the expectation of the geometric distribution (some messier than others). For now, we simply state the result:
$$\mathbb E(X)=\frac{1-p}p$$
We can derive the expectation of the first success distribution with [linearity of expectation](Expectation.md#Linearity%20of%20Expectation). $$\mathbb E(Y)=\mathbb E(X+1)=\mathbb E(X)+1=\frac1p$$

 ## Negative Binomial Distribution

The **negative binomial distribution** is a generalization of the geometric distribution. Consider a sequence of independent Bernoulli trials, each with success probability $p\in(0,1)$. Assume that the trials continue at least until the $r$-th success, where $r\in\mathbb Z^+$. 

Let $X$ be the number of failures before the $r$-th success. Then $X\sim{\rm NBin}(r,p)$. (Note that when $r=1$, this is just the Geometric distribution.)

### PMF of the Negative Binomial Distribution
$$\Pr(X=n)=\binom{n+r-1}{r-1}p^r(1-p)^n$$
Note that we have $n$ failures and $r$ successes. We know that the last element must always be a success, so there are only $n+r-1$ manipulable slots. Of these slots, we choose $r-1$ slots for successes (where the remaining slots are failures). Then, like the binomial PMF, we multiply these by the probabilities of each of these events.

## Poisson Distribution

The Poisson distribution is often used as a model for count data (i.e., data with possible values 0, 1, 2, ...). In this story, we model a count variable $X$ as the number of successes in a sequence of Bernoulli trials where
- the number of trials is large and
- in each trial, the probability of success is small

>**Examples.**
>- $X$ is the number of text messages you receive in class
>- $X$ is the number of car accidents in Philadelphia in the next hour

Consider that second example. Let $X$ be the number of car accidents in Philadelphia during the next hour. We can model the distribution of $X$ with some simplifications:
- The hour is divided into $n$ subintervals of time, where $n$ is large.
- In each subinterval, there's a small probability $p$ of one car accident and we assume that having more than one accident has probability 0. 
- Accidents across subintervals are independent.

Each of these is then a binomial event. One motivation for the Poisson distribution is when it becomes computationally expensive to calculate the PMF of ${\rm Bin}(n,p)$ for large $n$. The Poisson approximates this when $n$ is large and $p$ is small.

This approximation comes by finding the binomial PMF as $n\to\infty$ with $\lambda=np$ held constant.

$$\begin{align}
\Pr(X=0)&=(1-p)^n \\
&=\left(1-\frac\lambda n\right)^n
\end{align}$$
Recall that $$\lim_{n\to\infty}\left(1-\frac xn\right)^n=e^x$$
Letting $x=-\lambda$,
$$\lim_{n\to\infty}\Pr(X=0)=e^{-\lambda}$$

Further, for $k=1,2,\dots$, the ratio $$\frac{\Pr(X=k)}{\Pr(X=k-1)}=\frac{n-(k-1)}{k}\frac p{1-p} =\frac{\lambda-(k-1)p}{k(1-p)}$$
Then, as $n\to\infty$, with $\lambda=np$ fixed, we have $p\to0$ and 
$$\lim_{n\to\infty}\frac{\Pr(X=k)}{\Pr(X=k-1)}=\frac\lambda k$$
Thus $$\begin{align}
\lim_{n\to\infty}\Pr(X=0)&=e^{-\lambda} \\
\lim_{n\to\infty}\Pr(X=1)&=e^{-\lambda}\lambda \\
\lim_{n\to\infty}\Pr(X=2)&=e^{-\lambda}\frac{\lambda^2}{2} \\
\end{align}$$
From here, we can find the general formula.

>[!definition]
>A random variable $X$ has the **Poisson distribution** with parameter $\lambda>0$, written $X\sim{\rm Pois(\lambda)}$, if the PMF of $X$ is $$\Pr(X=k)=\frac{e^{-\lambda}\lambda^k}{k!}$$
>for $k\in\mathbb N$ (and 0 otherwise).
>
>$\lambda$ is often known as the **rate** parameter.

### Properties
- If $X\sim {\rm Bin}(n,p)$ and we take the limit as $n\to\infty$ and $p\to0$ with $\lambda=np$, then the PMF of $X$ converges to the ${\rm Pois}(\lambda)$ PMF.
- If $X\sim{\rm Pois}(\lambda_1), Y\sim{\rm Pois}(\lambda_2)$ and $X\perp Y$, then $X+Y\sim{\rm Pois}(\lambda_1+\lambda_2)$.
- If $X\sim{\rm Pois}(\lambda)$, then $\mathbb E(X)={\rm Var}(X)=\lambda$.
- The Poisson distribution is often a good approximation even when the $n$ Bernoulli trials have different success probabilities and aren't perfectly independent. 

The last bullet is known as the **Poisson paradigm**, which we only cover informally. In more detail, let $A_1, A_2,\dots, A_n$ be events with $p_j=\Pr(A_j)$, where $n$ is large, the $p_j$ are small, and the $A_j$ are independent or weakly dependent. Let $I_j$ be an indicator for $A_j$, and 
$$X=\sum_{j=1}^nI_j$$
Then, $X$ is approximately ${\rm Pois}(\lambda), \lambda=\sum_{j=1}^np_j$. 
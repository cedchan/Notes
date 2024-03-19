A continuous random variable can take on any real value in an interval (e.g., height of a person, temperature, etc.). It's not super useful to define a [PMF](Random%20Variables.md#Probability%20Mass%20Functions) for a continuous random variable $X$, because it's probably unlikely that $X$ will be exactly the number you're measuring. 

This is because if there exists any range in which the probability of any single point in that range is non-negative (this must be true, otherwise our random variable would be discrete), we will get an infinite number of non-negative numbers, which will sum to more than 1, which is impossible. Thus, we must say all numbers are infinitesimally small—that is, 0. Note, however, that the probability that $X$ lies within some non-empty interval can be positive because the interval has a positive length.

So if the PMF is not useful, what should we use? We'll use the [CDF](Random%20Variables.md#Cumulative%20Distribution%20Functions) and its derivative—the probability density function.

>[!definition]
>A random variable $X$ has a **continuous distribution** if its cumulative distribution function $F(u)=\Pr(X\le u)$ is
>- Differentiable (and therefore continuous) everywhere, or
>- Continuous everywhere and differentiable at all but a finite number of points in $\mathbb R$.
>  
>  We say $X$ is a **continuous random variable** if it has a continuous distribution.

## Probability Density Functions

>[!definition]
>For a continuous random variable $X$ with CDF $F_X$ (or $F$), the **probability density function (PDF)** $f_X$ (or just $f$) is the derivative of the CDF:
>$$f(u)=F'(u)$$
>
>The **support** of $X$ is the set of all $u$ such that $f(u)>0$.

The PDF of a continuous random variable is analogous to the PMF of a discrete one. It's important to note, however, that $f(u)$ is not a probability (recall from earlier that $\Pr(X=u)=0$). Rather, it's an approximation that $X$ lies within a small interval of length $\epsilon$ that is centered on $u$. That is,
$$f(u)\cdot\epsilon\approx\Pr\left(X\in\middle[u-\frac\epsilon2,u+\frac\epsilon2\middle]\right)$$

### Properties

- The PDF is nonnegative: $f(u)\geq 0$ for all $u\in\mathbb R$
- The PDF integrates to 1: $$\int_{-\infty}^\infty f(u)du=1$$
	Note that this really means
	$$\int_{-\infty}^\infty f(u)du=\lim_{b\to\infty}\lim_{a\to-\infty}\int_a^bf(u)du$$
  
### PDF to CDF

>[!theorem]
>Let $X$ be a continuous random variable with PDF $f$. Then the CDF of $X$ is
>$$F(u)=\int_{-\infty}^uf(t)dt$$

**Proof.** We know $f$ is the derivative of $F$. Then, by the Fundamental Theorem of Calculus,
$$\int_a^uf(t)dt=F(u)-F(a)$$
Finally, taking the limit as $a\to-\infty$, we have
$$\int_{-\infty}^uf(t)dt=F(u)-\lim_{a\to-\infty}F(a)=F(u)-0=F(u)$$

### Finding Probabilities

To estimate the probability that $X$ lies in some interval $[a,b],(a,b],[a,b),(a,b)$, we can use the PDF or the CDF (probability can be thought of as the area under the curve). Note that the endpoints don't matter (that is, the probability that $X$ lies in any of those four intervals is equal) because $\Pr(X=a)=\Pr(X=b)=0$. 

Then, 
$$\Pr(a<X\leq b)=F(b)-F(a)=\int_a^bf(u)du$$
>**Example.** The Rayleigh distribution. The Rayleigh distribution has this CDF:
>$$F(x)=\begin{cases}1-e^{-x^2/2} & x>0\\ 0 & x\leq 0\end{cases}$$
>Find the PDF.
>>[!solution]-
>>Recall the chain rule: $\frac{dy}{dx}=\frac{dy}{du}\frac{du}{dx}$. Now, for $x>0$: Let $u=\frac{-x^2}2$
>>$$\begin{align}
f(x)=F'(x)&=-e^{-x^2/2}(-x) \\
&=xe^{-x^2/2}
\end{align}$$
>>Note that it's important to specify the support that $x>0$.
>
>Find $\Pr(X>2)$ using the CDF.
>>[!solution]-
>>$$\begin{align}
\Pr(X>2)&=1-\Pr(X\leq2) \\
&=1-F_X(2)
\end{align}$$
>
>Find $\Pr(X>2)$ using only the PDF and $u$-substitution.
>>[!solution]-
>>$$\begin{align}
\Pr(X>2)&=\int_2^\infty xe^{-x^2/2}dx \\
\text{Let }u&=-\frac{x^2}2 \\
\frac{du}{dx}&=-x \\
du&=-dx\\
x=2&\to-\frac{2^2}{2}=-2 \\
x=\infty&\to-\infty \\
\Pr(X>2)&=\int_{-2}^{-\infty} -e^udu \\
&=\int_{-\infty}^{-2}e^udu \\
&=e^u\Big|_{-\infty}^{-2} \\
&=e^{-2}-\lim_{u\to-\infty}e^u \\
&=e^{-2}
\end{align}$$

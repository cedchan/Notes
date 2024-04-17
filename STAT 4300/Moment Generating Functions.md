## Moments

>[!definition]
>For any random variable $X$ and for $n\in\mathbb N$, 
>- The $n$-th **moment** of $X$ is $\E(X^n)$.
>- The $n$-th **central moment** of $X$ is $\E([X-\mu]^n)$, where $\mu=\E(X)$.
>- The $n$-th standardized **moment** of $X$ is $\E\left(\middle[\frac{X-\mu}\sigma\middle]^n\right)$, where $\sigma={\rm SD}(X)=\sqrt{\Var(X)}$
>  
>  If expectations are undefined, so are the corresponding moments.

Moments are often used as summaries of a distribution:
- [Mean](Expectation.md) (1st moment)
- [Variance](Expectation.md#Variance) (2nd central moment)
- Skewness (3rd standardized moment)—how (a)symmetrical a distribution is
- Excess kurtosis (4th standardized moment minus 3)—how heavy the tails are
	- E.g., the [Uniform Distribution](Continuous%20Distributions.md#Uniform%20Distribution) would have the lowest kurtosis

## Moment Generating Functions

>[!definition]
>The **moment generating function (MGF)** of a random variable $X$ is 
>$$M_X(t)=\E(e^{tX})$$
>as a function of $t$, if $\E(e^{tX})$ is finite for all $t$ in some open interval $(-a,a)$ where $a>0$ (otherwise the MGF doesn't exist). 

>**Example.** The Bernoulli MGF.
>
>Suppose $X\sim\Bern(p)$. For any $t\in\mathbb R$, [LOTUS](Expectation.md#Law%20of%20the%20Unconscious%20Statistician%20(LOTUS)) gives us
>$$\begin{align}
\E(e^{tX})&=pe^{t\cdot1}+(1-p)e^{t\cdot0} \\
&=pe^t+(1-p)<\infty
\end{align}$$
>Thus, the MGF is $$M(t)=\frac{e^{tb}-e^{ta}}{t(b-a)}$$for all $t\in \mathbb R$.

>**Example.** The Exponential MGF
>
>The PDF is $f(x)=e^{-x}$ for $x>0$. For any $t<1$, [LOTUS](Continuous%20Random%20Variables.md#Expectation#Continuous%20Law%20of%20the%20Unconscious%20Statistician%20(LOTUS)) gives us that
>$$\begin{align}
M_X(t)&=\E(e^{tX}) \\
&=\int_{-\infty}^\infty e^{tx}f(x)dx \\
&=\int_0^\infty e^{tx}e^{-x}dx \\
&=\int_0^\infty e^{(t-1)x}dx \\
&=\frac{1}{t-1}e^{(t-1)x}\Big|_{x=0}^{x\to\infty}
\end{align}$$
>Then, we have 2 cases:
>
>*Case 1a:* $t<1$. 
>$$\begin{align}
t<1&\implies t-1<0 \\
M_X(t)&=0-\left(\frac1{t-1}\right) \\
&=\frac{1}{1-t}
\end{align}$$
>*Case 1b:* $t>1$.
>$$\begin{align}
t>1&\implies t-1>0 \\
M_X(t)&=\infty-\frac1{t-1} \\
&\implies \E(e^{tX}) \text{ is undefined}
\end{align}$$
>*Case 2:* $t=1$.
>$$\begin{align}
M_X(t)&=\int_0^\infty1dx \\
&=\infty \\
&\implies \E(e^{tX}) \text{ is undefined}
\end{align}$$
>Still, we only need the MGF to be defined for some open interval, which is covered in case 1a. 

### Why MGFs?

>[!theorem]
>If the MGF of $X$ exists, the $\E(X^n)$ equals the $n$-th derivative of the MGF, evaluated at 0. That is,
>$$\E(X^n)=M^{(n)}(0)$$
>for $n\in\mathbb N$.

As some motivation, recall that by the Taylor series expansion,
$$e^x=1+x+\frac{x^2}{2!}+\dots$$
Then,
$$\E(e^{tX})=1+tE(X)+\frac{t^2\E(X^2)}{2!}+\dots$$

>**Example.** Suppose $X\sim\Expo(1)$. Then,
>$$M_X(t)=\frac1{1-t}$$
>for $t<1$. Find $\E(X)$ and $\Var(X)$. 
>
>>[!solution]-
>>From above results,
>>- $\E(X)=M'_X(0)$
>>- $\E(X^2)=M_X''(0)$
>>- $\Var(X)=\E(X^2)-\E(X)^2$
>>
>>Then,
>>$$\begin{align}
M_X(t)&=\frac1{1-t} \\
&=(1-t)^{-1} \\
M_X'(t)&=-1(1-t)^{-2}(-1) \\
&=(1-t)^{-2}\\
M''_X(t)&=2(1-t)^{-3} \\
\E(X)&=1\\
\Var(X)&=2-1^2 \\
&=1
\end{align}$$

>[!theorem]
>If $X$ and $Y$ have the same MGF, they must have the same distribution.

>[!theorem]
>If $X$ and $Y$ are independent and their MGFs exist, then the MGF of $X+Y$ is the product of their MGFs:
>$$M_{X+Y}(t)=M_X(t)\cdot M_Y(t)$$

**Proof.**
$$\begin{align}
X\perp Y&\implies e^{tX}\perp e^{tY} \\
\E(e^{t(X+Y)})&=\E(e^{tX}e^{tY}) \\
&=\E(e^{tX})\E(e^{tY})\\
&\qed
\end{align}$$

## Location-Scale Transformations

>[!theorem]
>If $X$ has MGF $M_X(t)$, then the MGF of $a+bX$ is
>$$M_{a+bX}(t)=\E(e^{t(a+bX)})=e^{at}\E(e^{btX})=e^{at}M_X(bt)$$

>**Example.** Suppose $X\sim\Expo(1)$. Let $Y=\frac{X}\lambda, Y\sim\Expo(\lambda)$.
>
>Let $a=0$, $b=\frac1\lambda$
>$$\begin{align}
Y&=a+bX \\
M_Y(t)&=M_X\left(\frac t\lambda\right) \\
&=\frac{1}{1-\frac t\lambda} \\
&=\frac \lambda{\lambda-t}
\end{align}$$
>for $t<\lambda$.

>**Example.** Standard normal MGF
>
>If $Z\sim\N(0,1)$, by LOTUS,
>$$\begin{align}
\E(e^{tZ})&=\int_{-\infty}^\infty e^{tz}\frac1{\sqrt{2\pi}}e^{-\frac{z^2}2}dz \\
&=\int_{-\infty}^\infty
\frac{1}{\sqrt{2\pi}}e^{-\frac{z^2}2}dz \\
\end{align}$$
>Completing the square,
>$$-\frac{z^2}2+tz=-\frac{z^2-2tz}{2}=-\frac{(z-t)^2}{2}+\frac{t^2}{2}$$
>Then,
>$$\begin{align}
\E(e^{tZ})&=\int_{-\infty}^\infty\frac{1}{\sqrt{2\pi}}\exp\paren{-\frac{(z-t)^2}{2}+\frac{t^2}2}dz
\end{align}$$
>The above is the PDF of the $\N(t,1)$ distribution, so it must integrate to 1. Thus,
>$$M_Z(t)=e^{t^2/2}$$ for all $t\in\mathbb R$.

>**Example.** General normal MGF
>If $X\sim\N(\mu,\sigma^2)$, then $X=\mu+\sigma Z$, where $Z$ is the standard normal.
>
>Then,
>$$M_X(t)=e^{\mu t}M_Z(\sigma t)=e^{\mu t}e^{(\sigma t)^2/2}=\exp\left(\mu t+\frac12\sigma^2t^2\right)$$
>for all $t\in\mathbb R$.
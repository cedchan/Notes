---
header-includes: []
---
## Review: Linear Models

>[!danger]
>Review this

>[!definition]
>A **hyperplane** $H$ is defined as $\{x\mid w^\top x + b=0\}$.

A **linear model** has the form
$$h(x)=\mathrm{sign}(w^\top x+b)$$
Properties:
- Scale invariant: $w\rightarrow\alpha w$ are equivalent
	- $\forall x\rightarrow \beta x$ a similar hyperplane exists
	- Assume $\max ||x||=1 \implies ||x|| \leq 1$
- $b$ is useless
	- $w, b\implies w^\top x + b$
- Margin of a hyperplane $\gamma=\min\limits_i d(H, x_i)=\min\limits_i|w^\top x_i|$
- $y_i w^\top x_i\geq 0$

## Perceptron Algorithm

Assumes $\exists w^* \text{ s.t. } \forall i, y_iw^{*\top}x_i\geq 0$. That is, we assume there exists some hyperplane that separates the data—the data is **linearly separable**.

>[!algorithm]
>$$\begin{align}
\hline
&\text{$w_0\leftarrow 0$} \\
&\text{\textbf{for} $t=1, 2, \dots$:} \\
&\text{\quad find some $i$ so that $y_iw^\top x_i\leq 0$} \\
&\text{\quad{\bf if} none:} \\
&\text{\quad\quad break} \\
\hline
\end{align}$$

$$\begin{align}
w_t^\top x_i \\
w_{t+1}^\top x_i&=(w_t+y_ix_i)^\top x_i \\
&=w_t^\top x_i+y_ix_i^\top x_i \\
&\leq w_t^\top x_i + 1 \\
\end{align}$$
Assume $w^*$ exists: $w_f \rightarrow w^*$
$$\begin{align}
\cos\theta&=\frac{w_t^\top w^*}{||w_t||} \leq1 \\
w_t^\top w^*&=(w_{t-1}+y_ix_i)^\top w^* \\
&=w_{t-1}^\top w^*+\underbrace{y_iw^{*\top}x_i}_{=|w^{*\top}x_i|\geq\gamma} \\
&\geq w_{t-1}^\top w^*+\gamma \\
&\geq w_0^\top w^*+t\gamma \\
w_t^\top w^*&=(w_{t-1}+y_ix+i)^\top w^* \\
&=w_{t-1}^\top w^*+y_i w^{*\top}x_i \\
&=w_{t-1}^\top w^*+|w^{*\top}x_i| \\
&\geq w_{t-1}^\top w^*+\gamma \\
w_t^\top w_t&=(w_{t-1}+t_ix_i)^\top(w_{t-1}+y_ix_i) \\
&=w_{t-1}^\top w_{t-1}+2y_iw_{t-1}^\top x_i+\underbrace{\cancel{y_i^2}}_{=1}\underbrace{x_i^\top x_i}_{\leq 1} \\
&\leq w_{t-1}^\top w_{t-1}+1 \\
1&\leq\frac{w_t^\top w^*}{\sqrt{w_t^\top w_t}} \\
&\geq\frac{\gamma t}{\sqrt t} \\
1&\leq \gamma\sqrt{t} > t \leq \frac1{\gamma^2}
\end{align}$$
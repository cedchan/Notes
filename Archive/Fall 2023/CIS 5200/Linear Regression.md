## Model Definition

1. **Hypothesis Class:** $h(x)=w^\top x$. That is, $H=\{x\rightarrow w^\top x+b\mid x\in \mathbb R^d, b\in \mathbb R\}$
2. **Loss:** $\ell_\mathrm{sq}(\hat y, y)=(\hat y-y)^2\iff(h(x)-y)^2\iff(w^\top x-y)^2$
	$\hat R(w)=\frac1n\sum_{i=1}^n(w^\top x_i-y_i)^2$, where $\mathcal D=\{(x_1, y_1), \dots, (x_n, y_n)\}$
3. **Update:** $w_{t+1}\leftarrow w_t-\eta_t\nabla\hat R(w_t)$

## Analytic Solution

$$\begin{gather}
X=\begin{bmatrix}\vec x_1 \\ \vec x_2 \\ \vdots\\ \vec x_n\end{bmatrix}, y=\begin{bmatrix}y_1 \\ y_2 \\\vdots \\ y_n\end{bmatrix}, w=\begin{bmatrix}w_1 \\ w_2 \\\vdots \\ w_d\end{bmatrix} \\
Xw=\begin{bmatrix}w^\top x_1 \\w^\top x_2 \\\vdots\\ w^\top x_n\end{bmatrix}, Xw-y=\begin{bmatrix}w^\top x_1-y \\w^\top x_2-y \\\vdots\\ w^\top x_n-y\end{bmatrix}, v=\begin{bmatrix}v_1 \\ v_2 \\ \vdots \\ v_n\end{bmatrix}
\end{gather}$$
Squared loss:
$$\begin{align}
(Xw-y)^\top(Xw-y)&=\sum_{i=1}^n(w^\top x_i-y_i)^2 \\
\hat R(w)&=\frac1n\sum_{i=1}^n(w^\top x_i-y_i)^2 \\
\end{align}$$
Noting that $\nabla(f(x)+g(x))=f'(x)+g'(x)$,
$$\begin{align}
\nabla\hat R(w)&=\frac1n\sum_{i=1}^n\nabla_w(w^\top x_i-y_i)^2
\end{align}$$
Noting that $\nabla f(g(w))=f'(g(x))\cdot g'(x)$,
$$\begin{align}
&=\boxed{\frac1n\sum_{i=1}^n2(w^\top x_i-y_i)x_i}
\end{align}$$

### Matrix Form

$$\begin{align}
\nabla\hat R(w)&=\frac1n\sum_{i=1}^n2(w^\top x_i-y_i)x_i\\
&=\frac2n\sum_{i=1}^n(w^\top x_i)x_i-y_ix_i \\
&=\frac2n X^\top Xw-X^\top y
\end{align}$$
Now to minimize, we set to 0:
$$\begin{align}
\frac2n X^\top Xw-X^\top y&=0 \\
X^\top Xw&=X^\top y \\
w^*&=(X^\top X)^{-1}X^\top y
\end{align}$$
## When is Linear Regression Too Powerful

Suppose $n=d\implies X$ is an $n\times n$ matrix. Suppose also that $X$ is invertible.

$$\begin{align}
Xw^*& =X(X^\top X)^{-1}X^\top y\\ 
&=XX^{-1}X^{-1}X^\top y \\
&= y
\end{align}$$ 
Because matrices are invertible with very high probability, this means that in high dimensions, linear regression is essentially able to memorize the dataset. 

### Regularization

$$\mathcal L(w)=\hat R(w)+\underbrace{t(w)}_\mathclap{\text{regularizer}}\iff\min\hat R(w) \text{ s.t. } t(w)\leq B$$

Essentially, we put a weight on each feature so that no single feature is contributing too much to our prediction. Intuitively, $t(w)$ measures the "complexity" of $w$. We introduce a tradeoff here between complexity and accuracy.

There are 2 main regularizers that we'll talk about:
- L1 Regularization: $t(w)=\lambda||w||_1^2=\lambda\sum_{i=1}^d|w_i|$ 
- L2 Regularization: $t(w)=\lambda||w||_2^2=\lambda\sum_{i=1}^dw_i^2$

#### L1 Regularization
$$t(w)=\lambda||w||_1\iff \min\frac1n\sum_{i=1}^n(w^\top x_i-y_i)^2\text{ s.t. }t(w)\leq B$$
That is, we're minimizing the loss (as usual), but with the added constraint that $t(w)$ must be at most $B$. This notation is intuitively easier to understand but the lefthand side is easier to calculate (constrained vs. unconstrained optimization).

In a toy example, let us have 2 features $w_1, w_2$. L1 regularization, by definition, has the limit $|w_1|+|w_2|\leq B$. Graphically, this is a diamond.

![](Pasted%20image%2020230927141929.png)

Our constrained optimization problem means that we're trying to find the point inside the constraint that is closest to $w^*$ (presumably outside of the bounds). 

Because of our construction as a diamond, we're typically going to end up at a corner. This means that at least 1 feature will be set to 0, reducing the number of features we're using. That is, we can use L1 regularization as a sort of feature selection. We get **sparse** solutions.

>[!hint]
>Higher $\lambda$ $\implies$ fewer features.

#### L2 Regularization

Now, instead of having a diamond, L2 regularization has a circle as the constraint:
$$w_1^2+w_2^2\leq B$$
Unlike L1 regularization, we don't get sparse solutions (since there are no corners to land on, it'll be more unlikely that features get eliminated). Instead, though, L2 forces us to rely more evenly on all our features, rather than a couple of strong ones. 

As it turns out, there's an analytic solution to L2 regularization. 
$$\mathcal L(w)=\frac1n\sum_{i=1}^n(w^\top x_i-y_i)^2+||w||_2^2$$
Solving this gives 
$$w^*=(X^\top X+\lambda I)^{-1}X^T y$$
This is called **ridge regression**. From an optimization standpoint, this is easier, so L2 regularization is often preferred.

## Assumptions of Linear Regression

Linear regression assumes that the data is linear, with Gaussian noise added. That is, that the truth is $$y=w^\top x+\varepsilon, \varepsilon\sim N(0, \sigma^2)$$ This implies that 
$$\begin{align}
\Pr(y\mid X, w)&=N(w^\top x, \sigma^2) \\
&=\frac1{\sqrt{2\pi\sigma^2}}e^\frac{-(w^\top x-y)^2}{2\sigma^2}
\end{align}$$
We maximize our probability by maximizing $-(w^\top x-y)^2$, or equivalently, minimizing $(w^\top x-y)^2$.

>[!error]
>look at the notes for full derivation


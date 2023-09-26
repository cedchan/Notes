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
## When is Linear Regression too Powerful

Suppose $n=d\implies X$ is an $n\times n$ matrix. Suppose also that $X$ is invertible.

$$\begin{align}
Xw^*& =X(X^\top X)^{-1}X^\top y\\ 
&=XX^{-1}X^{-1}X^\top y \\
&= y
\end{align}$$ 
Because matrices are invertible with very high probability, this means that in high dimensions, linear regression is essentially able to memorize the dataset. 

### Regularization

$$\mathcal L(w)=\hat R(w)+\underbrace{t(w)}_\mathclap{\text{regularizer}}\iff\min\hat R(w) \text{ s.t. } t(w)\leq B$$
- L1 Regularization: $t(w)=\lambda||w||_2^2$ 
- L2 Regularization: $t(w)=\lambda||w||_1^2$

Essentially, we put a weight on each feature so that no single feature is contributing too much to our prediction. 



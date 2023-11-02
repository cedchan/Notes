## Boosting

**Given:** Algorithm $\mathcal A(\mathcal D)$ that learns **weak learners** $h$ (slightly better than chance, but not very good; e.g., decision stump—depth 1 decision trees).

**Output:** Model $\mathcal H(x)=\sum_{t=1}^T\alpha_th_t(x)$. That is, we learn an ensemble of weak learners and predict by combining these. 

>[!note]
>Intuitively, the difference between boosting and [bagging](Random%20Forests.md#Bagging) is that boosting makes weak models more powerful while bagging makes powerful models weaker.

**Approach:** Train iteratively. At iteration $t$, we have $H_{t-1}(x)=\sum_{i=1}^{t-1}\alpha_{i}h_i(x)$. Add some $h_t: \mathcal H_t(x)\gets \mathcal H_{t-1}(x)+\alpha_th_t(x)$. 

>[!idea]
>At a high level, use the mistakes of $\mathcal H_{t-1}$ to inform $h_t$.
>1. Instead of fitting the labels $y$, fit the errors of $\mathcal H_{t-1}$
>	Imagine $x_i$ has label $y_i$, and $\mathcal H_{t-1}(x_i)$ is wrong. Then, we have residual $h_t(x_i)=y_i-\mathcal H_{t-1}(x_i)$, which gives $\mathcal H_t(x_i)=\mathcal H_{t-1}(x_i)+h_t(x_i)$
>2. Train $h$ on the labels, but give higher weight to points $(x_i, y_i)$ that $\mathcal H_{t-1}$ gets wrong.

## Algorithm

>[!algorithm]
>$$\begin{align}
\hline
&\textbf{Gradient Boosted Regression Trees} \\
\hline
&H_0\gets0 \\
&\textbf{for } t\in[1..T] \\
&\quad \forall i, \text{ compute } r_i=y_i-\mathcal H_{t-1}(x) \\
&\quad h_t\gets\mathcal A_{\text{decision-stump}}(\{(x_1, r_1), \dots, (x_n, r_n)\}) \\
&\quad \mathcal H_t\gets \mathcal H_{t-1}+\alpha h_i \\
\hline
\end{align}$$

Note that $\alpha$ is typically chosen to be constant. It's similar to the learning rate in gradient descent—the lower $\alpha$ is, the more weak learners you need to make your model powerful.

Why doesn't this overfit when $T$ is very high? Well, notice that each time we're decreasing the residuals, which is how we make the model more powerful. This means that the residuals will get closer and closer to 0. At this point, though, since we're only adding weak models, it's impossible to overfit to match a single datapoint—all the model does is choose a single split and have constants on either side. 

The implication of this is that the models we add *must* be very weak, otherwise we will overfit when we keep adding models.

That said, with an excessively large $T$, you might see some points carved out. The solution to this is decreasing $\alpha$. 

## Theory of Boosting

**Central Question:** Where does the residual update come from?

Define a loss $\ell$ that measures how bad $h_t$ is. Then,
$$\begin{align}
h_t&=\underset{h}{\arg\min}\;\ell(\mathcal H_{t-1}+\alpha h) \\
&\approx\underset{h}{\arg\min}\;\ell(\mathcal H_{t-1})+\langle\nabla\ell(\mathcal H_{t-1}),\alpha h\rangle & \text{(Taylor approx.)} \\
&=\underset{h}{\arg\min}\;\begin{bmatrix}
\frac{\partial\ell}{\partial\mathcal H(x_1)} \\ \vdots \\ \frac{\partial\ell}{\partial\mathcal H(x_n)}
\end{bmatrix}^\top\begin{bmatrix}
\alpha h(x_1) & \dots & \alpha h(x_n)
\end{bmatrix}
\end{align}$$

With $\ell(\mathcal H)=\sum_{i=1}^n(\mathcal H(x_i)-y_i)^2$, we get
$$\begin{align}
\begin{bmatrix}2(\mathcal H(x_1)-y_1) \\ 2(\mathcal H(x_2)-y_2)\\\vdots\\2(\mathcal H(x_n)-y_n)\end{bmatrix}^\top[\dots]&=\sum_{i=1}^n2\underbrace{(\mathcal H(x_i)-y_i)}_{u_i}\alpha_nh(x_i) \\
&=\sum_{i=1}^n2u_i\alpha h(x_i)
\end{align}$$
We want $$\underset{h}{\arg\min}\;\sum_{i=1}^n(\alpha h(x_i)-r_i)^2$$to make it a familiar least-squares minimization problem. We can achieve this using some algebraic manipulation.

Note the following:
1. $\sum_{i=1}^nr_i^2$ is constant w.r.t. $h$
2. $\sum_{i=1}^n\alpha^2h(x_i)^2$ is constant. This isn't necessarily true, but we can make it true by changing $h$ such that $\sum_{i=1}^nh(x_i)^2 =1$. 

Then,
$$\begin{align}
\underset{h}{\arg\min}\sum_{i=1}^n-2u_i\alpha h(x_i)&=\underset{h}{\arg\min}\sum_{i=1}^nr_i^2-2r_i\alpha h(x_i) &\text{(Note 1)}\\
&=\underset{h}{\arg\min}\sum_{i=1}^nr_i^2-2r_i\alpha h(x_i)+\alpha^2h(x_i)^2 &\text{(Note 2)} \\
&=\underset{h}{\arg\min}\sum_{i=1}^n(\alpha h(x_i)-r_i)^2
\end{align}$$


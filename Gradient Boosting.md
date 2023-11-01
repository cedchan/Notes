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

Note that $\alpha$ is typically chosen to be constant. It's similar to the learning rate in gradient descent.

Why doesn't this overfit when $T$ is very high? Well, notice that each time we're decreasing the residuals, which is how we make the model more powerful. This means that the residuals will get closer and closer to 0. At this point, though, since we're only adding weak models, it's impossible to overfit to match a single datapoint—all the model does is choose a single split and have constants on either side. 

The implication of this is that the models we add *must* be very weak, otherwise we will overfit when we keep adding models.
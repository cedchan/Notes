## General Boosting

**Goal:** Train a model $H(x)=\sum_{t=1}^T\alpha_th_t(x)$
$${\rm Boosting}(\mathcal D, \mathcal A)\to H(x)$$
At iteration $t$, I have $H_t(x)$. 

There are 2 main approaches to boosting:
1. Fit $h_{t+1}$ to the errors of $H_t(x)$. This is what we did with [gradient boosted trees](Gradient%20Boosting.md).
$$h_{t+1}=\underset{h}{\arg\min}\;\ell(H_t+\alpha h_{t+1})\iff \underbrace{h_{t+1}=\underset{h}{\arg\min\;}\sum_{t=1}^n(h_{t+1}(x)-r_i)^2}_{\mathcal A(\{(x_1,r_1),(x_2,r_2),\dots,(x_n,r_n)\})}$$
	where $r_i=y_i-H_t(x_i)$.
	
2. Reweight data by their errors, and train$$\mathcal A(\{(x_1, y_1,w_1),\dots,(x_n,y_n,w_n)\})$$
**Adaboost** uses method 2.

## Model Setup

1. Adaboost is useful for classification: $y_i\in\{+1,-1\} \quad (x_i\in\mathbb R^d)$.
2. $\alpha_t$ will be a non-constant. (It is no longer a hyperparameter)
3. $\ell(H)=\sum_{i=1}^n\exp(-y_iH(x_i))$. This is more sensitive to outliers, which in general isn't a good thing because outliers can easily blow up the error, but works here for boosting weak models.

**Goal:** 
$$\begin{align}\underset{h}{\arg\min}\;\ell(H_t+\alpha h_{t+1})
&=\underset{h}{\arg\min}\,\langle\nabla_H\ell,\vec h\rangle \\
\nabla_H\ell=\begin{bmatrix}\frac{\partial\ell}{\partial H(x_1)}\\\vdots\\\frac{\partial\ell}{\partial H(x_n)}\end{bmatrix}
&, \vec h=\begin{bmatrix}h_(x_1)\\\vdots\\h(x_n)\end{bmatrix} \\
\frac{\partial\ell}{\partial H(x_i)}&=-y_i\exp(-y_iH_t(x_i))\\
\end{align}$$
This gives our final minimization problem:
$$\underset{h+1}{\arg\min}\sum_{i=1}^n-yh_{t+1}(x_i)\exp(-y_iH_t(x_i))$$

## Derivation

We have a current ensemble $H_t$. We want to find $h_{t+1}$ using the above minimization problem.
$$\begin{align}
h_{t+1}&=\underset{h+1}{\arg\min}\sum_{i=1}^n-yh_{t+1}(x_i)\underbrace{\exp(-y_iH_t(x_i))}_{\triangleq \hat w} \\
\hat w&=\exp(-y_iH_t(x_i)) \\
z&=\sum_{i=1}^n\hat w_i \\
w_i&=\frac{\hat w_i}{z} \end{align}$$
To interpret this, $\hat w_i$ is the exponential "loss" for a given datapoint. Then, $w_i$ is the "normalized" version—the fraction $\hat w_i$ takes up of all $\hat w$. 
$$
\begin{align}
\implies h_{t+1}&=\underset{h_{t+1}}{\arg\min}\,\frac{-1}{z}\sum_{i=1}^ny_ih_{t+1}(x_i)\hat w_i \\
&=\underset{h+1}{\arg\min}-\sum_{i=1}^nw_i\underbrace{y_ih_{t+1}(x_i)}_{-1\text{ when wrong}} \\
&=\underset{h+1}{\arg\min}-\sum_{\mathclap{h_{t+1}(x_i)\neq y_i}}-w_i+\sum_{\mathclap{h_{t+1}(x_i)= y_i}}w_i
\end{align}$$

The key idea in the last step is to split up the wrong and right examples based on the fact that $y_ih_{t+1}(x_i))$ will be $+1,-1$ based on classification.
$$\begin{align}
h_{t+1}&=\underset{h+1}{\arg\min}\underbrace{\sum_{\rm wrong}w_i}_\epsilon+\sum_{\rm right}w_i \\
&=\underset{h+1}{\arg\min\;}\epsilon-(1-\epsilon) \\
&=\underset{h+1}{\arg\min\;}2\epsilon-1 \\
&=\underset{h+1}{\arg\min\;}\epsilon
\end{align}$$
Thus, minimizing for Adaboost is equivalent to minimizing the weighted training error, where the weights are initially equal and then are trained.

## Implementation

1. Train a logistic regressor where you weight the loss (by multiplying by $w$)
2. Given a weighted dataset 
	Then, you can just solve by bagging, where the bags are chosen based on the weight. A useful function is:
	```python
	torch.distributions.multinomial
	```

Given in iteration $t$, $H_t$ ($H_1=0)$
$$\begin{align}
\hline
&\textbf{Algorithm: Adaboost}\\
\hline
&\forall i, w_i=\frac12\exp(y_iH_t(x_i)) \\
&\text{Draw } \mathcal D_w=\{(\hat x_1, \hat y_1),\dots,(\hat x_n, \hat y_n)\}, \text{where points are drawn with probability } w_i \\ 
&h_{t+1}\gets\mathcal A(\mathcal D_w)\\
&H_{t+1}\gets H_t+\alpha^* h_{t+1} \\
\hline
\end{align}$$

## Finding $\alpha^*$ 

The remaining question is how to find $\alpha^*$. At this point, we already know $H_t, h_{t+1}$ from the algorithm.

$$\begin{align}
\alpha^*&=\underset{\alpha}{\arg\min\;}\ell(H_t+\alpha h_{t+1}) \\
&=\underset{\alpha}{\arg\min}\sum_{i=1}^n\exp(-y_i[\underbrace{H_t(x)}_{\rm const}+\alpha \underbrace{h_{t+1}(x_i)}_{\rm const}])
\end{align}$$
**Approach:** Differentiate with respect to $\alpha$, set to 0 and solve.

$\alpha^*=0.5\ln\frac\epsilon{1-\epsilon}$ in the hw
**Random forests** is a [supervised learning](Supervised%20Learning.md) algorithm based on [decision trees](Decision%20Trees.md). Random forests try to resolve the key issue with decision trees: that it's very easy to overfit (by creating a leaf for each datapoint).
## Bagging

>[!idea]
>The central idea of **bagging** (**b**ootstrap **agg**regat**ing**) is that if we have more data and take the average prediction, we'll be more likely to be closer to the true mean. In reality, there isn't more data, so we can simulate this by taking random samples from the dataset $\mathcal D$.
>
>That is, create new datasets $\mathcal D_1,\mathcal D_2, \dots, \mathcal D_T$ by randomly sampling $n$ points from $\mathcal D$ with replacement.

How do we know that these datasets won't have too much overlap?
$$\begin{align}
\Pr[\text{Pick $(x_i, y_i)$ first}]&=\frac1n \\
\Pr[\text{Never pick $(x_i, y_i)$}]&=\left(1-\frac1n\right)^n \\
\lim_{n\to\infty}\left(1-\frac1n\right)^n&=\frac1e\approx0.3678
\end{align}$$
This means that for any given datapoint, around 37% of the samples won't have that datapoint, meaning there's a pretty large chance that the datasets won't have overlap.

## Bagged Decision Trees

Random forests are essentially bagged decision tree, with one change:
1. From $\mathcal D$, make $\mathcal D_1, \dots, \mathcal D_T$ via bagging
2. On each $\mathcal D_t$, train a full-depth decision tree $h_{\mathcal D_t}$ (that is, with a good chance of overfitting)
3. $H(x)$ combines $h_{\mathcal D_1}, \dots, h_{\mathcal D_T}$
	1. For regression: $H(x)=\frac1T\sum_\limits{t=1}^Th_{\mathcal D_t}(x)$ (that is, the average score)
	2. For classification: $H(x)=\mathrm{mode}(h_{\mathcal D_1}(x), \dots, h_{\mathcal D_T}(x))$
4. **The (optional) twist.** Every split I make, consider only $k\leq d$ of the features, chosen randomly. (Note that when $k=d$, we're not applying this twist.) Scikitlearn uses $k=\sqrt d$ by default.

>[!hint]
>$T$ is chosen to be "as large as necessary." That is, with our train/validation split, we keep increasing $T$ until our error stops decreasing. 
>
>Note that there isn't a risk of overfitting here intuitively because we're taking averages and bagging is a form of "regularization."

## Advantages

1. **Scale invariance:** DTs don't care about feature scale
2. **Categories:** It's easy to use categorical features
3. **Out-of-bag (OOB) estimation:** For $x_i$, evaluate $H_{\lnot i}(x_i)$. Intuitively, since not every data point will be in every tree, we can look at the trees that don't use that point, and this serves as a sort of validation error.
4. **Uncertainty quantification:** 
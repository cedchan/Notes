Decision trees are a simple supervised learning model, where the model traverses a tree based on conditions on each node based on the input, until reaching a leaf, which has the prediction. 

Decision trees can also be visualized as partitioning the input space into different predictions.
## Training

Algorithm:
1. Pick a split for the root. A split ${\bf s}=(j, v)$, for feature $j$ and feature value $v$.
	$\mathcal D_{<\bf s}, \mathcal D_{>\bf s}$ denote the subsets of the dataset determined by $\bf s$. $$\begin{gather}\mathcal D_{<\bf s}=\{\vec x_i \mid x_{ij}<v\}\\
	\mathcal D_{>\bf s}=\{\vec x_i \mid x_{ij}>v\}
	\end{gather}$$
2. Recurse on $\mathcal D_{<\bf s}$ and $\mathcal D_{>\bf s}$.
3. Stop if 
	1. $|\mathcal D_{<\bf s}|=1|$
	2. You can't split the data anymore

### Deciding Splits

There are two main questions at play here:
1. Which splits do we try?
2. How do I score splits?

Along a particular axis in the space, the only splits worth trying lie in the middle between 2 datapoints, to maximize the margin. Thus, there are only $O(nd)$ possible splits total. Thus, we can just sort the data along each axis and go through each pair to try the split that lies between them.

#### Entropy

>[!definition]
>Given a random variable $X$, with values in the alphabet $\mathcal X$, distributed according to $p:\mathcal X\rightarrow[0,1]$, **entropy** is defined as $$H[X]=-\sum_{x\in\mathcal X}p(x)\log(x)=\mathbb E[-\log p(X)]$$

Here, we define $$H[\mathcal D_{<\bf s}]=-p_{<\bf s}\log p_{<\bf s}-(1-p)\log(1-p_{<\bf s})$$ Graphically, ![](Pasted%20image%2020231025144123.png)
We define the entropy of a split $\bf s$ is the weighted average of the entropies of the datasets it creates. That is, we want to find $H[\mathcal D_{<\bf s}], H[\mathcal D_{>\bf s}]$. 
$$H[{\bf s}]=\frac{|\mathcal D_{<\bf s}|}{|\mathcal D|}H[\mathcal D_{<\bf s}]+\frac{|\mathcal D_{>\bf s}|}{|\mathcal D|}H[\mathcal D_{>\bf s}]$$
Then, we define our optimal split ${\bf s}^*$ as
$${\bf s}^*=\underset{{\bf s}\in \mathcal S}{\arg\min\, } H[{\bf s}]$$
#### Gini Index

An alternative is the **Gini index**.

Here, we have $$G[\mathcal D_{<\bf s}]=p_{<\bf s}(1-p_{<\bf s})$$Graphically,
![](Pasted%20image%2020231025144634.png)
Same as with entropy, we find the Gini index of $\bf s$ with the weighted average of the Gini indexes of the split datasets.
$$G[{\bf s}]=\frac{|\mathcal D_{<\bf s}|}{|\mathcal D|}G[\mathcal D_{<\bf s}]+\frac{|\mathcal D_{>\bf s}|}{|\mathcal D|}G[\mathcal D_{>\bf s}]$$
## Regression Trees

Suppose a leaf has dataset $\mathcal D_{<\bf s}$, predict $$\overline y=\frac{1}{|\mathcal D_{<\bf s}|}\sum_\limits{y\in\mathcal D_{<\bf s}}y$$That is, take the average label. Now compute the squared loss:
$$\ell_{\rm sq}(\mathcal D_{<\bf s})=\sum_{y\in\mathcal D_{<\bf s}}(\overline y - y)^2$$From this we can compute the squared loss of the split itself, again using a weighted average of the split datasets:
$$\ell_{\rm sq}({\bf s})=\frac{|\mathcal D_{<\bf s}|}{|\mathcal D|}\ell_{\rm sq}(\mathcal D_{<\bf s})+\frac{|\mathcal D_{>\bf s}|}{|\mathcal D|}\ell_{\rm sq}(\mathcal D_{>\bf s})$$

## Regularization

One of the issues with just pure decision trees is that they will achieve 0% training error by carving out a specific space for each data point. Regularization limits this, which hopefully makes the model more general. There are a couple of methods for this.

1. **Depth limit**: The idea here is that the number of leaves grows exponentially (half of the nodes of a full binary tree are leaves), so even decreasing depth by a little will reduce the power of a model a great deal.
2. **Bagging**: A particular form of regularization that leads to random forests.
3. "**Boosting**": The idea here is similar to depth limiting, but it allows for more fine-tuned control over the regularization. This leads to gradient boosted trees.

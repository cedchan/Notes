**Input:** Dataset $D=\{(\vec x_1, y_1), (\vec x_2, y_2), \dots, (\vec x_n, y_n)\}$
- $\vec x_i\in \mathbb R^d$ are **feature vectors, inputs,** or **examples**
- $y_i \in \mathcal Y$ are **labels**

**Goal:** Produce a **model** $h$ such that $h(\hat x)\approx \hat y$
## Types of Supervised Learning Problems

### Binary Classification

>[!definition]
>**Binary classification** is a problem where the model has to decide between two options based on the input.

>**Example 1.** 
>- $\vec x_i$ is a vector representing a "flattened" image
>- $y_i\in \{-1, 1\}$, where 
>	- $y_i = 1 \implies \text{cat}$
>	- $y_i=-1 \implies \text{dog}$

### Regression

>[!definition]
>**Regression** is a problem where we predict a numerical value.

>**Example 2.** Zestimates
>- $\vec x_i$ consists of values like square footage, # bathrooms, zip code, 1 if has pool 0 if not, etc.
>- $y_i\in \mathbb R$ is the price in dollars

### Multiclass Classification

>[!definition]
>**Multiclass classification** is like binary classification, but there are more than two possible labels.

## Solving Supervised Learning Problems

Supervised machine learning models learn in the following manner:
$$\underbrace{X=n\begin{bmatrix}\vec x_1 \\ \vec x_2 \\ \vdots\\ \vec x_n\end{bmatrix}, y=n\begin{bmatrix}y_1 \\ y_2 \\\vdots \\ y_n\end{bmatrix}}_{\text{Training data}}\rightarrow \text{learning algorithm}\rightarrow\text{model } h$$
Learning goes on by defining some **loss function** $\ell(\hat y, y)$, and trying to minimize the **training error** $\hat R(h)$, which is based on the loss function.

### Error Functions
#### Error in Binary Classification

The binary classification loss function is just 0 if the prediction is incorrect and 1 otherwise.
$$\ell_{0/1}(\hat y, y)=\begin{cases}0 & \text{if } \hat y \neq y \\ 1 & \text{o.w.}\end{cases}$$

The training error, simply put, is the fraction of the data that is predicted correctly.
$$\hat R(h)=\frac{1}{n}\sum_{i=1}^n{\ell_{0/1}(h(x_i), y_i)}$$
#### Error in Regression

The low-hanging fruit might be to use the real the predicted values.
$$\ell_\text{terrible}(\hat y, y)=\hat y-y$$
The issue with this is that we can get negative values. Instead, the commonly accepted solution is to instead use the squared error.
$$\ell_\text{sq}(\hat y, y)=(\hat y-y)^2$$
$$\hat R(h)=\frac1n\sum_{i=1}^n\ell_\text{sq}(h(x_i),y(i))$$
This is referred to as the **training mean squared error (MSE)**.

### Generalization

The following model simply memorizes the dataset.
$$h_\text{mem}(x)=\begin{cases}y_i & \text{if } x=x_i \\ 1 & \text{o.w.}\end{cases}$$
Training error will always be 0, but it can't generalize to new data, which is the point of ML models.

To generalize to new data, we must assume that all data is drawn **iid (independent and identically distributed)** from some distribution $\mathcal P$. 
$$(\vec x_i, y_i) \stackrel{\mathrm{iid}}{\sim} \mathcal P$$
The problem with $h_\text{mem}$ is that it samples well from $D$, the dataset, but not $P$ the overall distribution.

>[!definition]
>The **empirical risk** $\hat R(h)$ is the loss on the dataset $\mathcal D$ (that is, the training error). The **true risk** $R(h)$ is the expectation of loss on the true distribution $\mathcal P$:
>$$\mathbb E_{(\vec x_i, y_i)\sim P}[\ell(h(x_i), y_i)]$$

The key assumption is that the empirical risk is a good estimate of the true risk (by the weak law of large numbers).

#### Generalization Gap

>[!definition]
>The **generalization gap** is the difference between the empirical risk and the true risk.
>$$R(h)-\hat R(h)$$

It appears in this tautology:
$$\underbrace{R(h)-\hat R(h)}_{\substack{\text{Generalization} \\ \text{gap}}}+\underbrace{\hat R(h)}_{\substack{\text{Training} \\ \text{error}}}=R(h)$$

#### Estimating the Generalization Gap

Say I collect $\hat{\mathcal D}=\{(\hat x_1, \hat y_1), \dots, (\hat x_m, \hat y_m)\}$. Then $\frac1m\sum_{i=1}^m\ell(h(\hat x_i), \hat y_i)\approx R(h)$.

The key here is that $\hat{\mathcal D}$ and $\mathcal D$ are different. In practice, this means we take our dataset and partition it into **training** and **testing** sets (e.g., in an 80:20 split).

### Classifiers

What is the best possible classifier? We can take our distribution and make it into a conditional distribution. We ask: Given $h$, what is the expected risk?

$$\begin{align}
\mathbb E_{P(y\mid x)}[\ell_{0/1}(h(x), y)]&=\Pr(y=-1\mid x)\mathbb 1(h(x)=+1)+\Pr(y=+1)\mathbb 1(h(x)=-1)
\end{align}$$

$$\begin{align}
P(x, y)&=h(y\mid x)p(x) \\
R(h)&=\mathbb E_{(x, y)\sim \mathcal P}[\ell_{0/1}(h(x), y)] \\
&=\mathbb E_{y\mid x}[\ell_{0/1}(h(x), y)] \\
&=\mathbb E_x\big[\Pr(y=1\mid x)\mathbb 1(h(x)=0)+\Pr(y=0\mid x)\mathbb 1(h(x)=1)\big] \\
&\qquad \text{where } \mathbb 1(h(x)=a)=\begin{cases}1 & h(x)=a \\ 0 & \text{o.w.}\end{cases}
\end{align}$$
From this we get the best possible classifier: the **Bayes Optimal Classifier**
$$h^*(x)=\begin{cases}+1 & \Pr(y=1\mid x)>0.5 \\ -1 & \text{o.w.}\end{cases}$$

>[!error]
>Review what is going on here


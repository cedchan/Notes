Recall that the basic idea of dimensionality reduction is $$x_i\in\mathbb R^D\rightarrow f(x_i)\rightarrow z_i\in\mathbb R^d\rightarrow g(z_i)\rightarrow\hat x_i$$ where we do the minimization $$\underset{f,\,g}{\arg\min\,}\|\hat x_i-x_i\|^2$$
That is, the function $f$ will map our vector of $D$ dimensions to a space of $d<D$ dimensions, and the function $g$ will convert this transformed vector back to the original space, as best as possible. The idea is that we not only want to reduce the dimensions, but we want to do so in a way that captures most of the information in the data, measured by how well we can go back to the original data.

## PCA Format

For PCA, we have the following functions:
- $f(x)=Qx, Q\in \mathbb R^{d\times D}$
- $g(z)=Q^\top z, Q^\top\in\mathbb R^{D\times d}$
- $\hat x=Q^\top\underbrace{Qx}_{f(x)}=g(f(x))$

Recall from linear algebra:

>[!definition]
>A **basis** of a vector space $V$ is a linearly independent subset of $V$ that spans $V$.
>

Where our basis is $\{\vec q_1, \vec q_2, \dots, \vec q_D\}$, we can write $x\in\mathbb R^D$ as $$x=a_1\vec q_1+a_2\vec q_2 +\dots+a_D\vec q_D$$
which PCA translates into a new basis to get $$z=a_1\vec q_1+\dots+a_d\vec q_d$$
The simplest way of doing this might be to simply drop $a_{d+1}\vec q_{d+1}+\dots+a_D\vec q_D$. Then, the lossiness of this reduction is just dependent on how much information in dimensions $[d+1..D]$. 

For PCA, we want to minimize that lossiness by maximizing the variance of the data in the new basis, because this means that we've captured the most information possible. But how do we find this new basis?

Given dataset 
$$z_1, \dots,z_n$$
with 0 mean, the unbiased sample variance is
$$s^2=\frac1{n-1}\sum_{i=1}^nz_i^2$$
Suppose $z_i=x_i^\top q_1$. Then we can rewrite the sample variance as
$$s^2=\frac1{n-1}\sum_{i=1}^n(x_i^\top q_1)^2=\frac{1}{n-1}\|Xq_1\|^2$$
We want to find, then,$$q_1^*=\underset{q_1}{\arg\min\,}\frac1{n-1}q_1^\top X^\top Xq_1=\underset{q_1,\,\|q_1\|=1}{\arg\max\,}q_1^\top S q_1$$where $S$ is the covariance matrix $\frac{1}{n-1}X^\top X$. 

Using Lagrange multipliers to solve this problem, we make this a minimization problem first by making the expression negative and solve $$\mathcal L(q_1,\lambda)=-q_1^\top Sq_1+\lambda(q_1^\top q_1-1)$$
$$\begin{align}
Sq_1&=\lambda q_1 \\
q_1^\top\underbrace{Sq_1}_{\lambda q_1}&=\lambda q_1^\top q_1=\lambda
\end{align}$$
Then we have a naive implementation of PCA:
1. $x_i\gets x_i-\overline x, \overline x=\frac1n\sum_{i=1}^nx_i$
2. $S=\frac{1}{n-1}X^\top X$
3. Keep $q_1, \dots, q_d$ as leading eigenvectors. $S=Q\Lambda Q^\top$, taking $Q[:,:d]$ as your projection.

Then, our loss for a given vector is $$\|\hat x_i-x_i\|^2=\sum_{j=d+1}^D((x^\top_iq_j)q_j)^2$$
It follows that our total loss is this, for each $i$:
$$\sum_{i=1}^n\sum_{j=d+1}^D(x_i^\top q_j)^2=\sum_{j=d+1}^Dq_j^\top X^\top Xq_j=\sum_{j=d+1}^Dq_j^\top Sq_j$$
An alternative interpretation of PCA, then, is to minimize this value.

This form looks a lot like the expression we tried to maximize earlier. The idea is that in our first interpretation, maximizing the variance, we want to maximize this quantity to make the basis vectors we keep as important as possible. Then in this second interpretation, where we minimize the variance in the vectors we throw away.

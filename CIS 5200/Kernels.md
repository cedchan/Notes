
Linear models: $h(z)=w^\top z$
Define: feature map $\phi(z)$
Kernel $\underbrace{k(x, z)}_{O(d)}=\underbrace{\phi(x)}_{O(2^d)}\,^\top\phi(z)$

## Radial Basis Function (Gaussian) Kernel

This is probably the most commonly used kernel.

>[!definition]
>The **Radial Basis Function (Gaussian) Kernel** is defined as follows:
>$$k_{\rm RBF}(x, z)=\exp\left(\frac{-\|x-z\|_2^2}{2\sigma^2}\right)$$

Note that $\|x-z\|_2^2$ is the squared distance between $x, z$, so
- As $x, z$ get close, $k(x, z)\rightarrow 1$
- As $x, z$ get far, $k(x, z)\rightarrow 1$

$\sigma$ is a hyperparameter. Making $\sigma$ smaller means that only close points will matter. At large values of $\sigma$, it's like KNN with $k=n$. It can be thought of like a softer KNN using similarity. 

For every training point $x_i$, we calculate some notion of similarity—namely, the kernel (in the equation, $\alpha$)—and in testing each point gets a "vote" based on similarity, weighted by distance.

## Kernel Ridge Regression

$$\mathcal L(w)=\sum_{i=1}^n(w^\top x_i-y_i)^2+\lambda\|w\|_2^2$$

Two steps:
1. Replace $x_i$ with $\phi(x_i)$, $w$ with $\sum_{i=1}^n\alpha_i\phi(x_i)$
$$\mathcal L(\alpha)=\sum_{i=1}^n\left(\sum_{j=1}^n\alpha_i\underbrace{\phi(x_j)^\top\phi(x_i)}_{k(x_j,x_i)}-y_i\right)^2+\underbrace{\lambda\sum_{i=1}^n\sum_{j=1}^n\alpha_i\alpha_j\phi(x_i)^\top\phi(x_j)}_{w^\top w}$$
2. Then, plugging in the kernel definition, we have
	$$\mathcal L(\alpha)=\sum_{i=1}^n\left(\sum_{j=1}^n\alpha_ik(x_j,x_i)-y_i\right)^2+\lambda\sum_{i=1}^n\sum_{j=1}^n\alpha_i\alpha_j k(x_i,x_j)$$
## Ridge Regression Take 2

We start with a matricized version of the loss
$$\mathcal L(w)=\|Xw-y\|_2^2+\lambda w^\top w$$
We use the trick $w\rightarrow\sum_{i=1}^n\alpha_ix_i=X^\top\alpha$ to get
$$\mathcal L(\alpha)=\|XX^\top\alpha-y\|_2^2+\lambda\alpha^\top XX^\top\alpha$$
$$\mathcal L(\alpha)=\|K\alpha-y\|_2^2+\alpha\alpha^\top K\alpha$$where $K$ is the **kernel matrix** such that $K_{ij}=k(x_i,x_j)$.

Now we can optimize the expression
$$\min_\alpha\|K\alpha-y\|_2^2+\lambda\alpha^\top K\alpha$$
Applying the derivative we have
$$\begin{align}
\cancel2(K\alpha-y)K+\cancel2\alpha K\alpha&=0 \\
K^2\alpha-Ky+\lambda K\alpha&=0 \\
K^2\alpha+\lambda K\alpha&=Ky \\
K(K\alpha+\lambda I\alpha)&=Ky \\
(K\alpha+\lambda I\alpha)&=y \\
(K+\lambda I)\alpha&=y \\
\alpha^*&=(K+\lambda I)^{-1}y
\end{align}$$
Recall that the closed-form solution of ordinary ridge regression is $$w^*=(XX^\top+\lambda I)^{-1}y$$
As we can see, the kernelized version is just kernalizing the closed-form solution too.
A
### Methods for Showing Valid Kernels

1. $\underbrace{k_3(x, x')}_{\phi_3}=\underbrace{k_1(x,x')}_{\phi_1}+\underbrace{k_2(x,x')}_{\phi_2}$. Show that there exists $\phi_3$ that maps to $\phi_1+\phi_2$.
2. $k(x, x')$ is a valid kernel iff $K$ is PSD.
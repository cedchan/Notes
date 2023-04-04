
## Definition 

The inner product is a generalization of the dot product. It multiplies two vectors to result in a scalar. The notation is shown below:
$$\langle \cdot,\cdot\rangle: V\times V \rightarrow \mathbb{R}$$

Properties for a real vector space:
1. $\langle\vec{u}, \vec{v}\rangle=\langle\vec{v},\vec{u}\rangle$
2. $\langle\vec{u},\lambda_1\vec{v}_1+\lambda_2\vec{v}_2\rangle=\lambda_1\langle\vec{u},\vec{v}_1\rangle+\lambda_2\langle\vec{u},\vec{v}_2\rangle$
3. $\forall \vec{v}\neq\vec{0}, \langle\vec{v},\vec{v}\rangle>0$

(Note that property 2 can be expanded into two properties: scalar multiplication and linearity.)

Extensions:
1. $\langle\vec{v},\vec{0}\rangle=\vec{0}$ 
	Proof:
$$
\begin{align}
\langle\vec{v},\vec{0}\rangle&=\langle\vec{v},\vec{0}-\vec{0}\rangle\\
&=\langle\vec{v},\vec{0}\rangle-\langle\vec{v},\vec{0}\rangle \\
&=\vec{0}
\end{align}
$$
2. $\langle\lambda_1\vec u_1+\lambda_2\vec u_2, \vec v\rangle=\lambda_1\langle\vec u_1, \vec v\rangle+\lambda_2\langle\vec u_2, \vec v\rangle$ (follows from property 2)
3. Cauchy's Inequality
	$\langle\vec u, \vec v\rangle^2\leq\langle \vec u, \vec u\rangle\langle\vec v, \vec v\rangle$
	$|\vec u \cdot \vec v| \leq ||\vec u|| \cdot ||\vec v||$

>**Example.** $\mathbb{R}^2$ dot product

>**Example.** $M_{2\times2}(\mathbb{R}), \langle\cdot,\cdot\rangle$
>$$
\begin{align}
\langle A,B\rangle&=(A^TB) \\
\left\langle\begin{pmatrix}a&b\\ c&d\end{pmatrix},
\begin{pmatrix}a&b\\ c&d\end{pmatrix}\right\rangle&=a^2+b^2+c^2+d^2
\end{align}$$

>[!danger]
>There was something before the $(A^TB)$ that I didn't catch.

## Functions

The definition of the inner product of functions on $[0, 2\pi]$.
$$\langle f,g\rangle=\frac{1}{2\pi}\int_0^{2\pi}f(x)g(x)dx$$

## Orthonormal Basis

An **orthonormal basis** of $V$ with respect to $\langle\cdot,\cdot\rangle$ is $\mathcal{R}=\{\vec{v}_1,\vec{v}_2,\dots,\vec{v}_n\}$ such that 
1. $\langle\vec{v}_i,\vec{v}_i\rangle=1$ (i.e., they each vector in a unit/normal vector)
2. $\langle\vec v_i, \vec v_j\rangle=0$ (i.e., each vector is orthogonal)

>**Example.** The Fourier Space
>$\left\{\frac{1}{\sqrt{2}},\cos x, \sin x, \cos 2x, \sin 2x, \dots \right\}$ is an orthonormal basis that spans all functions.

An orthonormal basis, like with typical numerical vectors, can be found by using the Gram-Schmidt process. 

## Definition 

The inner product is a generalization of the dot product. It multiplies two vectors to result in a scalar. The notation is shown below:
$$\langle \cdot,\cdot\rangle: V\times V \rightarrow \mathbb{R}$$
Properties for a real vector space:
1. $\langle\vec{u}, \vec{v}\rangle=\langle\vec{v},\vec{u}\rangle$
2. $\langle\vec{u},\lambda_1\vec{v}_1+\lambda_2\vec{v}_2\rangle=\lambda_1\langle\vec{u},\vec{v}_1\rangle+\lambda_2\langle\vec{u},\vec{v}_2\rangle$
3. $\forall \vec{v}\neq\vec{0}, \langle\vec{v},\vec{v}\rangle>0$

(Note that property 2 can be expanded into two properties: scalar multiplication and linearity.)

Corollaries:
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
4. $\langle \vec u, \vec v \rangle = \vec 0 \implies \vec u \perp \vec v$

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

### Functions

The definition of the inner product of functions on the domain $[a, b]$.
$$\langle f,g\rangle=\int_a^{b}f(x)g(x)dx$$

## Inner Product on Complex Vector Spaces

Recall the definition of the [inner product](Transformations.md#Inner%20Product). For complex vector spaces, we say
$$\langle\cdot , \cdot \rangle:V\times V\rightarrow \mathbb C$$

Consider the complex vector space $\mathbb C^n$, and two vectors in it 
$$
\vec u=\begin{pmatrix} z_1 \\ \vdots \\ z_n \end{pmatrix}, 
\vec v=\begin{pmatrix} w_1 \\ \vdots \\ w_n \end{pmatrix}
$$
Then we have the following inner products
$$
\begin{align}
\langle\vec u, \vec v\rangle&=\overline{z_1}w_1+\overline{z_2}w_2+\dots+\overline{z_n}w_n \\
\langle\vec u,\vec u\rangle&=\overline{z_1}z_1+\overline{z_2}z_2+\dots+\overline{z_n}z_n \\
&=|z_1|^2+|z_2|^2+\dots+|z_n|^2
\end{align}
$$
From this, we can conclude that the magnitude (norm) of $\vec u$ is given by
$$||\vec u||=\sqrt{\langle\vec u, \vec u\rangle}\geq 0$$
### Properties

1. $\langle\vec u, \vec v\rangle = \overline{\langle\vec v, \vec u\rangle}$
2. $\langle\vec u,\lambda_1\vec v_1+\lambda_2\vec v_2\rangle=\lambda_1\langle\vec u,\vec v_1\rangle+\lambda_2\langle\vec u,\vec v_2\rangle$
3. $\vec u \neq \vec 0\implies\langle \vec u,\vec u\rangle>0$

(Note that the inner product of any vector with $\vec 0$ is $\vec 0$.)

>**Example.** $\vec v_1=(i, 1)^T, \vec v_2=(-i, 1)^T$.
>$${\begin{align}
\langle\vec v_1,\vec v_1\rangle&=\overline{i}\cdot i+\overline 1\cdot 1 \\
&=(-i)i+1\cdot 1 \\
&=2 \\
||\vec v_1||&=\sqrt{2} \\
\langle\vec v_1,\vec v_2\rangle&=\overline{i}(-i)+\overline1\cdot 1 \\
&=(-i)^2+1=0 \\
\therefore \vec v_1 &\perp \vec v_2
\end{align}}$$

### Complex Functions

The definition of the inner product of complex functions on the domain $[a, b]$.
$$\langle f,g\rangle=\int_a^{b}\overline{f(x)}g(x)dx$$

## Orthonormal Basis

An **orthonormal basis** of $V$ with respect to $\langle\cdot,\cdot\rangle$ is $\mathcal{R}=\{\vec{v}_1,\vec{v}_2,\dots,\vec{v}_n\}$ such that 
1. $\langle\vec{v}_i,\vec{v}_i\rangle=1$ (i.e., they each vector in a unit/normal vector)
2. $\langle\vec v_i, \vec v_j\rangle=0$ (i.e., each vector is orthogonal)

>**Example.** The Fourier Space
>$\left\{\frac{1}{\sqrt{2}},\cos x, \sin x, \cos 2x, \sin 2x, \dots \right\}$ is an orthonormal basis that spans all functions.

An orthonormal basis, like with typical numerical vectors, can be found by using the Gram-Schmidt process. 
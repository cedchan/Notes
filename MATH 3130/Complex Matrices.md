
>**Example.** Consider the following matrix: $$A=\begin{pmatrix}0 & -1\\1 & 0\end{pmatrix}$$
>which represens a 90-degree counterclockwise rotation. When we solve for the eigenvalues, we get $\lambda=\pm i$, which results in eigenvectors $\vec v_1=(i, 1)^T$ and $\vec v_2=(-i,1)^T$.
>
>Now let's diagonalize. $$P=\begin{pmatrix}i & -i \\1 & 1\end{pmatrix}, J=\begin{pmatrix}i & 0 \\0 & -i\end{pmatrix}$$

Clearly, complex numbers are unavoidable both in diagonalizing certain matrices and finding their eigenvalues/eigenvectors.

## Complex Numbers

>[!definition]
>We denote the set of **complex numbers** as $$\mathbb C=\{a+bi\mid a, b \in \mathbb R\}$$

The basic operations for complex numbers include addition, multiplication, complex conjugation, magnitude, and angle.

### Geometry of Complex Numbers

The **magnitude** of a complex number is given by 
$$\begin{align}
|a+bi|&=\sqrt{(a+bi)(a-bi)} \\
&=\sqrt{a^2+b^2}
\end{align}$$

Its **angle** (in the imaginary plane) is given by $$\theta=\tan^{-1}\frac{b}{a}$$
>[!equation]
>Given the angle and magnitude of a complex number, we can rewrite it as $$a+bi=re^{i\theta}$$

### Multiplication

Consider two imaginary numbers $z_1=r_1e^{i\theta_1}$ and $z_2=r_2e^{i\theta_2}$. Then their multiplication is
$$\begin{align}
z_1z_2&=r_1r_2e^{i\theta_1}e^{i\theta_2} \\
&=r_1r_2e^{i(\theta_1+\theta_2)}
\end{align}$$
Thus, geometrically, the product of two complex numbers has a magnitude equal to the product of the input magnitudes, and an angle equal to the sum of the input angles.

### Complex Conjugation

The **complex conjugation** of an imaginary number is defined as$$\overline{a+bi}=a-bi$$
## Euler's Formula

>[!equation]
>$$e^{i\theta}=\cos\theta+i\sin\theta$$

**Euler's formula** is helpful in calculating the complex conjugate of numbers in the form $e^{nix}$, which will later be used to show that can form orthonormal bases. 

The complex conjugate of $re^{nix}$:
$$\begin{align}
\overline{e^{nix}}&=\overline{\cos\theta+i\sin\theta} \\
&=\cos\theta-i\sin\theta \\
&=e^{-nix}
\end{align}$$

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

Consider two complex functions $f, g:[0,2\pi]\rightarrow\mathbb C$. Their inner product is defined as 
$$\langle f, g\rangle=\frac1{2\pi}\int_0^{2\pi}\overline{f(x)}g(x)dx$$
which follows from the ordinary definition of the [inner product of functions](Inner%20Product.md#Functions).

>**Example.** Find the inner product of $e^{ix}$ with itself.

>[!solution]+
>$${\begin{align}
\langle e^{ix},e^{ix}\rangle&=\frac1{2\pi}\int_0^{2\pi}\overline{e^{ix}}e^{ix}dx \\
e^{ix}&=\cos x+i\sin x \\
\overline{e^{ix}}&=\cos x -i\sin x \\
\langle e^{ix},e^{ix}\rangle&=\frac1{2\pi}\int_0^{2\pi}1dx \\
&=1
\end{align}}$$

>**Example.** Find the inner product of 1 with $e^{ix}$.

>[!solution]+
>$${\begin{align}
\langle1,e^{ix}\rangle&=\frac1{2\pi}\int_0^{2\pi}\overline1e^{ix}dx \\
&=0
\end{align}}$$
Again note that this means $1\perp e^{ix}$.

## The Fourier Series

### An Orthogonal Basis

We first want to show that the set $\{e^{nix}\}$ forms an orthogonal basis. We do this by showing generally that $\langle e^{aix}, e^{bix} \rangle=0$. 

$$\begin{align}
\langle e^{aix},e^{bix}\rangle&=\frac1{2\pi}\int_0^{2\pi}e^{-aix}e^{bix}dx \\
&=
\end{align}$$

### The Fourier Transform

Consider some function $f$ defined on 
$$f:[0,2\pi]\rightarrow \mathbb C$$
From our exploration of the inner product of complex numbers, we know that we can form an [orthogonal basis](Inner%20Product.md#Orthonormal%20Basis) using functions in the set $\{e^{nix}\}$. We can therefore rewrite $f$ as a linear combination of an orthogonal basis formed by $\{e^{nix}\}$, with **Fourier coefficients** $c_n\in \mathbb C$. 
$$f=\sum_{n=-\infty}^\infty c_ne^{nix}$$
So how do we find the coefficients? We can use the formula
$$\begin{align}
c_n&=\langle e^{nix},f(x)\rangle \\
&=\frac1{2\pi}\int_0^{2\pi}e^{-nix}f(x)dx
\end{align}$$
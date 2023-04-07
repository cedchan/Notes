
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
>where $r$ is its magnitude and $\theta$ its angle from the $x$-axis in the complex plane.

### Multiplication

Consider two imaginary numbers $z_1=r_1e^{i\theta_1}$ and $z_2=r_2e^{i\theta_2}$. Then their multiplication is
$$\begin{align}
z_1z_2&=r_1r_2e^{i\theta_1}e^{i\theta_2} \\
&=r_1r_2e^{i(\theta_1+\theta_2)}
\end{align}$$
Thus, geometrically, the product of two complex numbers has a magnitude equal to the product of the input magnitudes, and an angle equal to the sum of the input angles.

### Complex Conjugation

The **complex conjugation** of an imaginary number is defined as$$\overline{a+bi}=a-bi$$
## The Conjugate Transpose

>[!definition]
>The **conjugate transpose** $A^H$ (also denoted as $\overline{A}^T, A^*, A^+$) of a matrix $A$ is the element-wise complex conjugate of $A^T$. 
>
>For a $2\times2$ matrix $A=\begin{pmatrix}a & b \\ c & d\end{pmatrix}$,
>$$A^H=\begin{pmatrix}\overline a & \overline c \\ \overline d & \overline d\end{pmatrix}$$

### Properties
1. $(A^H)^H=A$
2. $\langle \vec u, A\vec v\rangle=\langle A^H\vec u, \vec v\rangle$
	*Proof:* 
	$$\begin{align}
	\text{LHS}=\left\langle\begin{pmatrix}z_1 \\ z_2\end{pmatrix},
	\begin{pmatrix}aw_1+bw_2 \\ cw_1+dw_2 \end{pmatrix}\right\rangle
	&=a\overline{z_1}w_1+b\overline{z_1}w_2+c\overline{z_2}w_1+d\overline{z_2}w_2 \\
	\text{RHS}=\left\langle\begin{pmatrix}\overline az_1+\overline cz_2 \\
	\overline bz_1+\overline dz_2\end{pmatrix},
	\begin{pmatrix}w_1,w_2\end{pmatrix}
	\right\rangle &= a\overline{z_1}w_1+c\overline{z_2}w_1+b\overline{z_1}w_2+d\overline{z_2}w_2
	\end{align}$$
3. $\langle\vec u, A^H\vec v\rangle=\langle A\vec u, \vec v\rangle$.
	*Proof:*
	$$\begin{align}
	B&=A^H \\
	\langle \vec u, A^H\vec v\rangle &= \langle B^H\vec u, \vec v\rangle \\
	&=\langle(A^H)^H\vec u, \vec v\rangle \\
	&=\langle A\vec u, \vec v\rangle
	\end{align}$$

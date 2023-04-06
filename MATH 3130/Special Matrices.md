
## Orthogonal Matrices

>[!definition]
>**Orthogonal matrices** are matrices that satisfy $A^T=A^{-1}$ and $A^TA=I$. Geometrically, their columns are
>1. Normalized (i.e., have a norm of 1)
>2. Mutually orthogonal

## Symmetric Matrices

>[!definition]
>**Symmetric matrices** are matrices that satisfy $A^T=A$.

### Properties
1. Symmetric matrices are always diagonizable by an orthogonal matrix

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

## Hermitian Matrices

>[!definition]
>**Hermitian matrices** are complex matrices such that $A^H=A$. They are analogous to symmetric matrices in the real space.
>
>$A$ is Hermitian $\iff\langle A\vec u, \vec v\rangle=\langle\vec u, A\vec v\rangle$ (follows from [properties of conjugate transpose](Special%20Matrices.md#The%20Conjugate%20Transpose#Properties)).

From the second definition, it is clear that Hermitian matrices make the most sense on spaces with a defined inner product.

>**Example.** $A=\begin{pmatrix}5 & 2+i \\ 2-i & 3\end{pmatrix}$
>We can verify this by checking that $A^H=A$.

>**Example.** Pauli's Matrices
>3 matrices that help measure angular momentum in quantum physics.
>1. $\sigma_x=\begin{pmatrix}0 & 1 \\ 1 & 0\end{pmatrix}$
>2. $\sigma_y=\begin{pmatrix}0 & -i \\ i & 0\end{pmatrix}$
>3. $\sigma_z=\begin{pmatrix}1 & 0 \\ 0 & -1\end{pmatrix}$

### Properties
1. The eigenvalues of $A$, a Hermitian matrix, are always real
2. There exists a unitary $P$ such that
$$P^HAP=\begin{pmatrix}
\lambda_1 & 0 &\cdots &0 \\ 
0 & \lambda_2 & \ddots& \vdots \\
\vdots & \ddots& \ddots& 0\\
0 & \cdots & 0 & \lambda_n
\end{pmatrix}$$
3. All physics observables are Hermitian matrices

## Unitary Matrices

>[!definition]
>**Unitary matrices** are complex matrices that satisfy $A^H=A^{-1}$ and $A^HA=I$. They are analogous to orthogonal matrices in the real space.
>
>$A$ is unitary $\iff \langle A\vec u, A\vec v\rangle=\langle \vec u, \vec v\rangle$ (follows from [properties of conjugate transpose](Special%20Matrices.md#The%20Conjugate%20Transpose#Properties)).

From the second definition, it is clear that Hermitian matrices make the most sense on spaces with a defined inner product, just as with Hermitian matrices.

### Properties
1. $||A\vec u||=||\vec u|| \iff \langle A\vec u, A\vec v\rangle=\langle \vec u, \vec v\rangle$


## Orthogonal Matrices

>[!definition]
>**Orthogonal matrices** are matrices that satisfy $A^T=A^{-1}$ and $A^TA=I$. Geometrically, their columns are
>1. Normalized (i.e., have a norm of 1)
>2. Mutually orthogonal

### Properties
1. $\det A=\pm 1$ 

## Symmetric Matrices

>[!definition]
>**Symmetric matrices** are matrices that satisfy $A^T=A$.

### Properties
1. Symmetric matrices are always diagonizable by an orthogonal matrix

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

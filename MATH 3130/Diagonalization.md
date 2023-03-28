
## Jordan Canonical Form

Suppose we have a [transformation](Transformations.md) $T: V\rightarrow V$, whose matrix with respect to basis $\mathcal B$ is $A$. How do we find the Jordan Canonical Form?

The **Jordan canonical form** is $J$ such that the diagonal from $(0,0)$ to $(n, n)$ is filled, while all other values are $0$. We can decompose a matrix into such a form iff it is diagonalizable.
$$
J=\begin{pmatrix}
J_1 & 0 & \cdots & 0 \\
0 & J_2 & & \vdots \\
\vdots & & \ddots & 0\\
0 & \cdots& 0& J_n
\end{pmatrix}
$$

When a matrix $A$ is indeed diagonizable, we can decompose it in the diagonal form
$$
A=PJP^{-1}
$$
where $P$ consists of the eigenvectors and $J$ is a diagonal matrix (in Jordan canonical form) such that the eigenvalues are along the diagonal and correspond with the eigenvectors in $P$.
$$
\begin{align}
P&=\begin{pmatrix}
\vert & \vert & \cdots & \vert \\
\vec v_1 & \vec v_2 & \cdots & \vec v_n \\
\vert & \vert & \cdots & \vert
\end{pmatrix}\\\\
J&=\begin{pmatrix}
\lambda_1 & 0 & \cdots & 0 \\
0 & \lambda_2 & & \vdots \\
\vdots & & \ddots \\
0 & & & \vec v_n
\end{pmatrix}
\end{align}
$$
**Example.** $A=\begin{pmatrix}0 & 1 \\ 1 & 0\end{pmatrix}=PJP^{-1}$

>[!solution]+
We first solve for the eigenvalues.
>$${
\begin{align}
0&=|A-\lambda I|\\
&=\begin{vmatrix}
-\lambda & 1\\
1 & -\lambda
\end{vmatrix} \\
&=\lambda^2-1 \\
\lambda=1&,\lambda=-1
\end{align}}$$
Then, solving for the eigenvectors (not shown),
>$${\begin{align}
v_1&=(1,1) \\
v_2&=(1,-1) \\
P&=\begin{pmatrix}
1 & 1 \\
1 & -1
\end{pmatrix}\\
J&=\begin{pmatrix}
1 & 0\\
0 & -1
\end{pmatrix} \\
A&=PAP^{-1}
\end{align}
}$$

## Jordan Block

When the matrix is not diagonizable, we take a similar, but slightly different approach. Again, the diagonal is composed of eigenvalues $\lambda_i$, but this time with $1$s above to each repeated eigenvalue, we call this for the **Jordan block** $J_i$. 
$$
J_i=\begin{pmatrix}
J_1 & 1 & 0 & \cdots & 0 \\
0 & J_2 & 1 & \ddots & \vdots \\
\vdots & & \ddots& \ddots & 0\\
& & & J_{n-1} & 1\\
0 & \cdots & & 0& J_n
\end{pmatrix}
$$
In the Jordan block, each eigenvalue appears as many times as its geometric multiplicity. For all generalized eigenvalues, a $1$ appears above it in the block.

>**Example.** $A=\begin{pmatrix}1 & 1\\-1 & -1\end{pmatrix}=PJ_iP^{-1}$. 

>[!solution]+
>Again, we start by solving for the eigenvalues and eigenvectors of $A$. 
>$${\begin{align}
|A-\lambda I|&=0\\
&=\lambda^2 \\
\lambda &=0 \\
A\vec v_1&=\vec 0 \\
\vec v_1&=(1,-1)
\end{align}}$$
>But we need another eigenvector to cover 2 dimensions, so we use the generalized eigenvector.
>$${
\begin{align}
A\vec v_2&=\vec v_1 \\
\vec v_2 &=(0, 1)
\end{align}}$$
>Then we put it all together in block form.
>$${\begin{align}
P&=\begin{pmatrix}
1 & 0 \\
-1 & 1
\end{pmatrix} \\
J_i&=\begin{pmatrix}
0 & 1 \\
0 & 0
\end{pmatrix}
\end{align}}$$
>We see for $J_i$ that the diagonals are the eigenvalues. Here, we have $\lambda=0$, with geometric multiplicity 1 (we could only get 1 eigenvector from it) but algebraic multiplicity 2 (in the [characteristic polynomial](Math.md#Linear%20Algebra#Characteristic%20Polynomial), the term corresponding to this eigenvalue is to the power of two, $\lambda^2$). The $1$ appears above the second one because it was used to derive a generalized eigenvector.

## Finding a Diagonal Basis

One of the previously mentioned applications of performing a [change of base](Transformations.md#Change%20of%20Basis) is to find a new basis in which a non-diagonal matrix $A$ becomes diagonal. We can do this by using the diagonalization decompositions described above.

Consider the decomposition
$$A=PJP^{-1}$$
Clearly, it bears close resemblance to the change of basis equation
$$A_{\mathcal{B}_2\mathcal{B}_2}=P_{\mathcal B_2\mathcal B_1}A_{\mathcal{B}_1\mathcal{B}_1}P_{\mathcal B_2\mathcal B_1}^{-1}$$
The one difference is that the "new" and "old" bases are flipped. $A$ in our diagonalization is the old basis, whereas it is the new one in the second equation. Thus, we conclude that our transition matrix from old to new is in fact $P^{-1}$. Using the equation for a [transition matrix](Transformations.md#Linear%20Transformations#Transition%20Matrices), $P=\mathcal B_2^{-1}\mathcal B_1$, we can derive our basis
$$
\begin{align}
P^{-1}&=\mathcal B_2^{-1}\mathcal B_1 \\
\mathcal B_2P^{-1}&=\mathcal B_1 \\
\mathcal B_2 &=\boxed{\mathcal B_1P}
\end{align}
$$
>[!equation]
>The matrix $A$ is diagonal in the basis $\mathcal B_2$, where$${
\begin{align}
A&=PJP^{-1} & \text{(Jordan diagonalization)} \\
\mathcal B_2&=\mathcal B_1P
\end{align}
}$$

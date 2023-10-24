>[!theorem]
>Any real square matrix $A$ can be decomposed as $$A=QR$$
>where $Q$ is an [orthogonal matrix](Special%20Matrices.md#Orthogonal%20Matrices), and $R$ is an upper triangular matrix.
>
>For complex matrices, $Q$ is a [unitary matrix](Special%20Matrices.md#Unitary%20Matrices).

Note: If $A$ is invertible and the diagonal elements of $R$ are positive, then the decomposition is unique.

## Process

Let $A=\begin{bmatrix}\vec c_1 & \vec c_2 & \cdots & \vec c_k\end{bmatrix}$. We apply the [Gram-Schmidt process](Gram-Schmidt%20Process.md) on the column vectors $\vec c_i$ to get an orthonormal basis $\vec v_1, \vec v_2, \dots, \vec v_k$. We say
$$Q=\begin{bmatrix}\vec v_1 & \vec v_2 & \cdots & \vec v_k\end{bmatrix}$$
and 
$$R=\begin{bmatrix}
 \langle\vec v_1, \vec c_1\rangle & \langle\vec v_1, \vec c_2\rangle & \langle\vec v_1, \vec c_3\rangle & \cdots & \langle\vec v_1, \vec c_k\rangle \\
 0 & \langle\vec v_2, \vec c_2\rangle & \langle\vec v_2, \vec c_3\rangle & \cdots & \langle\vec v_2, \vec c_k\rangle \\
 0 & 0 & \langle\vec v_3, \vec c_3\rangle & \cdots & \langle\vec v_3, \vec c_k\rangle \\
 \vdots & \vdots & \vdots & \ddots & \vdots \\
 0 & 0 & 0 & \cdots & \langle\vec v_k, \vec c_k\rangle
\end{bmatrix}$$

### Shortcut

An alternative way to solve for $R$ makes use of the fact that $Q$ is an orthogonal matrix, which has the special property of $Q^{-1}=Q^T$. 

$$\begin{align}
A&=QR \\
Q^{-1}A&=Q^{-1}QR \\
Q^TA&=R
\end{align}$$
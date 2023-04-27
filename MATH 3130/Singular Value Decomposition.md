
>[!definition]
>Any matrix $A$ can be decomposed into a diagonal matrix of its singular values and two orthonormal matrices. This factorization, known as the **singular value decomposition (SVD)** is given by
>$$A=U\Sigma V^T$$
>for an $m\times n$ matrix $A$, where
>- $U$ is an $m\times m$ matrix of the orthonormal eigenvectors of $AA^T$
>- $V$ is an $n\times n$ matrix of the orthonormal eigenvectors of $A^TA$
>- $\Sigma$ is an $m\times n$ diagonal matrix of the singular values

>[!definition]
>The **singular values** $\sigma_i$ of a matrix $A$ are the square roots of the eigenvalues of $A^TA$. 
>
>A special property of singular values and the corresponding singular vectors is $$A\vec v_i=\sigma_i\vec u_i$$

It follows by the definition of eigenvalues, 
$$\begin{align}
AA^T\vec u_i&=\sigma_i^2\vec u_i \\
A^TA\vec v_i&=\sigma_i^2\vec v_i
\end{align}$$

The SVD decomposition allows us to break down $A$ into a sum of rank-1 matrices:
$$A=\sum_{i=1}^r\sigma_i\vec u_i\vec v_i^T$$where $u_i, v_i^T$ are respectively the columns of $U$ and rows of $V^T$.

## Process

First find the singular values. Since the eigenvalues (up to the possible rank) of $A^TA$ and $AA^T$  are the same, choose to calculate the one of the smaller dimension, for simplicity. 

Then, using the given eigenvalues, solve for $V$ first by finding the eigenvectors of the found eigenvalues. In the case that we calculated $AA^T$ before, we will have a missing eigenvector. We can find this from the property that our eigenvector will be orthogonal to the other ones. 

For example, in the case of a $3\times 3$, we can solve $\vec v_1, \vec v_2$ from the found eigenvalues. Then we find $\vec v_3=\vec v_1\times \vec v_2$ (scaled).

Then using the relation $A\vec v_i=\sigma_i\vec u_i$ from above, we can solve for $U$ with the relation $\vec u_i=\frac1{\sigma_i}A\vec v_i$. 

## Inverse with SVD

We can use SVD to easily calculate the inverse matrix.
$$\begin{align}
A&=U\Sigma V^T \\
A^{-1}&=(U\Sigma V^T)^{-1} \\
&=(V^T)^{-1}\Sigma^{-1}U^{-1} \\
&=\boxed{V\Sigma^{-1}U^T} & \text{($V, U$ are orthogonal)}
\end{align}$$
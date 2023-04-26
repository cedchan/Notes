
>[!definition]
>Any matrix $A$ can be decomposed into a diagonal matrix of its singular values and two orthonormal matrices. This factorization, known as the **singular value decomposition (SVD)** is given by
>$$A=UWV^T$$
>for an $m\times n$ matrix $A$, where
>- $U$ is an $m\times m$ matrix of the orthonormal eigenvectors of $AA^T$
>- $V$ is an $n\times n$ matrix of the orthonormal eigenvectors of $A^TA$
>- $W$ is an $m\times n$ diagonal matrix of the singular values

>[!definition]
>The **singular values** $\sigma_i$ of a matrix $A$ are the square roots of the eigenvalues of $A^TA$. 

## Process

First find the singular values. Since the eigenvalues (up to the possible rank) of $A^TA$ and $AA^T$  are the same, choose to calculate the one of the smaller dimension, for simplicity.


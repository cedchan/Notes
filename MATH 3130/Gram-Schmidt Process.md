Given a vector space $S$ spanned by linearly independent vectors $\vec c_1, \vec c_2, \dots, \vec c_k$, we want to find an orthnormal basis $\vec v_1, \vec v_2, \dots, \vec v_k$ for $S$. 

The **Gram-Schmidt process** allows us to systematically find such a basis with the following steps. First, we find orthogonal basis vectors $\vec u_1, \vec u_2, \dots, \vec u_k$ (*not necessarily* orthonormal). Then we normalize these basis vectors.

We calculate $u_i$ as follows:
$$\begin{align}
\vec u_1&=\vec c_1 \\
\vec u_2&=\vec c_2-{\rm proj}_{\vec u_1}\vec c_2 \\
\vec u_3&=\vec c_3-{\rm proj}_{\vec u_1}\vec c_3-{\rm proj}_{\vec u_2}\vec c_3 \\
\vec u_4&=\vec c_4-{\rm proj}_{\vec u_1}\vec c_4-{\rm proj}_{\vec u_2}\vec c_4-{\rm proj}_{\vec u_3}\vec c_4 \\
&\ \vdots\\
\vec u_k&=\vec c_k-\sum_{j=1}^{k-1}{\rm proj}_{\vec u_j}\vec c_k
\end{align}$$
Recall the definition of the projection operator:
$${\rm proj}_{\vec u}\vec v=\frac{\langle \vec v, \vec u\rangle}{\langle \vec u, \vec u\rangle}\vec u$$
We thus substitute to get the equivalent process
$$
\begin{align}
\vec u_1&=\vec c_1 \\
\vec u_2&=\vec c_2-\frac{\langle \vec c_2, \vec u_1\rangle}{\langle \vec u_1, \vec u_1\rangle}\vec u_1 \\
\vec u_3&=\vec c_3-\frac{\langle \vec c_3, \vec u_1\rangle}{\langle \vec u_1, \vec u_1\rangle}\vec u_1-\frac{\langle \vec c_3, \vec u_2\rangle}{\langle \vec u_2, \vec u_2\rangle}\vec u_2 \\
\vec u_4&=\vec c_4-\frac{\langle \vec c_4, \vec u_1\rangle}{\langle \vec u_1, \vec u_1\rangle}\vec u_1-\frac{\langle \vec c_4, \vec u_2\rangle}{\langle \vec u_2, \vec u_2\rangle}\vec u_2-\frac{\langle \vec c_4, \vec u_3\rangle}{\langle \vec u_3, \vec u_3\rangle}\vec u_3 \\
&\ \vdots\\
\vec u_k&=\vec c_k-\sum_{j=1}^{k-1}\frac{\langle \vec c_k, \vec u_j\rangle}{\langle \vec u_j, \vec u_j\rangle}\vec u_j
\end{align}
$$
Finally, we normalize each vector $\vec u_i$ to get our orthonormal basis vectors $\vec v_i$:
$$\vec v_i=\frac{\vec u_i}{\langle\vec u_i, \vec u_i\rangle}=\frac{\vec u_i}{||\vec u_i||} \quad \text{(for numerical vectors)}$$


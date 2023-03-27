>[!summary]+
>

--- 
## Linear Transformations

### Transformation Matrices

Transformation matrices do a linear combination when multiplied by a vector, resulting in a new vector within the same vector speace.

A transformation $T: V\rightarrow V$ is a map between vector spaces. Transformations are **linear** if they satisfy two conditions:
1. **Superposition:** $T(\vec{v}_1+\vec{v}_2)=T(\vec{v}_1) + T(\vec{v}_2)$
2. **Homogeneity:** $T(\lambda\vec{v})=\lambda T(\vec{v})$

$V$ has basis $\mathcal{B}=\{ \vec{v}_1, \vec{v}_2 \}$. Typically, a transformation might require two bases for the source and target of the mapping.

Transformation matrices transform matrices by expressing them as a different linear combination of the basis of the subspace. We can find such a transformation by looking at a transformation of the basis vectors. 
$$\begin{gathered}
	T\vec{v}_1=a\vec{v}_1+b\vec{v}_2 \\
	T\vec{v}_2=c\vec{v}_1 +d\vec{v}_2 \\
\end{gathered}$$
The coefficients of each row correspond to a column in the transition matrix $A$. 
$$\begin{gathered}
	A=A_{\mathcal{B}\mathcal{B}}=
	\begin{pmatrix}
		a & c \\
		b & d
	\end{pmatrix} \\
\end{gathered}$$
>[!hint]
>The notation for a transformation $X$ from space $\mathcal B_i$ to $\mathcal B_j$ is $X_{\mathcal{B}_j\mathcal{B}_i}$.  In other words, the bases appear in reverse order of the transformation in the subscript.

With this matrix, we can generalize to transform any vector in the space. The second equation listed is the matricized version. 
$$\begin{gathered}T(x_1\vec{v}_1+x_2\vec{v}_2)=y_1\vec{v}_1+y_2\vec{v}_2 \\
	\iff A\begin{pmatrix}x_1 \\ x_2\end{pmatrix}=\begin{pmatrix}y_1 \\y_2\end{pmatrix}
\end{gathered}
$$

**Example:**
>$$\begin{align}
P_2(\mathbb{R})&=\{a+bx+cx^2\} \\ 
T&=\frac{d}{dx}:P_2\rightarrow P_2 \\ 
T(a+bx+cx^2)&=b+2cx \\ 
\mathcal{B}&=\{1,x,x^2\} & \text{(basis of $P_2(\mathbb{R})$)} \\ 
T(1) &= 0 =0\cdot1+0\cdot x + 0\cdot x^2\\
T(x) &= x =1\cdot1 +0\cdot x + 0\cdot x^2\\ 
T(x^2) &= 2x =0\cdot 1 +2\cdot x+0\cdot x^2\\ 
A_{\mathcal{B}\mathcal{B}}&=
\begin{pmatrix}
0 & 1 & 0 \\
0 & 0 & 2 \\
0 & 0 & 0
\end{pmatrix}
\end{align}$$

### Transition Matrices

Transition matrices change the basis of a vector. We can follow the same schema as with transformation matrices, but this time we express the basis vectors of $\mathcal B_1$ as a combination of the basis vectors of $\mathcal B_2$. 
$$\begin{gathered}
	\mathcal{B}_1=\{\vec{v}_1,\vec{v}_2\} \\ \mathcal{B}_2=\{\vec{v}_1',\vec{v}_2'\} \\
	\vec{v}_1=a\vec{v}_1'+b\vec{v}_2' \\
	\vec{v}_2=c\vec{v}_1'+d\vec{v}_2' \\
	P=P_{\mathcal{B}_2\mathcal{B}_1}=
	\begin{pmatrix}
		a & c \\
		b & d
	\end{pmatrix} \\
	P(x_1\vec{v}_1+x_2\vec{v}_2)=y_1\vec{v}_1'+y_2\vec{v}_2' \\
	\iff P_{\mathcal{B}_2\mathcal{B}_1}\begin{pmatrix}x_1\\x_2\end{pmatrix}=\begin{pmatrix}y_1\\y_2\end{pmatrix}
\end{gathered}$$
### Change of Basis

Suppose we have a transformation matrix $A_{\mathcal{B}_1\mathcal{B}_1}$ and we want to perform the transition in the space spanned by $\mathcal{B}_2$. We can achieve this by using our transition matrix in combination with our transformation matrix.
$$
\begin{gathered}
	T: V\rightarrow V\\
	\mathcal{B}_1=\{\vec{v}_1,\vec{v}_2\} \\ \mathcal{B}_2=\{\vec{v}_1',\vec{v}_2'\} \\
	A_{\mathcal{B}_2\mathcal{B}_2}=PA_{\mathcal{B}_1\mathcal{B}_1}P^{-1} \\
	A_{\mathcal{B}_2\mathcal{B}_2}=P_{\mathcal{B}_2\mathcal{B}_1}A_{\mathcal{B}_1\mathcal{B}_1}P_{\mathcal{B}_1\mathcal{B}_2}
\end{gathered}
$$

Why is this helpful? Studying a matrix in one basis is easier in some bases than other (e.g., when it's diagonal). 

**Example:**
>$${\begin{gathered}
\mathcal{B}_2=\{1,x,\frac{x^2-1}{2}\} \\
1=1\cdot1 \\ x=1\cdot x \\
x^2=1\cdot 1+2\cdot\frac{x^2-1}{2} \\
P=P_{\mathcal{B}_2\mathcal{B}_1}=\begin{pmatrix}1 & 0 & 1\\0 & 1 & 0 \\ 0 & 0 & 2\end{pmatrix} \\
P^{-1}=\begin{pmatrix}
1 & 0 & -\frac{1}{2} \\
0 & 1 & 0 \\
0 & 0 & \frac{1}{2}
\end{pmatrix} \\
A_{\mathcal{B}_2\mathcal{B}_2}=PA_{\mathcal{B}_1\mathcal{B}_1}P^{-1}=\begin{pmatrix}0 & 1 & 0 \\0 & 0 & 1\\0 & 0 & 0\end{pmatrix}
\end{gathered}}$$

#### Transformation Across Bases

>[!danger]
>I don't think I wrote this right

A similar technique can be used to apply a transformation from one basis to another. For such a transformation from $\mathcal{B}_2$ to $\mathcal{C}_2$. 
$$\begin{gathered}
	T:V\rightarrow W \\
	V: \mathcal{B}_1, \mathcal{B}_2 \\
	W: \mathcal{C}_1, \mathcal{C}_2 \\
	A_{\mathcal{C}_2\mathcal{B}_2}=P_{\mathcal{C}_2\mathcal{C}_1}A_{\mathcal{C}_1\mathcal{B}_1}P_{\mathcal{B}_2\mathcal{B}_2}
\end{gathered}$$

## Inner Product 

The inner product is a generalization of the dot product. It multiplies two vectors to result in a scalar. The notation is shown below:
$$\langle \cdot,\cdot\rangle: V\times V \rightarrow \mathbb{R}$$

Properties for a real vector space:
1. $\langle\vec{u}, \vec{v}\rangle=\langle\vec{v},\vec{u}\rangle$
2. $\langle\vec{u},\lambda_1\vec{v}_1+\lambda_2\vec{v}_2\rangle=\lambda_1\langle\vec{u},\vec{v}_1\rangle+\lambda_2\langle\vec{u},\vec{v}_2\rangle$
3. $\forall \vec{v}\neq\vec{0}, \langle\vec{v},\vec{v}\rangle>0$

(Note that property 2 can be expanded into two properties: scalar multiplication and linearity.)

Extensions:
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

**Example.** $\mathbb{R}^2$ dot product

**Example.** $M_{2\times2}(\mathbb{R}), \langle\cdot,\cdot\rangle$
>[!danger]
>There was something before the $(A^TB)$ that I didn't catch.

>$$
\begin{align}
\langle A,B\rangle&=(A^TB) \\
\left\langle\begin{pmatrix}a&b\\ c&d\end{pmatrix},
\begin{pmatrix}a&b\\ c&d\end{pmatrix}\right\rangle&=a^2+b^2+c^2+d^2
\end{align}$$

**Example.** Space of functions on $[0, 2\pi]$.
>$$\langle f,g\rangle=\frac{1}{\pi}\int_0^{2\pi}f(x)g(x)dx$$

>[!danger]
>Not sure where this is from.

## Orthonormal Basis

An **orthonormal basis** of $V$ with respect to $\langle\cdot,\cdot\rangle$ is $\mathcal{R}=\{\vec{v}_1,\vec{v}_2,\dots,\vec{v}_n\}$ such that 
1. $\langle\vec{v}_i,\vec{v}_i\rangle=1$ (i.e., they each vector in a unit/normal vector)
2. $\langle\vec v_i, \vec v_j\rangle=0$ (i.e., each vector is orthogonal)

**Example.** The Fourier Space
>$\left\{\frac{1}{\sqrt{2}},\cos x, \sin x, \cos 2x, \sin 2x, \dots \right\}$ is an orthonormal basis that spans all functions.
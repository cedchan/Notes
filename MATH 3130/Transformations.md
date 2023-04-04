>[!summary]+
>

--- 
## Linear Transformations

### Transformation Matrices

Transformation matrices do a linear combination when multiplied by a vector, resulting in a new vector within the same [vector space](Vector%20Spaces.md).

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

>**Example.** $P_2(\mathbb R)=\{a+bx+cx^2\}, T=\frac{d}{dx}:P_2\rightarrow P_2$. Find $A_{\mathcal B\mathcal B}$.

>[!solution]+
>$$\begin{align}
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

>[!equation]
>We can simply write the transition matrix as $P=\mathcal B_2^{-1}\mathcal B_1$. 

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

>**Example.** $\mathcal{B}_2=\{1,x,\frac{x^2-1}{2}\}$. Find $A_{\mathcal B_2\mathcal B_2}$.

>[!solution]+
>$${\begin{gathered}
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

## Composition of Linear Transformations

Like with functions, transformation matrices can be **composed** to create a "new" transformation. 

>[!theorem]
>The composition of linear transformations is linear.
>
For linear transformations $S, T$ below, $TS$ is also linear.$$
\begin{align}
S&:U\rightarrow V\\
T&:V\rightarrow W\\
TS&:U\rightarrow W
\end{align}
$$

*Proof:* 
**Superposition:**
$$\begin{align}
(TS)(\vec u_1+\vec u_2)&=T(S(\vec u_1+\vec u_2) \\
&=T(S\vec u_1+S\vec u_2) \\
&=T(S\vec u_1)+T(S\vec u_2) \\
&=(TS)\vec u_1 +(TS)\vec u_2
\end{align}$$
**Homogeneity:** 
$$\begin{align}
(TS)(\lambda\vec u)=\lambda((TS)\vec u)
\end{align}$$
(Full steps not shown.)

>**Example.** Find $TS(\vec u_1+\vec u_2)$ given$${
\begin{align}
S\vec u_1&=4\vec v_1-2\vec v_2 \\
S\vec u_2&=\vec v_1 \\
T\vec v_1&=\vec w_1+\vec w_2 \\
T\vec v_2&=2\vec w_1+3\vec w_2
\end{align}
}$$

>[!solution]+
>$${\begin{align}
TS(\vec u_1+\vec u_2)&=T(S\vec u_1+S\vec u_2) \\
&=T(4\vec v_1-2\vec v_2+\vec v_1) \\
&=T(5\vec v_1-2\vec v_2) \\
&=5T(\vec v_1)-2T(\vec v_2) \\
&=5(\vec w_1+\vec w_2)-2(2\vec w_1+3\vec w_2) \\
&=w_1-w_2
\end{align}}$$

### Compositions of Transformations

Suppose the matrix of $S=A$, and the matrix of $T=B$. Then what is the matrix of the composition $TS$?

Since we apply $S$ first, then $T$, our answer is $BA$. 

>**Example.** $U, V, W$ have bases $\{\vec u_1, \vec u_2\}, \{\vec v_1, \vec v_2\}, \{\vec w_1, \vec w_2\}$ (from prior example). Find the matrix of the composition $TS$. 

>[!solution]+
>$${\begin{align}
A&=\begin{pmatrix}
4 & 1\\
-2 & 0
\end{pmatrix}\\
B&=\begin{pmatrix}
1 & 2\\
1 & 3
\end{pmatrix} \\
BA&=\begin{pmatrix}
0 & 1 \\
-2 & 1
\end{pmatrix}\\
BA\begin{pmatrix}1 \\ 1\end{pmatrix} &=\begin{pmatrix}1 \\ -1\end{pmatrix}
\end{align}}$$
This verifies the result we got from the previous example.

## Common Transformations

### Rotations

Let $rot$ be some rotation transformation. Then,
$$\det(rot)=1$$
because geometrically, the determinant represents the area of the parallelogram (or in 3-D space volume), so a rotation should have no impact, as shown below:
$$\begin{align}
\det(A)&=x \\
\det(rot\cdot A)&=\det(rot)\det(A) \\
&=\det(rot)\cdot x \\
&=x \\
\therefore \det(rot)&=1

\end{align}$$

### Reflections

Let $ref$ be some reflection transformation. Then,
$$\det(ref) =-1$$
Similar to rotations, reflections are also area-preserving, but it's the other "face" of the image, so the determinant is $-1$. Imagine that the vector is on a sheet of paper. A rotation just turns that paper without changing the area, while the reflection "flips" the paper. The steps for showing why this holds are essentially the same as in the rotations example.

### Projections

[TK]

### Common Compositions

>[!equation]
>Note the following common compositions:
>$$\begin{align}
(rot)(ref) &= (ref) \\ 
(ref)(ref) &= (rot) \\
(rot)(rot) &= (rot) \\
\end{align}$$

*Proof:* The proof directly follows the previous determinant calculations. 
$$\begin{align}
\det(rot)\det(ref)&=1(-1) \\
&=-1 \\
&=\det(ref) \\
\det(ref)\det(ref)&=(-1)(-1) \\
&=1\\
&=\det(rot) \\
\det(rot)\det(rot)&=1(1) \\
&=1 \\
&=\det(rot)
\end{align}$$
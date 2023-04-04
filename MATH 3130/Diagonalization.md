
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

The columns of $P$ are the eigenvectors $\vec v_i$ of $A$, and the value of the diagonal in $J$ is the corresponding eigenvalue $\lambda_i$. Clearly, this isn't work unless the geometric multiplicity of each eigenvalue—that is, how many eigenvectors we can find for it—is greater than or equal to the algebraic multiplicity—the multiplicity of its term in the characteristic polynomial.

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
>We see for $J_i$ that the diagonals are the eigenvalues. Here, we have $\lambda=0$, with geometric multiplicity 1 (we could only get 1 eigenvector from it) but algebraic multiplicity 2 (in the characteristic polynomial, the term corresponding to this eigenvalue is to the power of two, $\lambda^2$). The $1$ appears above the second one because it was used to derive a generalized eigenvector.

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

## Fast Matrix Exponentiation

Another useful application of the diagonal is calculating exponents $A^n$ quickly. Notice:
$$
\begin{align}
A^n&=(PJP^{-1})^n \\
&=\underbrace{PJP^{-1}PJP^{-1}\dots PJP^{-1}}_{n} \\
&=PJ\cancel{P^{-1}P}\cancel\dots\cancel{P^{-1}P}JP^{-1} \\
&=PJ^nP^{-1}
\end{align}
$$
When $J$ is diagonal, $J^n$ is equal to $J$, with all the elements raised to the $n$-th power.

When $J$ is in the block form (so not completely diagonal), $J_i^n$ can be calculated as follows
$$
\begin{align}
J_i&=J+\begin{pmatrix}
0 & 1 & 0 \\
0 & 0 & 1 \\
0 & 0 & 0
\end{pmatrix} \\
&=\lambda I+K \\
J^n&=(\lambda I+K)^n \\
&=\sum_{k=0}^n\binom{n}{k}\lambda^kIK^{n-k}
\end{align}
$$

>[!equation]
>A square matrix exponent can be quickly found by
>$$A^n=PJP^{-1}$$
>its diagonal decomposition.
>
>When $A$ is not diagonal, the same process can be applied to the Jordan block, but instead we subtract out the diagonal and apply the binomial expansion.


## Differential Equations

Let's say you have a differential equation for an equation, as well as its value at $t=0$, and you want to find its value for all other times $t$. How do we do this?

Let's start with a simple refresher on a typical differential equation. 
$$\begin{align}
u=u(t), \frac{du}{dt}&=au, a\in \mathbb R \\
\int\frac{du}u&=\int adt \\
\ln u &= at+c \\
u(t)&=e^{at}e^c \\
&=e^{at}u(0)
\end{align}$$
Now for the more complex case: The differential of one equation is given as a linear combination of the original function and another function. Our method from above doesn't work anymore.
$$\begin{align}
\vec u_1=\vec u_1(t) &, \vec u_2=\vec u_2(t) \\
\frac{d\vec u_1}{dt}&=a\vec u_1+b\vec u_2 \\
\frac{d\vec u_2}{dt}&=c\vec u_1+d\vec u_2
\end{align}$$
In the easy case, just like above, the differential is just given in terms of the original function. Then we can do integration as normal.
$$
\begin{align}
\frac{du_1}{dt}&=au_1, u_1=e^{at}u_1(0) \\
\frac{du_2}{dt}&=du_2, u_2=e^{dt}u_2(0)
\end{align}
$$
But how do we generalize this? We can vectorize our functions.
$$\begin{align}
\vec u(t)=\begin{pmatrix}u_1(t) \\ u_2(t)\end{pmatrix}&, A=\begin{pmatrix}a & b \\ c & d\end{pmatrix} \\
\frac{d\vec u}{dt}&=A\vec u \\
\vec u(t)&=\boxed{e^{At}\vec u(0)}
\end{align}$$
What do we do about the $e^{At}$ term, though? We can apply the Taylor expansion.
$$\begin{align}
e^x&=1+x+\frac{x^2}{2!}+\frac{x^3}{3!}+\dots \\
e^{At}&=I+At+\frac{A^2t^2}{2!}+\frac{A^3}{3!}+\dots \\
A&=PJP^{-1} \\
e^{At}&=I+PJtP^{-1}+\frac{PJ^2t^2P^{-1}}{2!}+\frac{PJ^3t^3P^{-1}}{3!}+\dots \\
&=P(I+Jt+\frac{J^2t^2}{2!}+\frac{J^3t^3}{3!}+\dots)P^{-1} \\
&=Pe^{Jt}P^{-1} \\
\vec u(t)&=\boxed{Pe^{Jt}P^{-1}\vec u(0)}
\end{align}$$

Let's try to find $e^{Jt}$ with a $2\times 2$ matrix $J=\begin{pmatrix}\lambda_1 & 0 \\ 0 & \lambda_2\end{pmatrix}$.
$$
\begin{align}
e^{Jt}&=I+Jt+\frac{J^2t^2}{2!}+\frac{J^3t^3}{3!}+\dots \\
&=\begin{pmatrix}
1 & 0 \\ 
0 & 1
\end{pmatrix}+
\begin{pmatrix}
\lambda_1t & 0 \\
0 & \lambda_2t
\end{pmatrix}+
\begin{pmatrix}
\frac{\lambda_1^2t^2}{2!} & 0 \\
0 & \frac{\lambda_2^2t^2}{2!}
\end{pmatrix}+\dots \\
&=\begin{pmatrix}
1+\lambda_1t+\frac{\lambda_1^2t^2}{2!}+\dots & 0 \\
0 & 1+\lambda_2t+\frac{\lambda_2^2t^2}{2!}+\dots
\end{pmatrix} \\
&=\begin{pmatrix}
e^{\lambda_1t} & 0 \\
0 & e^{\lambda_2t}
\end{pmatrix} \\
&=\boxed{e^{\lambda t}I}
\end{align}
$$

>[!equation]
>Given $${
\begin{align}
\frac{du_1}{dt}&=au_1+bu_2 \\
\frac{du_2}{dt}&=cu_1+du_2
\end{align}}$$
>we can matricize the problem as follows:
>$${\begin{align}
\vec u(t)=\begin{pmatrix}u_1(t) \\ u_2(t)\end{pmatrix} &,
A=\begin{pmatrix}
a & c \\
b & d
\end{pmatrix} \\
\implies \frac{d\vec u}{dt}&=A\vec u \\
\vec u(t)&=e^{At}\vec u(0) \\
&=\boxed{Pe^{Jt}P^{-1}\vec u(0)}
\end{align}}$$
>For a diagonal, this is
>$${\vec u(t)=Pe^{\lambda t}IP^{-1}\vec u(0)}$$


>**Example.** Doing this process with a Jordan block matrix $A=\begin{pmatrix}3 & 1 \\-1 & 1\end{pmatrix}$. Find $e^{At}$ (which can be used in $\vec u(t)=e^{At}\vec u(0)$). 

>[!solution]+
>$$\begin{align}
A&=PJP^{-1} \\
P&=\begin{pmatrix}
1 & 0 \\
-1 & 1
\end{pmatrix} \\
J&=\begin{pmatrix}
2 & 1 \\
0 & 2
\end{pmatrix} \\
e^{At}&=Pe^{Jt}P^{-1} \\
e^{Jt}&=I +Jt+\frac{J^2t^2}{2!}+\frac{J^3t^3}{3!}+\dots \\
&=\begin{pmatrix}
1 & 0 \\
0 & 1
\end{pmatrix}+
\begin{pmatrix}
2t & 1 \\
0 & 2t
\end{pmatrix}+
\begin{pmatrix}
\frac{2^2t^2}{2!} & 2t^2 \\
0 & \frac{2^2t^2}{2!}
\end{pmatrix} \\
&\qquad\qquad +
\begin{pmatrix}
\frac{2^3t^3}{3!} & \frac{2^2t^2}{2!}t \\
0 & \frac{2^3t^3}{3!}
\end{pmatrix}+
\begin{pmatrix}
\frac{2^4t^4}{4!} & \frac{2^3t^3}{3!}t \\
0 & \frac{2^4t^4}{4!}
\end{pmatrix}+\dots \\
&=\begin{pmatrix}
e^{2t} & e^{2t}t \\
0 & e^{2t}
\end{pmatrix} \\
e^{At}&=
\begin{pmatrix}
1 & 0 \\
-1 & 1
\end{pmatrix}
\begin{pmatrix}
e^{2t} & e^{2t}t \\
0 & e^{2t}
\end{pmatrix}
\begin{pmatrix}
1 & 0 \\
1 & 1
\end{pmatrix} \\
&=
\begin{pmatrix}
e^{2t} & e^{2t}t \\
-e^{2t} & e^{2t}(1-t)
\end{pmatrix}
\begin{pmatrix}
1 & 0 \\
1 & 1
\end{pmatrix} \\
&=
\begin{pmatrix}
e^{2t}(1+t) & e^{2t}t \\
-e^{2t} & e^{2t}(1-t)
\end{pmatrix}
\end{align}$$
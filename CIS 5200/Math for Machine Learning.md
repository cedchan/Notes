## Linear Algebra

### Special Matrices

#### Definite Matrices

>[!definition]
>A **positive definite matrix** satisfies the following: $$\forall \vec x \in \mathbb R^n \setminus \{\vec0\}, \vec x^\top A\vec x>0$$
>
>A **positive semi-definite matrix** $A^{n\times n}$ satisfies the following: $$\forall \vec x \in \mathbb R^n, \vec x^\top A\vec x\geq 0$$
>
>The definitions of **negative (semi-)definite matrices** follow in an analogous fashion.

We can test whether a matrix is a definite matrix by using an arbitrary vector $\vec x=(x_1, x_2, \dots, x_3)^\top$, and testing if the evaluated expression $\vec x^\top A\vec x$ satisfies the necessary conditions.
## Calculus

### Gradients

>[!definition]
>The **gradient** $\nabla_{\vec x}f(\vec x)$ of a function $f(\vec x), \vec x=(x_1, x_2, \dots, x_n)^\top$ is defined as a vector consisting of the partial derivatives of $f$. That is,
>$$\nabla_{\vec x}f(\vec x)=\left(\frac{\partial f}{\partial x_1}, \frac{\partial f}{\partial x_2}, \dots, \frac{\partial f}{\partial x_n}\right)^\top$$

### Second Derivatives

The **second derivatives** of a multivariable function can be found by taking the partial derivatives of the first-order derivatives.

Some notation: $f_x=\frac{\partial f}{\partial x}$, $f_{xy}=\frac{\partial f}{\partial y}\frac{\partial f}{\partial x}$.

### Discriminant

The **discriminant** of two-variable equations is the determinant of $\begin{bmatrix}f_{xx} & f_{xy} \\ f_{yx} & f_{yy}\end{bmatrix}$.

That is,
$$D=\begin{vmatrix}f_{xx} & f_{xy} \\
f_{yx} & f_{yy}
\end{vmatrix}=f_{xx}f_{yy}-f_{xy}^2$$
### Optimization

#### Critical Points

>[!definition]
>The **critical points** of a multivariable function $f(\vec x)$ are defined as the points where the gradient $\nabla_{\vec x}f(\vec x)$ is $\vec 0$. 

#### Second Derivative Test

For multivariable functions, critical points can be local minima, maxima, or saddle points. We can use the **second derivative test** to determine which is the case.

>[!theorem] Second Derivative Test
>Let $(a, b)$ be a critical point of $f(x, y)$. Let 
>- $D(a, b)>0 \land f_{xx}(a, b)>0 \implies$ local minimum
>- $D(a, b)>0 \land f_{xx}(a, b) < 0 \implies$ local maximum
>- $D(a, b) < 0 \implies$ saddle point
>- $D(a, b) = 0$ is indeterminate


## Probability

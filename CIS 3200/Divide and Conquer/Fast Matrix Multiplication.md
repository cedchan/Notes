---
tags:
  - divide-and-conquer
---

## Baseline

Recall that for two matrices $A^{n\times n}, B^{n\times n}$ with product $A\times B=C$, the element $c_{ij}$ is given by $$c_{ij}=\sum_{\ell=1}^na_{i\ell}\cdot b_{\ell j}$$
The baseline algorithm brute-forces $c_{ij}$ for all $i, j$. For each of these calculations, it must also iterate through all $\ell$, giving total $O(n^3)$ runtime.

## Divide-and-Conquer Attempt 1

Suppose we let $A, B$ be represented as follows:
$$A=\begin{bmatrix}
A_{11} & A_{12} \\
A_{21} & A_{22}
\end{bmatrix}, 
B=\begin{bmatrix}
B_{11} & B_{12} \\
B_{21} & B_{22}
\end{bmatrix}$$
Then, $C$ can be written as
$$C=\begin{bmatrix}
A_{11}B_{11}+A_{12}B_{21} & A_{11}B_{12}+A_{12}B_{22} \\
A_{21}B_{11}+A_{22}B_{21} & A_{21}B_{12}+A_{22}+B_{22}
\end{bmatrix}$$
>[!algorithm]
>
>Compute $A_{11}B_{11}, A_{11}B_{12},\dots,A_{22}B_{22}$. Then, add their outputs and place them in the right locations.
>
>Each of those are also matrix multiplications of size $\frac n2\times\frac n2$.

### Runtime

The combine step takes $O(n^2)$ time, since we have to go through each element and edit it. Then, with our recursive calls of size $\frac n2$, we get the recurrence
$$\begin{align}
T(n)&=8\cdot T\left(\frac{n}{2}\right)+O(n^2) \\
&=O(n^3) & \text{(Master Theorem)}
\end{align}$$

## Divide-and-Conquer Attempt 2

$$\begin{align}
T(n)&=7\cdot T\left(\frac n2\right)+O(n^2) \\
&=O(n^{\log_27})=O(n^{2.80\dots})
\end{align}$$

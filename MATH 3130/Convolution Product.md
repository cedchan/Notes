>[!definition]
>Consider $x, y\in L^2(\mathbb Z_n, \mathbb C)$. Then, $x*y\in L^2(\mathbb Z_n, \mathbb C)$, where $*$ denotes the **convolution product**. We define $x*y$ as follows:
>$$(x*y)_k=\sum_{l\in\mathbb Z_n}x_l\cdot y_{k-l}$$

>**Example.** In $\mathbb Z_3$, let $x=(1,2,3), y=(-2,3,5)$. Find $(x*y)_k$.

>[!solution]+
>$$\begin{align}
x=(1,2,3)&=(x_0,x_1,x_2) \\
y=(-2,3,5)&=(y_0,y_1,y_2) \\
(x*y)_0&=x_0y_0+x_1y_{-1}+x_2y_{-2} \\
&=\boxed{x_0y_0 +x_1y_2+x_2y_1} \\
(x*y)_1&=x_0y_1+x_1y_0+x_2y_{-1} \\
&=\boxed{x_0y_1+x_1y_0+x_2y_2} \\
(x*y)_2&=\boxed{x_0y_2+x_1y_1+x_2y_0}
\end{align}$$

Note that convolution is commutative. That is, $f*g=g*f$.

## Convolution Theorem

>[!theorem]
>The **Convolution Theorem** of $L^2(\mathbb Z_n, \mathbb C)$ states that if $X=F(x), Y=F(y)$, then 
>$$XY=F(x*y)$$ where $XY$ represents the element-wise (point-wise) product of $X$ and $Y$. 
>
>The inverse is also true. That is,
>$$x*y=F^{-1}(Fx)(Fy)$$

The Convolution Theorem allows us to perform certain operations quickly. 

## Efficient Convolution

From the Convolution Theorem, we know that we can a perform a convolution through a Fourier transform: $x*y=F^{-1}(Fx)(Fy)$. As it turns out, using the Fast Fourier Transform, calculating the righthand side is actually more efficient. 

## Polynomial Multiplication

Consider the polynomial multiplication here:
$$\begin{align}
p&=a_0+a_1t+a_2t^2 \\
q&=b_0+b_1t+b_2t^2 \\
pq&=a_0b_0+(a_0b_1+a_1b_0)t+(a_0b_2+a_1b_1+a_2b_0)t^2\\
&\qquad +(a_1b_2+a_2b_1)t^3+a_2b_2t^4
\end{align}$$
Notice that this looks oddly similar to convolution. Let's vectorize the problem as follows:
$$\begin{align}
a&=(a_0,a_1,a_2,0,0,0)\in L^2(\mathbb Z_b, \mathbb C) \\
b&=(b_0, b_1,b_2,0,0,0)\in L^2(\mathbb Z_b, \mathbb C) \\
a*b&=(a_0b_0,a_0b_1+a_1b_0,a_0b_2+a_1b_1+a_2b_0,a_1b_2+a_0b_1,a_2b_2,0)
\end{align}$$
We have to add the $0$s to have enough space for the "wraparound" effects.

This generalizes to all polynomial multiplication.

### Integer Multiplication

In the same manner as polynomial multiplication, integer multiplication for large numbers can be computed as a convolution. Applying the efficient algorithm, this becomes an application of the DFT (specifically the FFT).
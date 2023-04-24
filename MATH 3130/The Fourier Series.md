 
## Notation

$$
\begin{align}
L^2([0,2\pi],\mathbb C)&=\left\{f:[0,2\pi]\rightarrow\mathbb C \ \middle| \ \int_0^{2\pi}|f(x)|^2dx<\infty\right\} & \\
&\qquad\text{(square integrable)} \\
L^2(\mathbb Z, \mathbb C)&=\left\{(c_n)_{n\in\mathbb Z}
\ \middle|\ \sum_{n\in\mathbb Z}|c_n|^2<\infty, c_n\in \mathbb C\right\} \\
&\qquad\text{(This is the same as a function)} \\
L^2(\mathbb R,\mathbb C)&=\left\{f:\mathbb R\rightarrow\mathbb C 
\ \middle| \ \int_{-\infty}^\infty|f(x)|^2dx<\infty\right\} \\
\mathbb Z_n&=\{0,1,2,\dots,n-1\} \\
L^2(\mathbb Z_n, \mathbb C)&=\left\{x=(x_0,x_1,\dots,x_{n-1})\mid x_i\in\mathbb C\right\}
\end{align}
$$

## Euler's Formula

>[!equation]
>$$e^{i\theta}=\cos\theta+i\sin\theta$$

**Euler's formula** is helpful in calculating the complex conjugate of numbers in the  form $e^{nix}$, which will later be used to show that can form orthonormal bases. 

The complex conjugate of $re^{nix}$:
$$\begin{align}
\overline{e^{nix}}&=\overline{\cos\theta+i\sin\theta} \\
&=\cos\theta-i\sin\theta \\
&=e^{-nix}
\end{align}$$
### Euler's Identity

From Euler's formula, we can derive **Euler's identity**.

>[!equation]
>$$e^{i\pi}+1=0$$

*Proof:*
$$\begin{align}
e^{i\pi}&=\cos\pi+i\sin\pi \\
&=-1+i\cdot 0 \\
\therefore e^{i\pi}+1&=0
\end{align}$$

## Complex Functions

Consider two complex functions $f, g:[0,2\pi]\rightarrow\mathbb C$. Their inner product is defined as 
$$\langle f, g\rangle=\frac1{2\pi}\int_0^{2\pi}\overline{f(x)}g(x)dx$$
which follows from the definition of the [inner product of complex functions](Inner%20Product.md#Inner%20Product%20on%20Complex%20Vector%20Spaces#Complex%20Functions).

>**Example.** Find the inner product of $e^{ix}$ with itself.

>[!solution]+
>$${\begin{align}
\langle e^{ix},e^{ix}\rangle&=\frac1{2\pi}\int_0^{2\pi}\overline{e^{ix}}e^{ix}dx \\
e^{ix}&=\cos x+i\sin x \\
\overline{e^{ix}}&=\cos x -i\sin x \\
\langle e^{ix},e^{ix}\rangle&=\frac1{2\pi}\int_0^{2\pi}1dx \\
&=1
\end{align}}$$

>**Example.** Find the inner product of 1 with $e^{ix}$.

>[!solution]+
>$${\begin{align}
\langle1,e^{ix}\rangle&=\frac1{2\pi}\int_0^{2\pi}\overline1e^{ix}dx \\
&=0
\end{align}}$$
Again note that this means $1\perp e^{ix}$.

## An Orthogonal Basis

>[!theorem]
>$\{e^{nix}\mid n\in [-\infty..\infty]\}$ is an orthogonal basis.

*Proof:* We prove this by showing generally that $\langle e^{aix}, e^{bix} \rangle=0$ when $a\neq b$. 
$$\begin{align}
\langle e^{aix},e^{bix}\rangle&=\frac1{2\pi}\int_0^{2\pi}e^{-aix}e^{bix}dx \\
&=\frac1{2\pi}\int_0^{2\pi}e^{(b-a)ix}dx \\
&=\left.\frac{1}{2\pi}\cdot\frac{1}{(b-a)i}e^{(b-a)ix}\right\rvert_0^{2\pi} \\
&=\frac{1}{2\pi}\cdot\frac{e^{2\pi(b-a)i}-e^0}{(b-a)i} \\
e^{2\pi(b-a)i}&=\left(\left(e^{i\pi}\right)^2\right)^{b-a} \\
&=\left((-1)^2\right)^{b-a} & \text{(Euler's identity)}\\
&=\frac{1^b}{1^a} \\
&=1 \\
\therefore \langle e^{aix},e^{bix}\rangle&=\frac{1}{2\pi}\cdot\frac{1-1}{(b-a)i} \\
&=0 &\square
\end{align}$$

## The Fourier Series

Consider some function $f$ defined on 
$$f:[0,2\pi]\rightarrow \mathbb C$$
We know that we can form an [orthogonal basis](Inner%20Product.md#Orthonormal%20Basis) using functions in the set $\{e^{nix}\}$. We can therefore rewrite $f$ as a linear combination of an orthogonal basis formed by $\{e^{nix}\}$, with **Fourier coefficients** $c_n\in \mathbb C$. 
$$f=\sum_{n=-\infty}^\infty c_ne^{nix}$$
So how do we find the coefficients? The intuition is the same as how we normally represent vectors in new spaces: we can express our function $f$ in terms of each basis vector by projecting $f$ onto those vectors. That is, we find the inner product of the basis vector and $f$. 
$$\begin{align}
c_n&=\langle e^{nix},f(x)\rangle \\
&=\frac1{2\pi}\int_0^{2\pi}e^{-nix}f(x)dx
\end{align}$$
>[!equation]
>In short, the **Fourier series** represents a function $f:[0,2\pi]\rightarrow\mathbb C$ as a linear combination of the Fourier basis $\{e^{nix} \mid n\in[-\infty..\infty]\}$: $$f=\sum_{n=-\infty}^\infty c_ne^{n-x}$$ where $$\begin{align}
c_n&=\langle e^{nix},f(x)\rangle \\
&=\frac1{2\pi}\int_0^{2\pi}e^{-nix}f(x)dx
\end{align}$$

### Formal Notation

The Fourier Series transforms some function in the $L^2([0,2\pi],\mathbb C)$ space into a sequence of numbers. It establishes a one-to-one correspondence between the space of functions and the sequence space.

$$
\begin{align}
L^2([0,2\pi],\mathbb C)&\rightarrow L^2(\mathbb Z,\mathbb C) \\
f&\mapsto (c_n)_{n\in\mathbb Z} \\
c_n&=\frac{1}{2\pi}\int_0^{2\pi}e^{-2\pi inx}f(x)dx \\
&=\langle e^{2\pi inx},f\rangle
\end{align}$$

## The Fourier Transform

The full transformation transforms a function on the space of real numbers to a new function in the same space. Specifically, it transforms $x$ in the "time domain" into $\xi$ in the frequency domain.

$$\begin{align}
L^2(\mathbb R,\mathbb C)&\rightarrow L^2(\mathbb R,\mathbb C) \\
f(x)&\mapsto g(\xi)\triangleq F(f)(\xi) \\
g(\xi)\triangleq F(f)(\xi)&=\int_{-\infty}^{\infty} e^{-2\pi ix\xi}f(x)dx
\end{align}$$

## The Discrete Fourier Transform

Similarly, the **Discrete Fourier Transform (DFT)** transforms a sequence of numbers (an integer function) into another sequence of numbers of the same length. Again, it transforms a time representation $x$ into a frequency representation, notated as capital $X$. 
$$\begin{align}
L^2(\mathbb Z_n, \mathbb C)&\rightarrow L^2(\mathbb Z_n,\mathbb C) \\
x=(x_0,x_1,\dots,x_{n-1})&\mapsto X=(X_0,X_1,\dots,X_{n-1}) \\
X_k&=\sum_{i=0}^{n-1}e^\frac{2\pi ikl}{n}x_i
\end{align}$$
### Congruence

>[!definition] 
>In the space $\mathbb Z_n$, we say $a$ is **congruent** to $b$ when they have the equivalent modulo with $n$. Formally,
>
>$$a\equiv b \pmod n, a,b,n\in\mathbb Z, \text{ if } a-b=kn, \text{ for some } k$$

We can thus view our [space](The%20Fourier%20Series.md#Notation) $\mathbb Z_n$ as the set of **mod $n$ integers.**

>[!theorem]
>$$a\equiv b\pmod n\iff e^\frac{2\pi ia}{n}=e^\frac{2\pi ib}{n}$$

*Proof*:
$$\begin{align}
a\equiv b\pmod n&\implies a-b=kn \\
e^\frac{2\pi ia}{n}&=e^\frac{2\pi(b+kn)}{n} \\
&=e^{\frac{2\pi i b}{n}+2\pi ik} \\
&=e^\frac{2\pi ib}{n}e^{2\pi ik} \\
&=e^\frac{2\pi ib}{n} & \text{($e^{2\pi ik}=1$)} \\
&&\square
\end{align}$$

#### Properties of Congruence
If $a\equiv b\pmod n, c\equiv d\pmod n$, then
1. $a+c\equiv (b+d)\pmod n$
2. $ac\equiv bd\pmod n$

### The Fourier Matrix

>[!definition]
>Let the **n-th power of unity** be $\omega^n\triangleq e^\frac{2\pi i}{n}$. Note that $\omega^1=1$. 
>
>The **Fourier matrix** is a unitary $n\times n$ matrix $F_n$ such that $F_{jk}=\omega^{jk}$. We normalize the columns by multiplying the matrix by $\frac{1}{\sqrt{n}}$. 
>
>That is, $$F_n=\frac{1}{\sqrt{n}}(w^{jk})_{j,k\in[0..n-1]}$$

Equivalently,
$$
F_n=\frac{1}{\sqrt{n}}\begin{pmatrix}
1 & 1 & 1 & 1 & \cdots & 1 \\
1 & \omega & \omega^2 & \omega^3 & \cdots & \omega^{n-1} \\
1 & \omega^2 & \omega^4 & \omega^6 &\cdots & \omega^{2(n-1)} \\
1 & \omega^3 & \omega^6 & \omega^9 & \cdots & \omega^{3(n-1)} \\
\vdots & \vdots & \vdots & \vdots & \ddots & \vdots \\
1 & \omega^{n-1} & \omega^{2(n-1)} & \omega^{3(n-1)} & \cdots & \omega^{(n-1)(n-1)}
\end{pmatrix}
$$

This corresponds directly to the DFT. The columns of $F_n$ can be written as $F_n=\begin{pmatrix}\vec e_0 & \vec e_1 & \cdots & \vec e_{n-1}\end{pmatrix}$. Note that $\{\vec e_0, \vec e_1, \dots, \vec e_{n-1}\}$ forms an orthonormal basis, as shown [above](The%20Fourier%20Series.md#An%20Orthogonal%20Basis). 

The DFT represents any vector $x$ as a linear combination of the columns of $F_n$. We represent $x$ in the Fourier domain as $Fx$. 
$$\begin{align}
(Fx)_k&=\frac1{\sqrt n}\sum_{l\in\mathbb Z_n}\omega^{kl}x_l\\
x&=c_0\vec e_0+c_1\vec e_1+\dots+\vec e_{n-1} \\
\begin{pmatrix}
c_0 \\ c_1 \\ \vdots \\ c_{n-1}
\end{pmatrix}&=F_n^{-1}x
\end{align}$$


Practically, calculating this matrix multiplication takes $O(n^2)$ time, but the **Fast Fourier Transform (FFT)** can efficiently calculate it in $O(n\lg n)$ time. 

#### Square of the Fourier Matrix

>[!theorem]
>$$(F^2x)_k=x_{-k}=x_{n-k}$$
>That is, applying the Fourier transform twice "flips" the vector. 
>$$\begin{align}
x&=(x_0,x_1,x_2) \\
F^2x&=(x_2,x_1,x_0)
\end{align}$$

*Proof:*

>[!lemma]
>$$\sum_{k=0}^{n-1}e^\frac{2\pi imk}{n}=\begin{cases}0 & m\nmid n \\ n & n\mid m\end{cases}$$

*Proof:*
When $m \nmid n$, 
$$\begin{align}
\sum_{k=0}^{n-1}e^\frac{2\pi i mk}{n}&=\sum_{k=0}^{n-1}r^k, r=e^\frac{2\pi im}{n} \\
&=\frac{1-r^n}{1-r} \\
&=\frac{1-e^{2\pi im}}{1-e^\frac{2\pi im}{n}} \\
&=\boxed0
\end{align}$$

When $n\mid m$,
$$\begin{align}
\sum_{k=0}^{n-1}e^\frac{2\pi imk}{n}&=\sum_{k=0}^{n-1}1 \\
&=\boxed n \\
& & \square
\end{align}$$
Main proof, continued:
$$\begin{align}
(Fx)_k&=\sum_{l\in\mathbb Z_n}\omega^{lk}x_l \\
(F^2x)_k&=(F(Fx))_k \\
&=\frac1{\sqrt n}\sum_{l\in\mathbb Z_n}\omega^{kl}(Fx)_l \\
&=\frac1{\sqrt n}\sum_{l\in\mathbb Z_n}\omega^{kl}\left(\frac1{\sqrt n} \sum_{m\in\mathbb Z_n}\omega^{lm}x_m\right)\\
&=\frac1n\sum_{l\in\mathbb Z_n}\sum_{m\in\mathbb Z_n}\omega^{l(k+m)}x_m \\
&=\frac1n\sum_{m\in\mathbb Z_n}\sum_{l\in\mathbb Z_n}\omega^{l(k+m)}x_m \\
&=\frac1n\sum_{m\in\mathbb Z_n}\sum_{l\in\mathbb Z_n}e^\frac{2\pi il(k+m)}{n}x_m \\
&=\frac1{\cancel n}\sum_{m\in\mathbb Z_n}\cancel n\cdot\delta_{k+m}x_m & \left(\delta_a=\begin{cases}1 & a=0 \\ 0 & a\neq 0\end{cases}\right) \\
&=x_{-k}=x_{n-k} \\
& & \square
\end{align}$$

#### Eigenvalues

>[!theorem]
>$$F^4=I$$

*Proof:*
$$\begin{align}
F^4x&=F^2F^2x \\
&=F^2x_{-k} \\
&=x \\
\implies F^4&=I \\
& & \square
\end{align}$$

>[!theorem]
>The eigenvalues ($\lambda$) of $F$ are in $\{1,-1,i,-i\}$.

*Proof:*
$$\begin{align}
Fv&=\lambda v \\
FFv&=F\lambda v \\
&=\lambda Fv \\
&=\lambda^2 v \\
v&=F^4v \\
&=\lambda^4v \\
\lambda^4&=1 \\
\lambda&=1,-1,i,-i \\
& & \square
\end{align}$$

### Inverse Discrete Fourier Transform

The **Inverse Discrete Fourier Transform (IDFT)** is defined as 
$$\begin{align}
F^{-1}:L^2(\mathbb Z_n,\mathbb C)&\rightarrow L^2(\mathbb Z_n, \mathbb C) \\
y&\mapsto F^{-1}y \\
(F^{-1}y)_k&=\frac{1}{\sqrt{n}}\sum_{l\in\mathbb Z_n}\omega^{-kl}y_l
\end{align}$$
which corresponds with the matrix
$$F^{-1}=\frac1{\sqrt n}\begin{pmatrix}
1 & 1 & 1 & 1 & \cdots & 1 \\
1 & \omega^{-1} & \omega^{-2} & \omega^{-3} & \cdots & \omega^{-(n-1)} \\
1 & \omega^{-2} & \omega^{-4} & \omega^{-6} &\cdots & \omega^{-2(n-1)} \\
1 & \omega^{-3} & \omega^{-6} & \omega^{-9} & \cdots & \omega^{-3(n-1)} \\
\vdots & \vdots & \vdots & \vdots & \ddots & \vdots \\
1 & \omega^{-(n-1)} & \omega^{-2(n-1)} & \omega^{-3(n-1)} & \cdots & \omega^{-(n-1)(n-1)}
\end{pmatrix}$$

## Convolution Product

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

### Convolution Theorem

>[!theorem]
>The **Convolution Theorem** of $L^2(\mathbb Z_n, \mathbb C)$ states that if $X=F(x), Y=F(y)$, then 
>$$XY=F(x*y)$$ where $XY$ represents the element-wise (point-wise) product of $X$ and $Y$. 
>
>The inverse is also true. That is,
>$$x*y=F^{-1}(Fx)(Fy)$$

The Convolution Theorem allows us to perform certain operations quickly. 

### Efficient Convolution

From the Convolution Theorem, we know that we can a perform a convolution through a Fourier transform: $x*y=F^{-1}(Fx)(Fy)$. As it turns out, using the Fast Fourier Transform, calculating the righthand side is actually more efficient. 

### Polynomial Multiplication

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

Integer Multiplication

In the same manner as polynomial multiplication, integer multiplication for large numbers can be computed as a convolution. Applying the efficient algorithm, this becomes an application of the DFT (specifically the FFT).
## Background
### Empirical Risk Minimization

Recall the equation for [risk](Supervised%20Learning.md#Solving%20Supervised%20Learning%20Problems) (i.e., a measurement of how bad $h$ is):
$$\underbrace{F(h)}_{R(h)}=\frac1n\sum_{i=1}^n\ell(h(x_i), y_i)$$
>[!idea]
>The idea of **empirical risk minimization (ERM)** is to find $h^*$ that minimizes $F(h)$. $$h^*=\underset{h\in H}{\arg\min\, }F(h)$$
#### Linear Models

For [linear models](Perceptron.md#Review%20Linear%20Models), we have
- $h(x)=w^\top x+b$
- $H:\{w\mid w\in \mathbb R^d\}$
This leads us to $w^*=\arg\min_w F(w)$, where $F(w)=\frac1n\sum_{i=1}^n\ell(w^\top x_i, y_i)$.
### Motivating Gradient Descent

To approximate a function at a certain point, we use Taylor polynomials. That is, we say
$$\begin{align}
f(w_0+v)&\approx F(w_0)+\nabla F(w_0)^\top v & (1)\\
&\approx F(w_0)+\nabla F(w_0)^\top v+\frac12v^\top Hv & (2)\\
H_{ij}&=\frac{\partial^2 F}{\partial w_i \partial w_j} & \text{(the Hessian)}
\end{align}$$
The second approximation, using second-order Taylor polynomials, is more difficult to work with, so most algorithms will choose to simply use the linear approximation.

To find the critical points of a function, the "standard" process is to find the roots of the derivative of the function. But for many functions, it's impossible to find the roots in closed form. Even a 6th degree polynomial, for example, will have a 5th degree polynomial derivative, whose roots can't be found in closed form.

Instead, we use gradient descent to get closer to critical points.
## The Gradient Descent Algorithm

>[!algorithm]
>$$\begin{align}
\hline
&\text{\textbf{Gradient Descent Algorithm}} \\
\hline
&w_0 \leftarrow \text{initialize randomly} \\
&\textbf{for } t=1\dots T: \\
&\quad w_t\leftarrow w_{t-1}-\eta_t\nabla F(w_{t-1}) \\
\hline
\end{align}$$

$\eta_t$ is the **learning rate**. It has a subscript $t$ because sometimes people have different learning rates for different points in the learning.

In general, we want the largest learning rate we can get away with—that is, the largest learning rate that won't diverge.

Note that gradient descent only finds local extrema, and because it relies on the derivative, can only work on smooth functions. For example, it can't target $\ell_{0/1}$. Still, many machine learning algorithms still use gradient descent on unsmooth functions—it has yet to be proven to work, but it empirically is successful.

$$\begin{align}
w_t&\leftarrow w_{t-1}-\eta_t\nabla F(w_{t-1}) \\
F(w_{t-1}+v)&\approx F(w_{t-1})+\nabla F(w_{t-1})^\top v & \text{(Taylor approx)}\\
F(w_{t-1}\underbrace{-\eta_t\nabla F(w_{t-1})}_{\text{Gradient descent}}) &\approx F(w_{t-1})-\nabla F(w_{t-1})^\top \eta_t\nabla f(w_{t-1}) \\
&\approx F(w_{t-1})-\eta_t\underbrace{\nabla F(w_{t-1})^\top\nabla F(w_{t-1})}_{\geq 0}
\end{align}$$
Because we're decreasing by a number $\geq 0$, we know that we're getting "closer" to the minimum. Also note that because the approximation only works when $v$ is small, $\eta$ cannot be too large.
## Newton's Method

Newton's method takes advantage of the second-order Taylor expansion.
$$f(w_t+v)\approx F(w_t)+\nabla F(w_t)^\top v+\frac12v^\top Hv$$
>[!idea]
>Minimize the quadratic approximation explicitly.
>$$v=\underset{v}{\arg\min\, }F(w_t)+\nabla F(w_t)^\top v+\frac12v^\top Hv$$

$$\begin{align}
\frac{\partial(F(w_t)+\nabla F(w_t)^\top v+\frac12v^\top Hv)}{\partial v}&=\nabla F(w_t)+Hv = 0 \\
v&=-H^{-1}\nabla F(w_t)
\end{align}$$

We can then use the update
$$w_t\leftarrow w_{t-1}-H^{-1}\nabla F(w_{t-1})$$

With Newton's method, the learning jumps are much bigger, under the assumption that the second-order approximation will be more accurate. Note too that there is no learning rate.

Because the Hessian (the second derivative) can tell us how "flat" a function is (acceleration), Taylor's method will make large steps in these areas (dictated by $H^{-1}$). Because of this, it can still diverge.

When Taylor's method works, it converges much, much faster than gradient descent. 

### When $H$ Is Singular

When $H$ isn't invertible, it indicates that in some direction, the function is essentially flat, meaning that to optimize we'd have to move infinitely far in that direction.

In practice, we can choose to optimize the other parameters, and then choose some solution on that flat line.

## When Gradient Descent Works

### Convexity

If $w$ and $w'$ are two points on the $x$-axis of some function $F$, any point between them can be written as $\alpha w + (1-\alpha)w'$. Similarly, we can say that any point between two points on the $y$-axis $F(w), F(w')$ can be written as $\alpha F(w)+(1-\alpha)F(w')$. 

![](Pasted%20image%2020230920140732.png)

We can imagine that $(w, F(w)), (w', F(w'))$ are the intersection points above, for example. 

We say a function is convex when this line is always greater than or equal to the function in $[w, w']$. That is, 
$$\alpha f(w)+(1-\alpha)f(w')\geq F(\alpha w+(1-\alpha)w')$$

An alternative definition is that the tangent line is always below the function. That is,
$$F(w)+\nabla F(w)^\top (w-v)\leq F(v)$$
### $L$-Smoothness

>[!definition] Definition 1
>A function is **$L$-smooth** if there exists some constant $L$ such that for all $w, w'$, 
>$$||\nabla F(w)-\nabla F(w')||\leq L||w-w'||$$

- Conceptually, this means that we can always draw a tangent line that lower-bounds the function
- A bigger $L$ is less smooth
- If $\nabla F$ is $L$-Lipshitz, then $F$ is $L$-smooth

>[!definition] Definition 2
>A function is **$L$-smooth** if
>$$F(w')\leq \underbrace{F(w)+\nabla F(w)^\top(w'-w)}_{\text{1st-order Taylor}}+L||w'-w||^2$$

- That is, at every point we can draw a quadratic function that upper bounds the function
- It is a "control" on the rate of growth

## Proof of Convergence

>[!theorem]
>The update step of gradient descent will converge when $F$ is [convexity](Gradient%20Descent.md#When%20Gradient%20Descent%20Works#Convexity) and [smooth](Gradient%20Descent.md#When%20Gradient%20Descent%20Works#$L$-Smoothness):
>$$w_{t+1}\leftarrow w_t-\frac1L\nabla F(w_t)$$

Note that we use a step size of $\frac1L$, where $F$ is $L$-smooth.

>[!lemma] Lemma 1
>$$\forall t, F(w_{t+1})\leq F(w_t)$$
>That is, $F(w_{t})$ is always non-increasing.

**Proof.** 
By our definition for $w$'s update,
$$\begin{align}
w_{t+1}&=w_t-\frac1L\nabla F(w_t)\\
\nabla F(w_t)&=L(w_t-w_{t+1}) \\
F(w_{t+1})&\leq F(w_t)+\nabla F(w_t)^\top(w_t)(w_{t+1}-w_t)+L||w_t-w_{t+1}||^2 \\
&\leq F(w_t)+\underbrace{L(w_t-w_{t+1})}_{\text{Sub. line 2}}{}^\top(w_{t+1}-w_t)+\underbrace{L(w_t-w_{t+1})^\top(w_t-w_{t+1})}_{\text{Expand}} \\
&\leq F(w_t)-L(w_t-w_{t+1})^\top\underbrace{(w_t-w_{t+1})}_{\text{Pull out neg.}}+L(w_t-w_{t+1})^\top(w_t-w_{t+1}) \\
&\leq F(w_t)
\end{align}$$

>[!lemma] Lemma 2
>If $\vec w$ is globally optimal, $w_t \rightsquigarrow w^*$.
>

**Proof.**
By convexity,
$$\begin{align}
F(w^*)&\geq F(w_t)+\nabla F(w_t)^\top(w^*-w_t) \\
F(w^*)&\geq F(w_t)+\underbrace{L(w_t-w_{t+1})}_{\text{From update defn.}}{}^\top(w^*-w_t) \\
F(w_t)-F(w^*)&\leq-L(w_t+w_{t+1})^\top\underbrace{(w_t-w^*)}_{\text{Pull out neg.}} \end{align}$$

Now, we do some clever manipulation to get an expression for $(w_t-w_{t+1})^\top(w_t-w^*)$.
$$\begin{align}
||w_{t+1}-w^*||^2&=||w_{t+1}\underbrace{-w_t+w_t}_\text{Tautology}-w^*||^2 \\
&=||w_{t+1}-w_t||^2+||w_t-w^*||^2-2\underbrace{(w_t-w_{t+1})}_\text{Pull out neg.}{}^\top(w_t-w^*) \\
(w_t-w_{t+1})^\top(w_t-w^*)&=\frac12\left(||w_{t+1}-w_t||^2+||w_t-w^*||^2-||w_{t+1}-w^*||^2\right) \\
F(w_f)-F(w^*)&\leq \frac L2\left(||w_{t+1}-w_t||^2+||w_t-w^*||^2-||w_{t+1}-w^*||^2\right) \\
F(w_{t+1})-F(w_t)&\leq-\frac L2||w_f-w_{t+1}||^2 \\
\end{align}$$
Adding the previous two inequalities,
$$\begin{align}
F(w_{t+1})-F(w^*)&\leq-\frac L2()
\end{align}$$






## Things to study
- hessian
- L-lipshitz
- matrix cookbook
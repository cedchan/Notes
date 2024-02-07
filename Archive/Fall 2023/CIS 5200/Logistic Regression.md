## Model Definition
Logistic regression is a [supervised](Supervised%20Learning.md) algorithm for binary classification. 

- Labels: $y\in\{+1,-1\}$
- Model: Linear models

Previously, when using linear models for binary classification, we used the $\mathrm{sign}$ function. That is, we looked at whether the value of $w^\top x$ was positive or negative and classified by that.

Logistic regression introduces a new method. Instead, we create a probability of being in either category:
$$w^\top x\rightarrow[0,1]$$
That is, if our previous model was $h(x)=\mathrm{sign}(w^\top x)$, the logistic regression model is 
$$h(x)=\sigma(w^\top x), \qquad\underbrace{\sigma(v)}_{\mathclap{\text{``squashing"}}}\in[0,1]$$
### Sigmoid Function

The particular "squashing" function $\sigma$ we're using is called the Sigmoid.

>[!definition]
>The **Sigmoid function** is defined as 
>$$\sigma(v)=\frac{1}{1+\exp(-v)}$$

Graphically, 
![](Pasted%20image%2020230927145441.png)
Clearly, the Sigmoid function takes any real-number input and squashes it in the range $[0,1]$. 

### Loss

With our function $h(x)=\sigma(w^\top x)$, our loss $\ell$ is defined as follows
$$\ell(h(x), y)=\begin{cases}
-\log h(x) & y=+1 \\
-\log(1-h(x)) & y=-1
\end{cases}$$
To understand what this loss is doing, note the following:

For $y=+1$, 
$$\begin{align}
h(x)\rightarrow0&\implies-\log h(x)\rightarrow\infty \\
h(x)\rightarrow1&\implies1-\log h(x)\rightarrow 0
\end{align}$$
For $y=-1$,
$$\begin{align}
h(x)\rightarrow0&\implies-\log(1-h(x))\rightarrow0 \\
h(x)\rightarrow1&\implies-\log(1-h(x))\rightarrow\infty
\end{align}$$
>[!error]
>Look at this again

To make the piecewise loss function cleaner, let's rewrite with the following form:
$$\begin{align}
h(x)=\sigma(w^\top x)&\implies\ell(h(x),y)=\underbrace{\log(1+\exp(-yw^\top x))}_\text{Logistic loss} \\
\hat R(w)&=\frac1n\sum_{i=1}^n\log(1+\exp(-y_iw^\top x_i))
\end{align}$$
When $y=+1$,
$$\begin{align}
-\log(h(x))&=-\log\underbrace{\frac{1}{1+\exp(-w^\top x)}}_{\sigma(w^\top x)=h(x)} \\
&=-(\log 1-\log(1+\exp(-w^\top x))) \\
&=\log(1+\exp(-w^\top x)) \\
&=\log(1+\exp(\underbrace{-yw}_{y=1}\,^\top x))
\end{align}$$
When $y=-1$,
$$\begin{align}
-\log(1-h(x)&=-\log\left(1-\frac1{1+\exp(-w^\top x)}\right) \\
&=-\log\left(\frac{\exp(-w^\top x)}{1+\exp(-w^\top x)}\right) \\
&=-\log\left(\frac{\exp(-w^\top x)}{1+\exp(-w^\top x)}\cdot\frac{\exp(w^\top x)}{\exp(w^\top x)}\right) \\
&=-\log\left(\frac{1}{1+\exp(w^\top x)}\right) \\
&=-\log(1+\exp(w^\top x)) \\
&=\log(1+\exp(-yw^\top x))
\end{align}$$


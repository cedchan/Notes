## Model Setup

**Setting:** Binary classification. That is, $y_i \in\{+1,-1\}$
**Models:** $h(x)=\mathrm{sign})w^\top x$
**Goal:** Find a separating hyperplane with maximum margin

### Distance to a Hyperplane

Consider a datapoint $x$ and the point on a hyperplane defined by the weight vector $w$ closest to it, $x_p$. The distance between it is defined by the vector $x-x_p$, whose distance is $\sqrt{d^\top d}=||d||$ (Pythagorean theorem). Then, $d=\alpha w$, that is, some constant multiplied the weight vector (which, recall, is orthogonal to the hyperplane).

We know $w^\top x_p=0$ because $x_p$ is on the hyperplane.
$$\begin{align}
w^\top(x-d)&=0 \\
w^\top(x-\alpha w)&=0 \\
w^\top x-\alpha w^\top w&=0 \\
\alpha&=\frac{w^\top x}{w^\top w}=\mathrm{proj}_wx \\
d=\alpha w&=\frac{w^\top x}{w^\top w}w \\
d^\top d&=\alpha^2 w^\top w \\
\sqrt{d^\top d}&=\sqrt{\frac{(w^\top x)^2}{(w^\top w)^2}w^\top w} \\
&=\frac{|w^\top x|}{\sqrt{w^\top w}}
\end{align}$$

In other words, the distance from a point $x$ to hyperplane $w$ is the norm of the projection of $x$ onto $w$.
>[!error]
>review
## Hard Margin SVM

Recall now the definition of the margin:
$$\gamma(w,D)=\min_i\frac{|w^\top x_i|}{\sqrt{w^\top w}}$$

Then we can optimize to get $w^*=\max_w\gamma(w, D)$ such that $\forall i, y_iw^\top x_i\geq 0$ (that is, that correctly classifies).

Plugging in the definition for margin, this is
$$w^*=\max_w\min_i\frac{|w^\top x_i|}{\sqrt{w^\top w}}\text{\quad s.t. }\forall i, y_iw^\top x_i\geq 0$$
We want to rephrase, this, however, such that it isn't a constrained optimization problem. 

Note that $w, cw$ are the same hyperplane, for $c\neq 0$. Suppose $w^*$ is optimal. We can choose $c$ such that $\min_i|(cw^*)^\top x_i|=1$. We argue that $cw^*$ is still optimal.

>[!error]
>look at notes to prove this whole part

Then, we can rewrite our definition of $w^*$ as 
$$\begin{align}
w^*&=\max_w\min_i\frac{|w^\top x_i|}{\sqrt{w^\top w}} &\text{s.t. }\forall i, y_iw^\top x_i\geq 0, \min_i|w^\top x_i|=1 \\
&=\max_w\frac1{\sqrt{w^\top w}}=\min_ww^\top w &\text{s.t. }\forall i, y_iw^\top x_i\geq 0, \min_i|w^\top x_i|=1 \\
&=\min_ww^\top w &\text{s.t. } \forall i, \underbrace{y_iw^\top x_i\geq 1}_\text{(min val for $y$ of 1)}
\end{align}$$
Now, we want to show:
1. $\forall i, y_iw^\top x_i\geq0$
2. $\min_i|w^{*\top}x_i|=1$

Suppose (2) is false. Then $\min_i|w^{*\top}x_i|=p, p>1$. Define $$\begin{align}
w^{**}&=\frac1pw^* \\
&=
\end{align}$$
Thus, we have the **Hard Margin SVM**:
$$\min_w w^\top w \text{\quad s.t. } \forall i, y_i, w^\top x_i\geq 1$$
It's called the hard margin because there's no "slack" allowed for here. 

## Soft Margin SVM

The version that is actually used allows some slack, called $\xi$. Then, we pay a cost $c$ for each time that you provide this slack. That is,
$$\min_{w,\xi_i} w^\top w+c\sum_{i=1}^n\xi_i \text{\quad s.t. } \forall i, y_iw^\top x_i\geq1-\xi, \forall i, \xi_i\geq 0$$
Clearly, as $c$ gets larger, we "care" more about every datapoint aligning perfectly. 

At the optimum, we actually know what value $\xi$ should take on:
$$\xi_i=\begin{cases}
1-y_iw^\top x_i & y_iw^\top x_i<1 \\
0 & y_iw^\top x_i\geq 1
\end{cases}\iff\xi_i=\max(0, 1-y_iw^\top x_i)$$
We can now plug this definition back into our equation to get

$$\min_w w^\top w+c\sum_{i=1}^n\max(0, 1-y_iw^\top x_i)$$

LOOK AT THE LOSS FUNCTION GRAPH
compared to logistic, cares less about neg loss, then past 0 x drops to 0 y immediately

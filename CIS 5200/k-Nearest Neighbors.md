Given a dataset $\mathcal D$, let
- $N_{\vec x}$: Set of nearest neighbors in $\mathcal D$ to $\vec x$ ($N_{\vec x} \subseteq \mathcal D$).
- $\forall \vec z_1 \in \mathcal D \setminus N_{\vec x}, \forall \vec z_2\in N_{\vec x}, \mathrm{dist}(\vec x, \vec z_1) \geq \mathrm{dist}(\vec x, \vec z_2)$ (that is, we have the closest $k$ neighbors)
- $h_{NN}(\vec x)=\mathrm{mode}(\{y\mid (\vec x, y)\in N_{\vec x}\})$ (that is, takes a majority vote of the $k$ closest neighbors)

>[!hint]
>Typically, an odd $k$ is chosen to avoid having to explicitly code tie-breakers.

## Distances

The performance of k-NN models is heavily dependent on the distance measurement used.

We'll take a look at a couple of them, for $\vec x \in \mathbb R^d$.

### Minkowski Distance

>[!definition]
>The **Minkowski Distance** is defined as $$\mathrm{dist}(\vec x, \vec z)=\left(\sum_{i=1}^d\left|\left[\vec x\right]_i-\left[\vec z\right]_i\right|^p\right)^\frac{1}{p}$$

Note here that $\left[\vec x\right]_i$ denotes the $i$-th element of $\vec x$.

#### Special Cases
- $p=1$
	This is the **Manhattan Distance**—that is, the sum of the differences between all corresponding indices.
	> **Example.** For $(1, 2), (3, 4)$, we have $|1-3|+|2-4|$. 
- $p=2$
	From the formula, we can see that this is just the **Euclidean Distance**.
- $p=\infty$
	This is the maximum difference between any of the corresponding indices.

### Normalized Compression Distance

Suppose we have a document $x$: 
- $x_1 = \text{``Machine learning"}$
- $x_2=\text{`` is fun"}$
- $x = x\oplus x_2=\text{``Machine learning is fun"}$, where $\oplus$ denotes string concatenation

The intuition is that if two documents are similar, they'll be able to compress more (normalized for length).

>[!definition]
>The **Normalized Compression Distance** of two documents $x, z$ is defined as
>$$\mathrm{NCD}(x, z)=\frac{\mathrm{gzlen}(x\oplus z)-\min(\mathrm{gzlen}(x), \mathrm{gzlen}(z))}{\max(\mathrm{gzlen}(x), \mathrm{gzlen}(z))}$$
>where $\mathrm{gzlen}(x)$ is the length of $x$ after being compressed by $\mathrm{gzip}$.

## Where k-NN Fails

### Images

If every pixel of an image are shifted by 1, the Euclidean distance (and indeed, Minkowski distance more generally) blows up, despite the two images being practically identical.

Similarly, if all the red values of each pixel are shifted by 1, distance also explodes.

### Curse of Dimensionality

Consider the unit cube $x_i\in[0, 1]^d$ drawn uniformly at random.

Then the volume of the cube $l^d=\frac{k}{n} \implies l=\left(\frac{k}{n}\right)^\frac1d$.

|$k$|$n$|$d$|$l$|
|-|-|-|-|
|1|100|2|0.1|
|1|100|10|0.63|
|1|100|100|0.95|
|1|100|1000|0.9954

That is, as dimensions increase, points become farther and farther away, so distance becomes less and less informative. The notion of "nearest" becomes meaningless when everything is relatively the same distance away.

**Another argument.** Consider $x\sim\mathcal N(0, 1)$. When we graph $||x||^2$, we see that most of the distribution is distance 0 from the origin. But as we increase dimensions of the Gaussian, all the points get shifter further and further away. 

#### Learning in High Dimensions

So how, despite the curse of dimensionality, do we learn on tasks with high dimensions? The answer is that the distributions we draw from are not, in fact, typically uniformly distributed. 

Instead, most datasets lie on some manifold in high-dimensional space. That is, they are locally Euclidean. 
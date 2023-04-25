**Problem:** Given a boolean sequence $c_1 \land c_2 \land \dots \land c_k$, where each $c_i$ is a clause of the form $(x_m \lor x_n)$, find assigments for the boolean values of each $x_i$ such that the entire sequence is true.

>**Example.** 
>$(x_1 \lor x_3) \land (x_2 \lor \lnot x_1) \land (\lnot x_2 \lor x_3)$

## Deterministic Solution

The key insight is the following equivalence
$$
(a \lor b)\equiv (\lnot a\implies b)\land (\lnot b\implies a)
$$
Thus, we can create the following algorithm:
1. Create a directed "implication" graph with $2n$ vertices $x_i, \lnot x_i$, where $n$ is the number of variables, and $2k$ edges that follow from the above relation (e.g., in the previous example, for clause $(x_1\lor x_3)$, draw edges $(\lnot x_1, x_3), (\lnot x_3, x_1)$).
2. Run [Kosaraju's algorithm](Strongly%20Connected%20Components.md) on the graph to find SCCs. If there exists a pair $x_i, \lnot x_i$ such that both elements of the pair are in the same SCC, return that there is no solution. Otherwise, all the values in the same SCC have the same truth value.

### Alternative Solution

Draw a [bipartite](Bipartiteness.md#Definitions) graph, where one side consists of the right elements of each clause, and the other consists of the left elements. Connect each clausal pair, and connect each other clause $x_i, \lnot x_i$. Run the [bipartiteness algorithm](Bipartiteness.md#Algorithm) to see if the graph is indeed 2-colorable. One color is true, one is false. If the graph is not 2-colorable, there is no solution.

## Probabilistic Solution

### Algorithm

```
2-SAT():
	Arbitrarily assign truth values
	for i = 1 to 2mn^2:
		Choose an arbitrary unsatisfied clause
		Choose uniformly at random one of the literals and switch its value
	if a valid truth assignment was ever found, return it, otherwise false
```

### Probabilistic Analysis

Let $X$ be a random variable denoting the number of correct values in our assignment. At each step, we flip the value of some literal. This gives the following:
$$
\begin{gather}
\Pr[X_{i+1}=1\mid X_i=0]=1 \\
\Pr[X_{i+1}=j+1 \mid X_i=j]\geq\frac12 \\
\Pr[X_{i+1}=j-1\mid X_i=j]\leq\frac12
\end{gather}
$$
In the first line, since every assignment is wrong, changing any of them must always increase the number of correct assignments. For the others, we flip some literal of the clause, which is correct with a probability of $\frac12$, yielding the above probabilities (intuitively).

Let $T_j$ be the expected number of steps to reach $n$ from state $j$, where again $n$ is the number of literals (i.e., all of the assignments are correct).

$$\begin{align}
T_0&=T_1+1 \\
T_n&=0 \\
T_j&=\frac12(1+T_{j-1})+\frac12(1+T_{j+1}) & \text{(LOE)} \\
&=1+\frac{T_{j-1}}2+\frac{T_{j+1}}2 & 1\leq j\leq n-1 \\
2T_j&=2+T_{j-1}+T_{j+1} \\
T_j-T_{j+1}&=2+T_{j-1}-T_j\\
&=2+2+T_{j-2}-T_{j-1} \\
&=2+2+2+T_{j-3}-T_{j-2} \\
& \ \vdots \\
&=2+2+2+\dots +2+T_0-T_1 \\
&=2j+1 & (T_0-T_1=1)
\end{align}$$

To get an upper bound on the expected number of steps needed given our algorithm, we can find $T_0$.

$$\begin{align}
T_0&=(T_0-T_1)+(T_1-T_2)+\dots+(T_{n-1}-T_n) \\
&=\sum_{j=0}^{n-1}T_j-T_{j+1} \\
&=\sum_{j=0}^{n-1}2j+1 \\
&=n^2
\end{align}$$
Let $Z$ be the number of steps until the algorithm returns the correct answer. Then, given $m$ segments and $n$ literals, we find the following probability using Markov's Inequality:
$$\Pr[Z>2n^2]\leq\frac{n^2}{2n^2}=\frac12$$
We do this $2n^2$ step $m$ times (for total $2mn^2$ iterations), so the probability of success is $1-\left(\frac12\right)^m$. 
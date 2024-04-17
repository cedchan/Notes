---
tags:
  - graph-algorithms
---
## Problem

The problem Bellman-Ford solves is a more general case of the single-source shortest path problem that [Dijkstra's algorithm](Dijkstra's%20Algorithm.md) solves. We can't use the exact same formulation though, because of the following claim.

>[!claim]
>There exist directed graphs $(G, w)$ such that no shortest path exists from $s$ to $u$.

**Proof.** Consider a path from $s$ to $u$ that contains some cycle $C$ with negative weight (that is, $\sum_{e\in C}w(e)<0$). We can decrease the path weight infinitely by looping through $C$ an arbitrary number of times.
$$\tag*{$\square$}$$

Thus our problem is restricted to graphs without negative-weight cycles.

Note also where Dijkstra's breaks down here: we can no longer say that the shortest path out of $S$ is the shortest path, because an initially long-looking path could end up being shorter if it has a large negative weight down the line.
## Algorithm

>[!algorithm]
>1. Repeat $x=n-1$ times:
>	1. Scan through edges $(u, v)$
>	2. $D(v)\gets\min\{D(v), D(u)+w(u,v)\}$
>2. Output $D$

Intuitively, each iteration we move closer to the optimal solution, while avoiding the assumptions that Dijkstra's makes about positive edge weights. 

The remaining question is how we chose $x$, the number of iterations. We show why $n-1$ guarantees all edges are found in the next section.

In fact, this result allows us to run a final $n$-th iteration, during which if any $D(u)$ updates, we know that a negative-weight cycle exists, so the algorithm fails the input.
## Correctness

>[!lemma]
>Consider $u\in V$ such that the true shortest path from $s$ to $u$ uses $k$ edges. Then, after $k$ iterations, $D(u)=D^*(u)$, the length of the true shortest path.

>[!lemma]
>Consider $u\in V$ such that the true shortest path from $s$ to $u$ is a simple path using $k\le n$ hops. Then, after $k$ iterations, $D(u)=D^*(u)$ stays

**Proof.** We prove by induction on $k$.

*Base Case:* $k=0$. $s$ is the only vertex such that $D(s)=0$. The lemma trivially holds.

*IS:* Suppose by induction that the lemma holds for $k$. We want to show that it holds for $u$ such that the shortest path for $u$ uses $k+1$ edges.

Recall that the subpath of any shortest path is still a shortest path ([proof](Dijkstra's%20Algorithm.md#Motivation)). Consider $z$, the vertex on the shortest path of $u$ that lies right before $u$. The shortest path $s\rightsquigarrow z$ uses $k$ edges, so by the IH, $D(z)=D^*(z)$. Since $D(u)$ is not yet its optimal, 
$$\begin{align}
D(u)&\le D(z)+w(z,u) \\
&=D^*(z)+w(z,u) \\
&=D^*(u)\\
&\tag*{$\square$}
\end{align}$$
Then, since we say that shortest paths are simple, after $n-1$ iterations we get all shortest paths.

>[!lemma]
>If there exists some negative weight cycle, then iteration $n$ does an update.

**Proof.** We prove the contrapositive: if iteration $n$ does no update, then there must not exist some negative weight cycle.

Pick any cycle $C$. Since we have no updates,
$$\sum_{(u,v)\in C}(D(v)-D(u))\leq\sum_{(u,v)\in C}w(u,v)$$
This is because otherwise we would've updated $D(v)\gets D(u)+w(u,v)$. Then, 
$$\sum_{(u,v)\in C}(D(v)-D(u))=0$$
because the above summation has $D(v)$ and $-D(v)$ exactly once each for each vertex in $C$. This shows that there are no negative-weight cycles.
$$\tag*{$\square$}$$

## Runtime

Without negative-weight cycles, we use $O(mn)$ time. If there is, then we declare it so.
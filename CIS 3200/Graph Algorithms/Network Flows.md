---
tags:
  - graph-algorithms
---
## Axioms of Flows

Intuitively, the flow is the amount of "stuff" that can get from one point in a graph to another. The idea is that in all of the internal nodes of such a path, nothing is being created or destroyed—rather, everything starts at a single source and ends at a single target.

>[!definiton]
>The **flow** of a graph with edge capacities $c:E\to\mathbb R_{\ge0}$ is a function $f:E\to\mathbb{R_{\ge0}}$ that represents the net number of units transferred along an edge from one node to another.

Flow functions must satisfy the following axioms:
1. Capacity constraint—the flow is at most the capacity: $\forall e\in E, f(e)\le c(e)$
2. Flow conservation—the number of units entering a vertex is the same as the number that exists the vertex: $\forall v\in V\setminus\{s, t\}$,$$\underbrace{\sum_{(s,u)\in E}f(s,u)}_{\substack{\text{what the source }s\\\text{creates}}}=\underbrace{\sum_{\substack{u\in V\\(u,v)\in E}}f(u,v)}_\text{what enters $v$}=\underbrace{\sum_{\substack{u\in V\\(v,u)\in E}}f(v,u)}_\text{what leaves $v$}=\underbrace{\sum_{(u,t)\in E}f(u,t)}_{\substack{\text{what the sink } t\\\text{absorbs}}}$$
3. Non-negativity: $\forall e\in E, f(e)\ge0$

Further, when we talk about "maximizing" flow, we mean maximizing the **flow value** $|f|$, which is defined as the flow coming out of $s$. That is,
$$|f|=\sum_{(s,u')\in E}f(s,u')-\sum_{(u,s)\in E}f(u,s)$$
But since we know by flow conservation that all nodes except $s$ and $t$ will have a net flow of 0, an equivalent definition is
$$|f|=\sum_{(u,t)\in E}f(u,t)-\sum_{(t,u')\in E}f(t,u')$$

**Proof.** Consider the flow of all internal vertices.
$$\begin{align}
O&=\sum_{v\in V\setminus\{s,t\}}\left(\sum_{(u,v)\in E}f(u,v)-\sum_{(v, u')\in E}f(v,u')\right) \\
&=\sum_{(a,b)\in E}(f(a,b)-f(a,b))
\end{align}$$
Then, the only things that don't cancel are the source and sink.
## Problem

>[!problem]
>**Inputs:**
>- Directed graph $G=(V,E)$
>- Edges have capacities $c:E\to \mathbb R_{\ge0}$ that limit the amount of "stuff" that can be sent on the edge
>- Source $s$
>- Sink $t$
>
>**Output:** $f:E\to\mathbb R_{\ge0}$ such that it is a feasible flow and is maximized

As it turns out, the max-flow problem allows us to solve many similar and related problems. The general strategy for showing this is that we take the new problem and convert it into a new graph that is solvable using the max-flow problem with the same solution.

>[!claim]
>If you can solve the max-flow problem, you can determine if a bipartite graph has a perfect matching.

The following visualization helps to illustrate this: Given a bipartite graph, we direct all edges as $A\to B$, and create a source $s$ that leads to all vertices in $A$ and a sink $t$ that all edges in $B$ lead to. If there's a perfect matching, the maximum flow of this graph will be exactly $|A|$. 

Note that in a perfect matching, we'd have no "intersections" of paths from $s$ to $t$. In this case, since each edge has max 1, we have max flow $|A|$. Conversely, if we can't achieve max flow $|A|$, then there must be some "bottleneck" between $A$ and $B$, where two edges are forced to lead to the same node (hence being throttled from contributing flow $1+1$ to just $1$).

![100%x300](Drawing%202024-03-27%2016.23.01.excalidraw.md)

>[!claim]
>The max-flow problem for a single source is sufficient to solve the max-flow problem for multiple sinks and sources.

The strategy here is that we create a new $s$ and $t$, where we have edges from $s$ to all sources, as well as edges from all sinks to $t$. Each of these edges has capacity $\infty$ so as not to introduce any new bottlenecks. 

![|100%](Drawing%202024-03-27%2016.31.28.excalidraw.md)

>[!claim]
>The max-flow problem solves this modification as well: Given a graph $G=(V,E)$ and source $s$, sink $t$, and capacities on the vertices rather than edges (that is, $c:V\to\mathbb R_{\ge0}$), find the max flow.

Again we take the approach of making a transformation. If we want the bottleneck to go from the vertex to edges, we can split each vertex $u$ into $u_0$ and $u_1$, where all edges going into $u$ now go into $u_0$ and all going out of $u$ now go out of $u_1$. Finally, we connect $u_0$ and $u_1$, with the capacity $c(u)$ put on $(u_0, u_1)$.

![100%x125](Drawing%202024-03-27%2016.34.27.excalidraw.md)

## Claims about Flows

>[!claim]
>Suppose $G=(V,E), c:E\to\mathbb R_{\ge0}$ such that $f:E\to\mathbb R_{\ge0}, f(e)=0,\forall e$.
>
>For a path $p:s\to t$ in $G$ such that $c(p)=\min\{c(e)\mid e\in p\}$, let $f_p:E\to\mathbb R_{\ge0}$ and
>$$f_p(e)=\begin{cases}c(p) & e\in p \\ 0 &\text{o.w.}\end{cases}$$
>
>Then, $f'=f+f_p$ is a feasible flow and $|f'|=|f|+c(p)$.

This claim in fact only holds in the first step, when the initial flow $|f|$ is all $0$. Let's look at a more general claim:

>[!claim]
>Given $G=(V,E),c:E\to\mathbb R_{\ge0},f:E\to\mathbb R_{\ge0}$ such that $f$ is a feasible flow.
>
>Suppose $p$ is a path $s\to t$ such that $\forall e\in p$, either
>1. $c(e)-f(e)>0$ or
>2. $e=(u,v), e'=(v,u)\in E, f(e')>0$
> 
>Let $$c(p)=\min\begin{cases}c(e)-f(e) & e\text{ in case 1} \\ f(e') & e\text{ in case 2}\end{cases}$$
>
>Consider $$f_p(e)=\begin{cases}c(p) & e\in p \text{ and case 1} \\
>-c(p) & e'\in p\text{ and case 2} \\
>0 & \text{o.w.}\end{cases}$$
>
>Then, $f'\triangleq f+f_p$ is feasible and $|f'|=|f|+c(p)$.

## Ford-Fulkerson Algorithm

**Scaffolding:**
- We start with a feasible flow $f(e)=0$.
	- Then, we repeatedly update $f$ until it gets stuck.
- Let $G_f$ be the **residual graph** where
	- For $e\in E,c_f(e)=c(e)-f(e)$
	- For $e$ such that $e'\in E$, $c_f(e)=f(e')$

>[!algorithm] Ford-Fulkerson Algorithm
>1. Initialize $\forall e\in E,f(e)\gets0$.
>2. While BFS finds path $s\to t$ in $G_f$: 
>	1. Push flow and update $f\gets f+f_p$
>3. Output $f$

### Runtime

Suppose that $c:E\to\mathbb Z_{\ge0}$ such that the true max flow is $F$.

Each iteration of the while loop takes $O(n+m)$ time to run BFS and construct $G_f$. We execute this $O(F)$ times at most because we necessarily increase our flow by at least 1 each iteration, yielding total $O(F(n+m))$ time.

As it turns out, though, $F$ is exponential in the input size, so the algorithm is overall exponential in the input size, which is slow.

### Correctness

>[!claim] Simple Claim
>For any feasible flow $f$, for any $(s,t)$ cut $S$, 
>$$\max_f|f|\le \min_SC(S)$$ 

**Proof.** 
$$\begin{align}
|f|&=\sum_{v\in S}\left(\sum_{\substack{u'\in V\\(v,u')\in\in E}}f(v,u')-\sum_{\substack{u\in V\\(u,v)\in\in E}}f(v,u')\right)\\
&=\sum_{(u,v)\in E}\begin{cases}
0 & u,v\in S \\
0 & u,v\notin S \\
f(u,v) & u\in S,v\notin S \\
-f(u,v) & u\notin S, v\in S 
\end{cases}\\
\end{align}$$

>[!claim] Final Claim
>Suppose $f$ is feasible and there does not exist an $s\to t$ path in $G_f$. Then, 
>$$\exists (s,t)\text{-cut } S\text{ s.t. } C(S)=|f|$$

**Proof.** Let $$S=\{v\mid v\text{ is reachable from $s$ in $G_f$}\}$$
Then,
$$\begin{align}
|f|&=\sum_{\substack{u\in S\\(u,v)\in E\\v\notin S}}f(u,v)-\sum_{\substack{u\notin S \\(u,v)\in E\\v\in S}}f(u,v) \\
&=\sum_{\substack{u\in S\\(u,v)\in E\\v\notin S}}c(u,v)-\sum_{\substack{u\notin S\\(u,v)\in E\\v\in S}}0 \\
&=\sum_{\substack{u\in S\\(u,v)\in E\\v\notin S}}c(u,v)
\end{align}$$

## Capacity Scaling

Ford-Fulkerson correctly solves the max flow problem, but is inefficient. Capacity scaling is a method of making it more efficient.

>[!algorithm]
>1. Initialize $f\gets0$ and an additional parameter $\Delta\gets F$
>2. Repeat until stuck
>	1. Write $G_f(\Delta)$, the residual graph that only includes edges if the $c_f(u,v)\ge\frac\Delta2$
>	2. BFS and push flow on $G_f(\Delta)$
>3. When stuck, if $\Delta < 1$, return. Otherwise, $\Delta\gets\frac\Delta2$, and return to (2).

### Analysis

>[!claim]
>Let $f:E\to\mathbb R_{\ge0}$ be the flow such that at stage $2\Delta$ and got stuck.
>
>Then, there exists an $(s,t)$-cut $S$ such that $c(S)\le|f|+m\Delta$.

It says that the moment you get stuck at stage $2\Delta$, the amount you need to increase before getting to the true max flow is at most $m\Delta$.

**Proof.**
$$\begin{align}
\max|f^*|-|f|&=\min_Sc(S)-|f| \\
&\le c(S)-|f| \\
&\le m\Delta\\
&\qed
\end{align}$$
This results in runtime $O(\lg F+m^2)$, which is polynomial time. 

$$\begin{align}
\Delta=C&\implies MF=nC \\
(\text{\# iterations})\cdot\frac\Delta2&\le|f| \\
&\le nC \\
\implies\text{\# iterations}&\le\frac{2nC}\Delta\\
&=2n
\end{align}$$

## Edmonds-Karp Algorithm

The Edmonds-Karp algorithm is yet another twist on the Ford-Fulkerson method that allows us to achieve a running time independent of the true max flow.

>[!algorithm]
>1. Initialize $f=0$
>2. If there exists an $(s,t)$-path in $G_f$, augment on the path to saturate the shortest $(s,t)$-path (in terms of the number of hops).

### Analysis

**Correctness:** Correctness, similar to the previous algorithms we discussed, follows from the max-flow/min-cut theorem.

**Running time:** Here is where things get more interesting. The key observation to make is the we are done when $s$ and $t$ are disconnected in $G_f$. Throughout the course of our algorithm's run, we track the number of hops of the shortest path $s\to t$. Specifically, we track
$$d(f)\triangleq\text{\# of hops on $(s,t)$ shortest path in $G_f$
}$$

>[!claim] Claim 1
>As the algorithm executes, $d(f)$ doesn't decrease.

>[!claim] Claim 2
>Every $O(m)$ iterations, $d(f)$ must increase at least one.

**Proof.** While $d(f)$ remains the same, we only push flow along "important" edges (i.e., edges from one level in the BFS tree to the next—we can't take back edges). Each iteration, we saturate at least one path on that level. There are $O(m)$ possible such paths, so after we exhaust all of them, $d(f)$ must increase at least once.

>[!claim 3]
>Claims 1 and 2 imply that the running time of the algorithm is $O(m^2n)$.

**Proof.** The maximum length of a path is $O(n)$. We know we get at least 1 closer to this maximum length every $O(m)$ iterations, and further we require $O(m+n)$ time to conduct a BFS for each iteration. This gives total running time $O(nm(m+n))=O(m^2n)$.
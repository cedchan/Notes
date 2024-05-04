## Computational Decision Problem

>[!definition]
>**Decision problems** can receive any input, but their outputs are either "accept" or "reject"—that is, they make a decision.

Oftentimes, decision problems are solvable iff their corresponding search problems (i.e., actually finding the accepting output) is solvable.

We can equivalently write problems in terms of formal languages $L\subseteq\{0,1\}^*$. 

>**Example.** Max-flow decision problem
>
>*Problem*: Given a graph $G=(V,E)$ and capacities $c$, decide whether the max flow is at least $T$.
>
>*Language:* The corresponding language is $$L_{\rm MF}=\{x\in\{0,1\}^*\mid x\text{ encodes $G,c,T$ such that the max flow of $G\ge T$}\}$$

We say that an algorithm $\sc{ALG}$ **decides** a language $L$ iff the following are satisfied:
1. $x\in L\implies\sc{ALG}(x)=\text{``accept"}$
2. $x\notin L\implies\sc{ALG}(x)=\text{``reject"}$

It decides in time $T(n)$ if $\sc{ALG}(x)$ always uses at most $T(|x|)$ steps. 

## Class P Languages

>[!definition]
>The polynomial class of languages is defined as follows:
$$\mathcal P=\{L\subseteq\{0,1\}^*\mid\exists c>0,\sc{ALG}\text{ s.t. $\sc{ALG}$ decides $L$ in time $T(n)\le n^c$}\}$$

## Class NP Languages

>[!definition]
>We define $\mathcal{NP}$ as
>$$\mathcal{NP}=\left\{L\,\middle|\, \exists c>0,\text{ verifier }V\text{ s.t. }\begin{array}{l}x\in L\iff \exists y \text{ s.t. } V(x,y)=\text{``accept"}\\
x\notin L\iff\exists y\text{ s.t. }V(x,y)=\text{``reject"}\end{array}\right\}$$

>**Example.** Longest simple path problem
>
>Given a graph $G=(V,E)$, output the longest simple path.
>
>Written as a decision problem language, we can say $$L=\{x\mid x\text{ encodes $G,k$ and the longest simple path of $G\ge k$}\}$$
>We want to find a polynomial-time verifier $V$. Define $V$ as follows:
>$V(x,y)$: Check if every edge in $y$ belongs to the graph, and check if the number of edges $\ge$ $k$. If so, output accept. Otherwise, reject.

### Cook-Levin Theorem

>[!theorem]
>The Circuit SAT question is NP-complete.

>[!problem]
>**Input:** A circuit $C$, which is a DAG consisting of logicals $\land,\lor,\lnot$.
>
>**Output:** $\exists$ some input such that the final output is true.

**Proof.** 

($\implies$) Circuit SAT is in NP

Since it's a DAG, the verifier can conduct a single graph traversal, calculating the values at each node based on previous values (which we never have to go back to). 

($\impliedby$) Circuit SAT is NP-hard

We know for any arbitrary $L\in\mathcal{NP}$ that there exists a verifier $V$ such that $V(x,y)$ can decide if $x$ is in $L$ using $y$.

We want to show that we can transform $V$ into a circuit. We do this by hardcoding $x$ into a circuit.

### 3-SAT

>[!problem]
>**Input:** Boolean formula in 3-CNF (the conjunction of clauses such that each clause is the disjunction of three literals/negations of literals).
>
>**Output:** Is it satisfiable?

>[!theorem]
>3-SAT is NP-complete.

**Proof.**

Clearly, just plugging in an assignment as the certificate of a value can yield a linear-time verification.

We reduce from Circuit SAT.

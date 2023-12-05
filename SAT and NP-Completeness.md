## Boolean Expressions

>[!definition]
>A **boolean formula** (or **propositional formula**) is an expression constrected from:
>- Boolean variables $x, y, z, \dots$
>- Logical connectives: And ($\land$), or ($\lor$), not ($\lnot$), implies ($\implies$)

### Semantics of Booleans

Truth assignment $\rho$: Assignment of 0/1 values to variables. $\rho(\varphi)$ is the value, either 0 or 1, of the formula $\varphi$ under the truth assignment $\rho$. 

Rules for evaluating logical connectives:
1. If $\rho(\varphi)=0$ then $\rho(\lnot\varphi)=1$ else $\rho(\lnot\varphi)=0$
2. If both $ρ(\varphi)$ = 1 and $ρ(ψ) = 1$ then $ρ( \varphi \land ψ ) = 1$ else $ρ(\varphi\land ψ ) = 0$ 
3. If either $ρ(\varphi) = 1$ or $ρ(ψ) = 1$ then $ρ( \varphi \lor ψ ) = 1$ else $ρ( \varphi \lor  ψ ) = 0$
4. If either $ρ(\varphi) = 0$ or $ρ(ψ) = 1$ then $ρ( \varphi \implies ψ ) = 1$ else $ρ( \varphi \implies ψ ) = 0$

$\varphi\implies\psi\equiv\lnot\varphi\lor\psi$

### Evaluation Problem

**Problem:** Given a formula $\varphi$ and a truth assignment $\rho$, find the value of $\varphi$ under this truth assignment.

This problem is in P. We can easily parse through the formula using boolean rules to get the result.

## SAT Problem

>[!definition]
>A formula is **satisfiable** if there exists a truth assignment $\rho$ such that $\rho(\varphi)=1$.

$${\rm SAT}=\{\langle\varphi\rangle\mid\varphi\text{ is a satisfiable boolean formula}\}$$

**Problem:** Determine if a boolean formula is in $\rm SAT$. 

Clearly, the SAT problem is in NP because we can use the evaluation problem as a verifier, taking in $\rho$ and some truth assignment as the certificate. We also note that the certificate is polynomial because there are a fixed number of variables to assign.

### Graph Coloring as SAT

**Goal:** Construct a boolean formula whose satisfying assignments encode assignments of 3 colors to vertices in a graph.

The variable $x_{ij}$ stands for vertex $i$ is assigned color $j$, where $i\in[1..n]$ and $j\in[1..3]$ (for 3 colors). 

We can restrict a single vertex $i$ to a color with the constraint
$$\varphi_i=(x_{i1}\land\lnot x_{i2}\land\lnot x_{i3})\lor(\lnot x_{i1}\land x_{i2}\land\lnot x_{i3})\lor(\land x_{i1}\land\lnot x_{i2}\land x_{i3})$$
which we combine into
$$\varphi=\bigwedge_{i}\varphi_i$$

We can then restrict edges $(i,j)$ between vertices (so their ends don't have the same color) with
$$\psi_{ij}=\lnot(x_{i1}\land x_{j1})\land\lnot(x_{i2}\land x_{j2})\land\lnot(x_{i3}\land x_{j3})$$
which we combine into
$$\psi=\bigwedge_{i<j}\psi_{ij}$$
**Claim:** A graph is 3-colorable iff $\varphi\land\psi$ is satisfiable.

This is an example of reducing a problem to SAT.

## NP-Completeness

>[!definition]
>A language/problem $A$ is called NP-complete if
>1. $A$ is in NP
>2. $A$ is NP-hard: for every language $B$ in NP, $B<_p A$ (every language in NP reduces to $A$)

(NP-hard can be thought of as a lower bound.)

>[!theorem] Cook's Thorem (1972)
>SAT is NP-complete—every problem in NP can be reduced to SAT. If SAT is in P, then P and NP are equivalent. 

### Independent Set

>[!definition]
>A set $U$ of vertices is an **independent set** if no two vertices in $U$ are connected by an edge.


**Problem:** Given a graph $G$ and a number $k$, does $G$ have a size $k$ independent set.

This problem is in NP: we can guess a size $k$ set and verify.

#### Reduction from Clique to Independent Set

We can reduce the clique problem to the independent set problem by toggling which pairs of vertices are connected and which aren't. That is, from $G=(V, E)$, we construct $G'=(V,E')$ where $E'=\{(i,j)\mid (i,j)\notin E\}$. 

## Invalidity
$${\rm INVALID}=\{\langle\varphi\rangle\mid\text{There exists a truth assignment $\rho$ such that $\rho(\varphi)=0$}\}$$
Observe that $\rm INVALID$ is in NP. Now we show that $\rm SAT<_pINVALID$ ($\rm SAT$ can be polynomially reduced to $\rm INVALID$.)

Given a boolean formula $\varphi$, we can check if our algorithm for $\rm SAT$ accepts $\lnot\varphi$. If yes, accept, otherwise reject.

## CoNP: The Complement of NP

Consider the problem$${\rm UNSAT}=\{\langle\varphi\rangle\mid\varphi \text{ is an unsatisfiable boolean formula}\}$$
To check that a formula is unsatisfiable, it doesn't suffice to find one truth assignment that makes it false. We need to show that each of the exponentially many possible assignments makes it false.

### Validity of Boolean Formulas

>[!definition]
>A formula $\varphi$ is called **valid** (or a **tautology**) if for every truth assignment $\rho$, $\rho(\varphi)=1$ (i.e., the formula is always true).

$${\rm VALID}=\{\langle\varphi\rangle\mid\varphi\text{ is a valid boolean formula}\}$$

$\rm VALID$ is in CoNP because its complement is in NP. (Its complement being that there exists an assignment that makes it true.)
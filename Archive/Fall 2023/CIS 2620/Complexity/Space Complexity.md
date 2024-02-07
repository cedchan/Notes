>[!definition]
>A TM $M$ has space complexity $f(n)$ if for every input $w$ of length $n$, $M$ uses at most $f(n)$ tape cells before deciding.

Again, this is an upper bound.

>[!theorem]
>If time complexity is $f(n)$, then the space complexity is $\leq f(n)$.

## The Class PSPACE

>[!definition]
>A language $A$ belongs to PSPACE if there exists a machine $M$ such that 
>1. $M$ solves $A$
>2. The space complexity of $M$ is $O(n^k)$ for some constant $k$

### Quantified Boolean Formulas (QBF)

>[!definition]
>**Quantified boolean formulas** are expressions constructed from
>- Boolean variables: $x, y, z$
>- Logical connectives: And, or, not
>- Variable quantifiers: Exists and for-all

>[!definition]
>A QBF formula $\varphi$ is **fully quantified** if it has no free variables.

$${\rm TQBF}=\{\varphi\mid\text{$\varphi$ is a fully quantified QBF and evaluates to true}\}$$

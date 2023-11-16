## Definition

Previously, we looked at the [class P](The%20Class%20P.md)—problems that could be solved by a standard TM. The class NP is similarly defined by the machines that can solve it, but here, an NTM is used.

The time complexity of an NTM $M$ is $f(n)$ if on every input $w$ of length $n$, every execution path terminates after at most $f(n)$ transitions. The depth of the execution tree is $f(n)$. Thus, the total number of possible execution paths is $2^{f(n)}$

>[!definition]
>Polynomial-time NTMs have time complexities of $f(n)=O(n^k)$ for some constant $k$. 

The definition of the class NP follows.

>[!definition]
>A language $A$ belongs to the **class NP** if there exists a nondeterministic TM $M$ such that
>1. $M$ decides $A$ (i.e., $L(M)=A$)
>2. Time complexity of $M$ is $O(n^k)$, for some constant $k$

### NP Algorithms

The typical structure for an NP algorithm is as follows:
1. Guess a solution (e.g., for the clique problem, guess a subset of vertices)
2. Check that guess is correct

There are two additional requirements on this structure:
1. The size of the guess must be polynomial with respect to the input length
2. The check must be conducted in polynomial time
## Verifier Based Definition

>[!definition]
>Consider a language $A$. Verifier $V$ for $A$ has, besides the original input $w$, an additional input $c$ (called the **certificate**) such that for all inputs $w$, $w\in A$ iff there exists $c$ such that $V$ accepts $\langle w, c\rangle$.

As an analogy to the original definition, $c$ is like the guess.

## Closure Properties

## Intersection and Union

The class NP is closed under intersection, and similarly union. The proof follows the one for the [[class P.md#Closure Properties of P#Closure Under Intersection#]].

## Complement

The class NP is not closed under complement.
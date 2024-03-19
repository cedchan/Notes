>[!definition]
>The **edit distance** is a measure of similarity between two strings defined as the minimum number of operations required to convert one string into another. Permissible operations include insertion, deletion, and substitution. 

>[!problem]
>**Input:** Two strings $A[1..n], B[1..m]$.
>
>**Output:** How many edits to go from $A$ to $B$.

## Alignments

Consider a grid with two rows—one each for $A$ and $B$. In each cell, there can be either a symbol of $A$ or $B$, or the blank symbol $\_$. 

A couple of principles follow:
- If some $A[i]$ is aligned with $\_$, we should insert $A[i]$ to $B$
- If some $B[i]$ is aligned with $\_$, we should insert $B[i]$ to $A$
- If some $A[i]$ is aligned with $B[j]\neq A[i]$, we should substitute

Thus, the number of edits per assignment it 
$$\sum_{i=1}^{n+m}\mathbb 1(\text{$i$-th column is unequal})$$
## Solution

- **Solution Space:** Set of alignments
- **Objective Function:** Cost for an alignment
- **Constraints:** Alignment of $A, B$

To find our subproblems, we ask a question: What is the first column? There are three options:

|  | 1 | 2 | 3 |
| ---- | ---- | ---- | ---- |
| $A$ | $A[1]$ | $\_$ | $A[1]$ |
| $B$ | $\_$ | $B[1]$ | $B[1]$ |
Then,
$$\begin{align}
G(i,j) &=\text{min-cost alignment between $A[i..n]$ and $B[j..m]$} \\
&=\min\{1+G(i+1,j),1+G(i,j+1),\mathbb1(A[i]\neq B[j])+G(i+1,j+1)\}
\end{align}$$

## Analysis

There are $O(nm)$ subproblems, each of which takes $O(1)$ time, resulting in total $O(nm)$ runtime.

---
tags:
  - divide-and-conquer
---
>[!definition]
>The **convex hull** of a set of points $A=\{(x_1, y_1), \dots, (x_n, y_n)\}$ is defined as
>$${\rm C{\small ONVEX}H{\small ULL}}(A)=\{z=(x, y)\in \mathbb R^2\mid z \text{ is an average of points in $A$} \}$$
>Where point $i$ gets weight $w_i\geq0$ and $\sum_{i=1}^nw_i=1$,
>$$z=\sum_{i=1}^nw_i(x_i, y_i)$$
>
>And equivalent definition is as follows: A segment connecting two points is in the boundary of the convex hull iff all points in $A$ lie on one side of the segment.

>[!problem]
>**Input:** Points in 2D plane: $(x_1, y_1), \dots, (x_n, y_n)$. Assume that all points are distinct and no points are colinear.
>
>**Output:** The convex hull, written is counter-clockwise order: $(a_1, b_1), \dots, (a_m, b_m)$.

## Baseline Algorithm

**Algorithm:** For each pair of points in $A$, draw the connecting segment and check if every other point lies on one of the two sides.

**Runtime:** $O(n^3)$

## Divide-and-Conquer Approach

>[!claim]
>Suppose we partition $A$ into $A_1\cup A_2$. Then $${\rm C{\small ONVEX}H{\small ULL}}(A)={\rm C{\small ONVEX}H{\small ULL}}(A_1)\cup{\rm C{\small ONVEX}H{\small ULL}}(A_2)$$

The merge algorithm uses two pointers to points along the convex hulls of the divided parts $C_1$ and $C_2$. Each pointer moves away from the middle line if doing so raises the point along the dividing line where the line connecting the two pointers intersects.

When both get stuck, that intersecting line is the new part of the convex hull.
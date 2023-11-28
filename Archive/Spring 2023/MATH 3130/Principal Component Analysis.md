
## Motivating Idea

In the simple two-dimensional case, linear regression minimizes the vertical distance between data points and a linear function. But what if instead of the vertical distance, we want to minimize the orthogonal distance? 

This is what we know as **principal components analysis**, or PCA. PCA is a dimensionality reduction technique that finds the orthogonal axis that maximizes the captured variance in the data (i.e., the orthogonal distances).

That is, we want to maximize $||A\vec w||$ for any $||\vec w||=1$. 

>[!theorem]
>For a data matrix $A$ the eigenvector of $A^TA$ with the largest eigenvalue points in the same direction as the line that minimizes the squared orthogonal distance to $A$. 

This is the first singular vector $\vec v_1$ of $A$. 

## Variance

>[!definition]
>- ${\rm average}(X)=\mu=\frac1n\sum x_i$
>- ${\rm variance}(X)=\frac1n\sum(x_i-\mu)^2$
>- ${\rm covariance}(X, Y)=\frac1n\sum(x_i-\mu_x)(y_i-\mu_y)$
>- ${\rm correlation}(X, Y)=\frac{{\rm covariance}(X, Y)}{\sqrt{{\rm variance}(X)}\sqrt{{\rm variance}(Y)}}$

For a matrix $A$, its **covariance matrix** is $A^TA$ (or $AA^T$, depending on the data is organized). The covariance matrix's rows and columns represent data points. Then, each cell represents the covariance of the point represented by its row and the one represented by its column. Note that this implies that the diagonal is just equal to variance. 

## PCA Calculation

Thus, we can perform PCA by finding the covariance matrix, then finding its eigenvectors and eigenvalues. Sorting the eigenvalues in order from greatest to least, the corresponding eigenvectors are the principal components, in order of most captured variance to least.

If $\lambda_1, \lambda_2, \dots, \lambda_n$ are the eigenvalues of $A^TA$, the principal component corresponding to $\lambda_i$ accounts for $\frac{\lambda_i}{\sum_{1\leq i\leq n}\lambda_i}$ of the variance.

## Applications

### Data Visualization
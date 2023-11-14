From [variance and bias](Variance%20and%20Bias.md), we saw the following:
$$\underbrace{\mathbb E_{x, y, \mathcal D}[(h_\mathcal{D}(x)-y)^2]}_{\text{Expected error of $\mathcal A$ on $\mathcal D$}}=\underbrace{\mathbb E_{x, y, \mathcal D}[(h_\mathcal{D}(x)-\overline h(x))^2]}_{\text{Variance → ``Overfitting"}}+\underbrace{\mathbb E[(\overline h(x)-\overline y(x))^2]}_{\text{Bias$^2$ → ``Underfitting"}}+\underbrace{\mathbb{E}[(\overline y(x)-y)^2]}_{\text{Noise (indep. of $\mathcal A$)}}$$
$\overline h$ is the optimal model of the form $\mathcal A$. $\overline y$ is the optimal model. (For example, if the true data is quadratic, $\overline y$ would be something like $x^2$, but if we're using a linear learning model, $\overline h$ would still be linear.)

Note that because noise is independent of the algorithm $\mathcal A$, no change in learning model choice will be able to decrease noise.

## Measuring Variance and Bias

[Recall](Supervised%20Learning.md#Solving%20Supervised%20Learning%20Problems#Generalization#Estimating%20the%20Generalization%20Gap) that datasets $\mathcal D$ are commonly split into training, validation, and test sets. The typical flow is
1. Train on training data
2. Measure performance on validation data
3. Repeat (1) and (2) with tweaks
4. Compute test error
5. Your test set is now validation

>[!idea]
 High **variance** (overfitting): $\text{Validation error} \gg \text{Training error}$
 >
 High **bias** (underfitting): $\text{Validation error} \approx \text{Training error}$ but both are high

![](IMG_6705.jpg)
![](Pasted%20image%2020231113144526.png)

## Combatting High Variance

1. Increase regularization
2. Get more data
3. Bagging (probably the most explicit expectation of $\overline h$)
4. Use a less powerful model
5. Early stopping (training on the validation error fewer times)
6. Feature selection

## Combatting High Bias

In general, combatting high bias constitutes doing the opposite of combatting high variance.

1. Decrease regularization
2. Use a more powerful model
3. Try a different assumption
4. Train more
5. More features
6. Boosting

## Combatting Noise

1. More features
2. Literally reduce noise


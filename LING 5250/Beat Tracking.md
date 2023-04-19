https://ieeexplore.ieee.org/abstract/document/1300607

https://ieeexplore.ieee.org/abstract/document/1495485

$$\begin{align}
\zeta(n)&=\sum_{k\geq 0}\Gamma_k(n) \\
S_k(n)&=X_k(n)e^{i\varphi_k(n)} \\
\Gamma_k(n)&=\left\{|\hat X_k(n)|^2+|X_k(n)|^2+\right. \\
&\qquad\left.-2|\hat X_k(n)||X_k(n)|\cos(\Delta\varphi_k(n))\right\}^\frac12 \\
\hat X_k(n)&=X_k(n-1)\\
\Delta\varphi_k(n)&=\varphi_k(n)-2\varphi_k(n-1)+\varphi_k(n-2)
\end{align}$$



Klapuri et al. Onsets
https://ieeexplore.ieee.org/abstract/document/757494

## Miguel Model

Agent-model
- Each agent is a hypothesis for a beat (called *tactus hypothesis*)
- Agents are given scores throughout the music (*congruency score*)
- High scores for a certain segment of the music indicate likelihood that the beat aligns there
- Generate predictions based on hypothesis. Called *projection* $p_k^{\rho, \sigma}$, with phase $\rho$ and period $\delta$ at time $k$.
$$
p_k^{\rho,\delta}=\rho+k\delta, k\in \mathbb Z^+
$$
- Scoring for a hypothesis $h=(\rho,\delta)$ at time $i$ is as follows, where $r_i$ is the real onsets:
$$
\begin{align}
\mathrm{congruency}(h,r_i)&=\frac{\text{\# hits}}{\text{\# predictions}}\cdot\frac{\text{\# hits}}{\text{\# events}} \\
\text{\# hits}&=\sum_k\mathrm{concurrence}(p_k^h,r_k) \\
\text{\# predictions}&=|p_k^h| \\
\text{\# events}&=|r_i| \\
\mathrm{concurrence}(p_k,r_k)&=0.01^{\frac{|p_k-r_k|}{\delta}}
\end{align}
$$

## Scoring

I use a slighly modified version of the Miguel model's scoring mechanism. In their implementation, the number of hits is calculated by calling the weight function on non-overlapping pairs of closest projected beats and onsets, iterating from left to right. 

For mine, I search for the closest onset to each projected beat, first irrespective of overlap. Then I resolve any shared closest pairs by choosing the closer projection. The losing projection then searches for neighboring onsets, so long as they don't "cross." Sequences are truncated if there aren't enough.

## Correction

Idea is that when projection and onset are simultaneous, $ce$ is 0. It then gets bigger as the distance increases, and goes back to 0 once the distance gets too far (to correct for too-far distances).
$$ce_k=m\cdot(r_k-p_k^h)\cdot d^\frac{|p_k^h-r_k|}{\delta}$$
We define
- $m$: The multiplier that determines how sensitive to error the correction  is
- $d$: The decay factor, for how far we must go before the error disappears.

Linear regression of $ce$ gives $\Delta h$, where $y$-intercept is phase and slope is period, since projections are linear functions. In this way, minimizes the error. 

Orig. uses $m= 2, d= 0.0001$.

>[!danger]
>With this implementation, I may have to go back to the original implementation of closest pairs, since the interceding pulse divisions will be ignored. But the score function should work to overcome, hopefully.


## Ideas
- Automatically resizing window

### Gaussian Weight

http://people.csail.mit.edu/hasinoff/320/sliding-notes.pdf

## Terminology

### Isochronous

A sequence is **isochronous** if it occurs at regular time intervals.
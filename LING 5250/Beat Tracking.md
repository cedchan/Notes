
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

### Gaussian Weight

http://people.csail.mit.edu/hasinoff/320/sliding-notes.pdf

## Terminology

### Isochronous

A sequence is **isochronous** if it occurs at regular time intervals.
https://ieeexplore.ieee.org/abstract/document/1300607

https://ieeexplore.ieee.org/abstract/document/1495485

$$

\zeta_t(n)=\delta+\lambda\cdot\mathrm{median\ }\zeta(k),k\in\left[n-\frac{H}{2},\frac H2\right] \qquad \delta,\lambda,H
$$\begin{align}
\zeta(n)&=\sum_{k\geq 0}\Gamma_k(n) \\
S_k(n)&=X_k(n)e^{i\varphi_k(n)} \\
\Gamma_k(n)&=\left\{|\hat X_k(n)|^2+|X_k(n)|^2+\right. \\
&\qquad\left.-2|\hat X_k(n)||X_k(n)|\cos(\Delta\varphi_k(n))\right\}^\frac12 \\
\hat X_k(n)&=X_k(n-1)\\
\Delta\varphi_k(n)&=\varphi_k(n)-2\varphi_k(n-1)+\varphi_k(n-2)
\end{align}

$$
S =\begin{bmatrix}
\ \rule[.5ex]{2.5ex}{0.5pt} \ S_1 \ \rule[.5ex]{2.5ex}{0.5pt} \ \\
\ \rule[.5ex]{2.5ex}{0.5pt} \ S_2 \ \rule[.5ex]{2.5ex}{0.5pt} \ \\
\ \rule[.5ex]{2.5ex}{0.5pt} \ S_3 \ \rule[.5ex]{2.5ex}{0.5pt} \ \\
\\
\ \rule[.5ex]{2.5ex}{0.5pt} \ S_f \ \rule[.5ex]{2.5ex}{0.5pt} \  \\
\rule[.5ex]{0.5pt}{2.5ex}
\end{bmatrix}
$$


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

$$\begin{align}
&\mathrm{score}=F_1=\frac{\rm precision\cdot recall}{\rm precision + recall} \\
&{\rm precision} = \frac{\rm\#\ hits}{\rm\#\ projected} \\
&{\rm recall}=\frac{\rm\#\ hits}{\rm\#\ onsets}\\
&{\rm\#\ hits}=\sum_k{\rm concurrence}(p_k^h,r_k) \\
&{\rm concurrence}=e^{-\frac{(p_k^h-r_k)^2}{2\delta^2}}
\end{align}$$


## Scoring

I use a slighly modified version of the Miguel model's scoring mechanism. In their implementation, the number of hits is calculated by calling the weight function on non-overlapping pairs of closest projected beats and onsets, iterating from left to right. 

For mine, I search for the closest onset to each projected beat, first irrespective of overlap. Then I resolve any shared closest pairs by choosing the closer projection. The losing projection then searches for neighboring onsets, so long as they don't "cross." Sequences are truncated if there aren't enough.

## Correction

Idea is that when projection and onset are simultaneous, $ce$ is 0. It then gets bigger as the distance increases, and goes back to 0 once the distance gets too far (to correct for too-far distances).
$$ce_k=m\cdot(r_k-p_k^h)\cdot d^\frac{|p_k^h-r_k|}{\delta}$$

$$
\epsilon_k=m\cdot(r_k-p_k^h)\cdot d^\frac{|p_k^h-r_k|}{\delta}
$$
We define
- $m$ The multiplier that determines how sensitive to error the correction  is
- $d$ The decay factor, for how far we must go before the error disappears.

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


This is a MATLAB implementation of a beat tracking algorithm that uses complex-domain onset detection[^1] and a multiple-agent beat model[^2]. Detailed information about the implementation, background, and appropriate citations may be found at [link TK].

---
## Using the Program

The end-to-end model can be used by created a `BeatTracker` object, which takes in the following parameters for the model:
- `window`: The size of the scoring/correction window in ms
- `mult`: The correction multiplier
- `decay`: The correction decay (must be $<1$)
- `delta`: The tolerance for how similar hypotheses can be before merging (see `Hypothesis.m` for details)

To track the beat of a signal, call `beats(x,fs)` on a `BeatTracker` object, where `x` is the input signal and `fs` is the sampling frequency. For example,
```matlab
tracker = BeatTracker(400,4,0.0001,0.5);
[x,fs] = audioread('sample.wav');
output = tracker.beats(x,fs);
```

Aside from the aforementioned parameters, the onset detection algorithm uses presets for the following values:
- `WIND_N = 128`: STFT window length
- `OVERLAP = 64`: STFT overlap length
- `MED_SHIFT = 0.05`: Median filter vertical shift
- `MED_SCALE = 1`: Median filter scaling factor
These can be manually tuned in the class definition.

## Classes

| Class Name | Function |
|-|-|
| `BeatTracker` | The central class that combines onset detection and beat modelling. |
| `OnsetDetector` | Takes in signal (`[x, fs]`) and finds onsets. An `OnsetDetector` object also stores the found detection function. |
| `BeatModel` | Models the underlying beat based on onset times and other other parameters. |
| `Hypothesis` | Stores a period, phase, and information about scores and corrections over time. |
| `Correction` | Evaluates a hypothesis over a given period and calculates the appropriate correction. |
| `Match` | Stores a pair of values (closest projection and onset times), and their difference. |
| `Util` | Additional methods, including `closestPairs()`. |

[^1]: Bello, J. P., Duxbury, C., Davies, M., & Sandler, M. (2004). On the use of phase and energy for musical onset detection in the complex domain. _IEEE Signal Processing Letters_, _11_(6), 553-556.
[^2]: Miguel, M. A., Sigman, M., & Fernandez Slezak, D. (2020). From beat tracking to beat expectation: Cognitive-based beat tracking for capturing pulse clarity through time. _PloS one_, _15_(11), e0242207.
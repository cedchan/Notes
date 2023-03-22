>[!summary]+

---

## Background

### Basic Sinusoids

At a high level, the DFT represents a periodic, infinite signal as a sum of sinusoids (in practice, it's a bit different).

The general formula for a sinusoid is
$$A\sin(2\pi f t+\phi)=A\sin(\omega t+\phi)$$
with
- $A$, amplitude
- $f$, frequency (oscillations per second)
- $\omega=2\pi f$, angular frequency, rate of change in radians/sec
- $\phi$, phase

We use the trigonometric identity $\sin(a+b)=a\cdot\cos(\phi)\cdot\sin(\omega t)+a\cdot\sin(\phi)\cdot\cos(\omega t)$ to derive the alternate formulation
$$A\sin(\omega t+\phi)=A\cos(\phi)\cdot\sin(\omega t)+A\sin(\phi)\cdot\cos(\omega t)$$
And conversely,
$$A_s\sin(\omega t)+A_c\cos(\omega t)=\sqrt{A_s^2+A_c^2}\cdot\sin\left(\omega t+\tan^{-1}\middle(\frac{B}{A}\middle)\right)$$
where $A_s, A_c$ are the sine and cosine weights, respectively. Thus, the sum of sinusoids of the same frequency is written as a single sinusoid with period $\sqrt{A_s^2+A_c^2}$ and phase $\tan^{-1}\left(\frac{B}{A}\right)$. We will revisit the importance of this later.

## Interpretation

When we apply the DFT to $x$, the resulting vector $X$ is called its **spectrum**.

### Phase and Amplitude

[TK]

In polar coordinates, this corresponds to
$$X(k)=|X(k)|e^{i\angle X(k)}$$

[TK]

The Fourier magnitude is given by
$$|F(k)=\left|\frac{N}{2}-k\right|$$

[TK]

MATLAB calculates this for us. The magnitude of each complex vector is given by `abs()`, while the angle is given by `angle()`. Thus, for our DFT vector `x`, we have

```matlab
amplitude = abs(x);
phase = angle(x);
```

Sometimes, it is useful to shift the samples so that the negative ones are first, which can be achieved with `fftshift()` (e.g., `fftshift(abs(x))`). 

### Graphical Representation

When a signal is graphed in the time domain, the $y$-axis is the amplitude, and the $x$ axis is time. Consider our signal with a sampling frequency $f_s$. 

>[!equation]
For samples $\mathbf{s}=[\text{start}..\text{end}]$ in the time-domain, our time vector is 
$$\mathbf{t}=s\frac{1}{f_s}$$

This is because $f_s=\frac{\text{samples}}{\text{sec}}$, so we divide to go from samples to seconds. Note that $\mathbf{s}$ should be adjusted for the particular range of samples in question.

In MATLAB, we have

```matlab
time = x(start:end)/Fs
```

When we apply the DFT, we move to the frequency domain, where the $x$-axis represents different frequencies, and the $y$-axis represents their magnitudes. The minimum frequency is obviously 0, while the maximum is just below $f_s$ at $(N-1)\frac{f_s}{N}$. In other words, each point along the frequency axis corresponds to a frequency increase of $\frac{f_s}{N}$, starting from 0. 

But for real signals, this will produce a symmetrical graph because half the results of the DFT are complex conjugates. Thus, we can instead take just the first half, up until $\left\lceil\frac{f_s}{2}\right\rceil$ (corresponding to the index $\frac{N}{2}$), which is known as the **Nyquist frequency**.

>[!equation]
>Let $N_2=\left\lceil\frac{N}{2}\right\rceil$. Consider $\mathbf{s}=[0..N_2-1]$. For a DFT-processed signal $\mathbf{X}$, the frequency vector is
>$$\mathbf{f}=f_N\frac{\mathbf{s}}{N_2}$$
>where $f_N$ is the Nyquist frequency $\left\lceil\frac{f_s}{2}\right\rceil$.

Obviously, this is half the original length of the signal.

In MATLAB, we have

```matlab
Nyquist = ceil(Fs/2);
N2 = ceil(nfft/2);
freq = Nyquist/N2*(0:(N2-1));
```
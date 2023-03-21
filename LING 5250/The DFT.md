>[!summary]

---

## Interpretation

### Phase and Amplitude


MATLAB calculates this for us. The magnitude of each complex vector is given by `abs()`, while the angle is given by `angle()`. Thus, for our DFT vector `x`, we have

```matlab
amplitude = abs(x);
phase = angle(x);
```

Sometimes, it is useful to shift the samples so that the negative ones are first, which can be achieved with `fftshift()` (e.g., `fftshift(abs(x))`). 

### A Graphical Representation

When a signal is graphed in the time domain, the $y$-axis is the amplitude, and the $x$ axis is time. Consider our signal with a sampling frequency $f_s$. 

>[!equation]
For samples $\mathbf{s}=[\text{start}..\text{end}]$ in the time domain, our time vector is 
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
N2 = ceil(N/2);
freq = Nyquist/N2*(0:(N2-1));
```
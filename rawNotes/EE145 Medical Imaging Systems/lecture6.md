# CUE
- why do not we care about the phase of light in medical imaging systems
- where does the convolution we study happens? in physics or in computer?
- Two ways of understanding sampling theorem
  - intuition: How many points do we need sampling in one period if we want to reconstruct an orbit
  - math: what is the sampling function looks like in time domain and frequency domain
- how to derive the function for getting decomposition of sinc function



## Quasi static assumption
because the distance in our system is far too large than wave length, we don't assume wave length

## compress sensing
sample sub nyquist, at information therotic nyquist

harder, need:
- sparsity (can be attained with sparsity transformation)
- sample randomly
- nonlinear reconstruction

# reversible reconstructions
$$
f(x) = \mathcal{F}\{F(k)rec(\frac{k}{2k_0})\} = f(x)\\
f_s(x) * 2k_0sinc(2k_0x) = f(x)
$$
thus 
$$
f(x) = \sum f(n\delta x)\frac1{\delta x}\operatorname{sinc}\left( \frac{x-n\delta x}{\delta x} \right)\delta x
$$

# SUMMARY DECOMPOSITION BASIS

1. boxcar
2. delta function
3. fourier
4. sampling

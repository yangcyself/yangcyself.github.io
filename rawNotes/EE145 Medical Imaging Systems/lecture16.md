# CUE
- what is the fourier transformation of the figure with rotation?
- what is the projection with an angle?
- what is the FT of that?
- when we add the pizza-samples together, how to model the effect of 'over sampling in the middle of the k-space'
- how to solve that problem
# recap

key things to remember

$$
F_{2D}\left\{f(\mathbb{R}(\theta)x )\right\} = F(\mathbb{R}(\theta)x k)
\text{ x and k are vectors}
$$

$$
P_{\theta}(L) = g_{\theta}(l) = \iint_\infty ^{\infty }  f(x,y)\delta (x\cos \theta + y\sin \theta - l)dxdy
$$

# FT for $R_{\theta}(l)$

$$

\begin{aligned}
    \mathcal{F}_{1D}\left \{g_{\theta} (l) \right\}  &= 
    \iiint f(x,y) \delta (x\cos \theta + y\sin \theta - l)dxdy e^{-2\pi i \rho l}dl\\
    & = \iint f(x,y)e^{-2\pi i \rho x\cos \theta + y\sin \theta} dl\\
    & = F(k_{x} , k _{y} )\delta (k_{x}\cos \theta + k _{y} \sin \theta = \rho  )\\
    & = F(\rho \cos \theta , \rho \sin \theta )
\end{aligned}
$$

the last step is get by letting $\rho \cos \theta = k_{x}$ and $\rho \sin \theta = k_{y}$

## nyquist of the sampling

$$
\rho _{max}\Delta \theta \leq \frac{1}{FOV}\\
\frac{\pi}{N}\rho _{max} \leq \frac{1}{FOV}
$$

How do we determine the $\rho_{max}$?

it is the maximum frequency you can image, decided by the FWHM of the PSF

> because x-ray is the mordality in CT, they should have the same PSF, thus CT's resolution  cannot be better than that of x-ray

# add the sampling together

if we add the samplings together, we are **over sampling in the middle of the k-space.** the DC value will be larger

How to model this?

we can regarded this as added another filter 
$$
\frac{\text{\# sample}}{\Delta p _{\theta } } = \frac{N}{2\pi \rho }
$$

thus the added k-space is like 
$$
\frac{N}{2\pi\rho  }F(k_{x} ,k_{y} )
$$

thus we have to change this back by adding a 
$$
\frac{2\pi\rho}{N} F(\rho \cos \theta , \rho \sin \theta )
$$

this is called "filter back projection"
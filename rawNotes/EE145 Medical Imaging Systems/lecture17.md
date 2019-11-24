# CUE
- derive the filter back projection algorithm
- what is the matlab function for this?

## rederive the F1D of the projection with rect function

$$
\iint \frac{1}{M_sW} \text{rect}\left( \frac{x\cos \theta +  y \sin \theta -l}{-M_s W} \right) \mu (x,y) dxdy = g_\theta (l)\\
 = g\theta (l) * rect??
$$
> this will appera in the next homework


this is a 2D rotated sincfunction, because the circululy symmetric PSF


## filter back projection algorithm

> this is a traditional algorithm, but is still used in nowaday CTs\
> this does not need to store too much data

from the folumar
$$
\mu (x,y) = \iint \hat{\mu} (k_{x} ,k_{y} ) e^{+ 2\pi i (xk_{x} + yk_{y} )}d{x} dy
$$

let $k_{x}  = \rho \cos \theta, k_{y}  = \rho \sin \theta$

$$
\iint \hat{\mu }(\rho \cos \theta , \rho \sin \theta )e^{+ 2\pi i \rho (x\cos \theta  + y\sin \theta  )}\rho \;d\rho d\theta 
$$

Note here the $\rho$ is the polor coordinate variable that goes $0\rightarrow \infty$, to change to pizza slice, we need it to be $-\infty , \infty$


unroll the $\mu$ 
we get
$$
\iiint_{-\infty}^{\infty}G_{\theta } (\rho )\delta (x\cos \theta + y \sin \theta -l) e^{2 \pi i \rho l} \rho \; d\rho  d\theta dl
$$
> I didnot understand this step

denote 
$$
\hat{g}_{\theta }(\rho )  =  \int_{-\infty}^{\infty}G_{\theta }(\rho )|\rho |  d\rho e^{+i2\pi \rho l}
$$
>
Note that this $\theta$ cna be $0,\pi$ and $\rho$ is $-\infty , \infty$
> this simply means that we get the fourier transformation($g_{\theta}$) and filter it with $|\rho |$ and inverse FT back


and back to last fomular we get 
$$
\mu (x,y) = \iint_{-\infty}^{\infty}\hat{g_{\theta }} (l) \delta (x \cos \theta + y \sin \theta -l)dl d\theta 
$$

> this means that each point(x,y) is the sum of the back projection of all different angls.

> this operation is called "radon" transform and invese rodan transform. The matlab function of this is `Radon`

> at the time it is invented, the inventer simply projected it back without $|\rho |$, so the DC signal is gained

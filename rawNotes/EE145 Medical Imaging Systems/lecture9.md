# CUE
- what is the fundamental of focusing electric wave
- what do we get in K space when we take a photo of X ray of the body?
- How many angels do we need to sample in the K space
- How bad is it if we use three times higher than the Nyquist law
- some vocabulary:
  - seizures: sudden, abnormal electrical activity in the brain.
  - Epilepsy: Epilepsy Also called: seizure disorder
  - eminently: to a notable degree; very.
  - mem·brane: 膜，
  - we model the (ionic, not electronic) charge on a nerve membrane inside the brain
that 

**what is the fundamental of focusing electric wave**

**the wave length:**

we can focus light, because we cann make significant phase difference

> we cannot see light(灯) flashing, because our neural perception is not that fast. Thus we cannot make lens for our neural impulse

## 2D fourier transform
$$
\mathcal{F}\left\{f(x,y) \right\} = \int_{-\infty}^{\infty}\int_{-\infty}^{\infty}f(x,y)e^{-2i\pi (xk_x+yk_y)}dxdy\\
f(x,y) = \int_{-\infty}^{\infty}\int_{-\infty}^{\infty}\mathcal{F}\left\{f(x,y) \right\}e^{2i\pi (xk_x+yk_y)}dxdy\\
$$
> NOTE, thsi fourier system has no scaling factor

## Projection-slice-theorem
suppose a wave through the body, and $\mu(x,y)$ is the attenuation coefficient.

$$
I = I_0e^{-\mu \Delta x}
$$

then the image
$$
\log \frac{i_x}{I_0} = -\int_{-\infty}^{\infty}\mu(x_i,y)dy
$$
we call this projection

the fourier function of this:

$$
\mathcal{F_{1D}}\left \{-\int_{-\infty}^{\infty}\mu(x_i,y)dy \right\} = 自己带进去推一下\\
= \mathcal{F_{2D}}\left \{\mu(x,y) \right\}|_{k_y=0}
$$

thus, when we make a projection photo (like x ray through the body), we are getting a line trough the K space.


## How many angels do we need to sample in the K space?
we have 
$$
\Delta k = \rho_{\max}\Delta\theta
$$
and 
$$
\rho_{\max}\Delta\theta\leq\frac{1}{\text{FOV}}
$$
where FOV is the field of view, and the $\rho_{\max}$ is the highest spatial frequency of our source.

**How bad is it if we use three times higher than the Nyquist law?**

Not that bad, because the alising only happends at high frequency part.



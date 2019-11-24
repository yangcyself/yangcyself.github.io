# CUE
- what are the conv relationships between Source Plane, Aperture plane and Image plane?
- what is the PSF for pin-hole camera and PSF for X-ray?
# math interpretation of X-ray

## Pin hole camera and x-ray

Three planes:

source plane <---> Aperture plane <---> Image plane

there distances:  $z$ and $d-z$

the relationship
$$
I(x,y) \propto S\left( \frac{x}{m_s},\frac{y}{m_s} \right) ** A\left(-\frac{x}{m_a},-\frac{y}{m_a}  \right)
$$

其中 $m$ 代表放大的作用

$$
m_s = \frac{d-z}{z}\\
m_a = \frac{d}{z}
$$

## Point spread functions

Note that in pin-hole camera, the *Source plane* is the *input image plane*

While For x-ray, the *aperture plane* is the input image plane

$$
I(x,y) \propto \underbrace{S\left( \frac{x}{m_s},\frac{y}{m_s} \right)}_\text{PSF for x-ray} ** \underbrace{A\left(-\frac{x}{m_a},-\frac{y}{m_a}  \right)}_\text{PSF for pin-hole camera}
$$



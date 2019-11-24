# MRI

核心思想:

encoding frequency to location, any resolution possible, trade off SNR and scan time

Note the half voxel(the square of particles,(resolution)) size requires 64 times scan time to get the same SNR

## polarization process

Put a large magnet field to polarize the particles.

If we put $1T$, we induce $4*10^{-9}T$ induced magnization


takes T1 to repolarize

T1 is tissue specific, 2ms to 2s

## precession 

> all photons have the exactly same $\gamma$

Put a gradient(in frequency) field.  The main field is DC magnetic field, does not generate magnet()


## Image acquisition

$$
s(t) \propto \iiint p(x,y,z) \exp(i2\pi k(t)x)d^{3} x
$$
where $k(t) = \gamma \int G(t)dt$

This $K$ is 2D spatial fourier transform.

## Physics background

### 1

$$
\mu _{0} M_{0} = \Chi _{n} B_{0}  = 3.8*10^{-9} B_{0} 
$$

$$
B = \underbrace{\mu _{0}}_{permeability} \left[ \underbrace{H}_{\text{magnetic field}}+\underbrace{M}_{\text{induced magnezation of the material}} \right]
$$

> the left side is in unit $T$ and the right side is in uint $A/M$

in linearized material

$$
= \mu _{0} (H+\Chi H) = \mu _{0} \mu _{R} H
$$

### 2

Prossesion

$$
\frac{d}{dt} e^{-i\gamma B_{0} t} \int p(x) e^{-ir(t)}  dt
$$

The left part is about 40M Hz and right part is about 40kHz.

So the derivitive can regard the integral as a constant.


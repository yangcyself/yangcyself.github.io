# CUE


**proving LTI**

when proving a system is LTI, it is equivalent to show that the inverse system is LTI

so to prove 
$$
\begin{array}{l}{\text { (a) } d f(x) / d x+b f(x)=u(x)} \\ {\text { (b) } d f(x) / d x=-b u(x) f(x)}\end{array}
$$

we don't need to solve the differential formulation

**quantization noise**

it is relatively simple to show that the **mean squared error** produced by such a rounding operation will be approximately $\Delta^{2} / 12$ （consider the uniform distribution）

**Properties for delta function**

All the properties of the delta function are deﬁned by integration

$$
\int_{-\infty}^{\infty} f(x) \delta(x) d x=f(0)
$$

## different modalities
- CT: 
  - The relative signal is $e^{-\mu x}$
- MRI：
  - Hydrogen generates the best NMR response of any nuclei 
- PET
  - detect coincident photons emitted by electron / positron annihilation events 
  - we can always make an extruded phantom in z to increase signal. 


**Gauss**
$$
\mathcal{F}\left\{\exp \left(-a x^{2}\right)\right\}=\sqrt{\frac{\pi}{a}} \exp \left(-\pi^{2} k^{2} / a\right)
$$


$$
\operatorname{Gaus}\left(\frac{x-x_{0}}{b}\right)=\exp \left[-\pi\left(\frac{x-x_{0}}{b}\right)^{2}\right]
$$

The area of Gaus is
$$
\int_{-\infty}^{\infty}\exp \left[-\pi a\left({x-x_{0}}\right)^{2}\right] = \sqrt{\frac{\pi}{a}}
$$

a very important trick dealing with gauss form

when we have form like 
$$
\int_{-\infty}^{\infty}exp(au^2+bux+cx^2) du
$$
we group according to $u$

and only integrate on $u$ form



**Sinc function**

$$
\text{sinc}(x) = \frac{\sin \pi x}{\pi x}\\
\lim_{x\rightarrow0} \text{sinc}x = 1
$$

rect(x) $\leftrightarrow$ sinc(k)

tri(x) $\leftrightarrow$ sinc^2(k)
> this is because tri(x) = rect(x) * rect(x)

做题的时候都是先写成求和的形式
$$
\begin{aligned} \mathcal{F}\left\{B_{n}\right\} &=\mathcal{F}\left\{\sum_{n} f[n \Delta x] \cdot \operatorname{Tr} \mathrm{i}\left(\frac{x-n \Delta x}{\Delta x}\right)\right\} \\ &=\sum_{n} f[n \Delta x] \cdot \mathcal{F}\left\{\operatorname{Tr}\left(\frac{x-n \Delta x}{\Delta x}\right)\right\} \end{aligned}
$$
然后n趋近无穷取极限

## HomeWork3
### Problem 1
$$
\text{COMB}(\frac{x}{\Delta x}) \rightarrow \Delta x \text{COMB}(k\Delta x)
$$

#### d
when signal is 
$$
F_s[k] = F(k) \cdot(\Delta x \operatorname{sinc}(k \Delta x)) * \operatorname{III}(k \Delta x)
$$
"we loose no information as long as we low pass filter with rect(k\Delta x)" and divide by  ...
$$
F(k)=\frac{F_{s}[k] \cdot \Pi(k \Delta x)}{\Delta x \operatorname{sinc}(k \Delta x)}
$$

### Problem 3
when calculating a bandwidth, define a arbitray limit $a$
$$
\frac{F\left(k_{b}\right)}{F\left(k_{p e a k}\right)}=a
$$

calculate the frequency limit band, and then apply the nyquist.

The assumed FWHM of $f(x)=e^{-\pi x^{2} / w^{2}}$ = $\frac{1}{w}$

**QUESTION:**

where does the overlap less than $\text{FWHM}/2$ comes from?

The Rayleigh criterion is the worst-case scenario in k-space: $\text{FWHM}/2$ overlapping in K-space






## HW4

### Problem 1

#### 1
QUESTION: why is my result `[ 1. -1.  1. -1.  1. -1.  1. -1.]`



N point DFT is $X = Wx$, $x$ is the input array length $n$
$$
W=\frac{1}{\sqrt{N}}\left(\begin{array}{cccc}{\omega^{0.0}} & {\omega^{0.1}} & {\dots} & {\omega^{0 . N}} \\ {\omega^{1.0}} & {\omega^{1.1}} & {\dots} & {\omega^{1 \cdot N}} \\ {\vdots} & {\vdots} & {\ddots} & {\vdots} \\ {\omega^{N \cdot 0}} & {\omega^{N \cdot 1}} & {\dots} & {\omega^{N \cdot N}}\end{array}\right)
$$  
$$
\omega=e^{-i 2 \pi / N}
$$

#### d
QUESTION????

> DFT remain some big problem

**Fourier transform of $\nabla^2$**


the fourier transform of $\nabla^{2} A(x, y)$ is 

$$
-4 \pi^{2}\left(k_{x}^{2}+k_{y}^{2}\right) \hat{A}\left(k_{x}, k_{y}\right)
$$

thus the equation

$$
\nabla^{2} A(x, y)=-\mu_{0} J(x, y)
$$

is equal to 

$$
-4 \pi^{2}\left(k_{x}^{2}+k_{y}^{2}\right) \hat{A}\left(k_{x}, k_{y}\right)=-\mu_{0} \hat{J}\left(k_{x}, k_{y}\right)
$$

**dealing with the high frequency noise**

$$
\hat{J}\left(k_{x}, k_{y}\right)=\frac{\hat{A}\left(k_{x}, k_{y}\right)}{\hat{H}\left(k_{x}, k_{y}\right)}
$$

we can add a low-pass filter

$$
J(x, y)=\mathcal{F}^{-1}\left\{\frac{\hat{A}\left(k_{x}, k_{y}\right)}{\hat{H}\left(k_{x}, k_{y}\right)} \Pi\left(\frac{\rho}{\rho_{\max }}\right)\right\}
$$

**REMEMBER THE RELATIONSHIP WITH PSF and TRANSFER FUNCTION**

这个题的思路:

我知道一个系统的PSF(x,y)

我还能从PDE里面求出来系统的H(kx,ky), 

我知道这两个相等，所以相当于我知道PSF中的某一部分的FT


## HW5
How is the Problem3 solved?

from 
$$
\mathcal{H}_{0}\left\{\frac{2 \pi}{\left(4 \pi^{2} r^{2}+1\right)}\right\} = e^{-\rho}
$$

to slove the hankel of 
$$
\frac{1}{8 \pi^{2} \epsilon_{0} z^{2}} \frac{2 \pi}{\left(4 \pi^{2}\left(\frac{r}{2 \pi z}\right)^{2}+1\right)^{\frac{3}{2}}}
$$



## Some suggestions from professor
>always label your axies

anti-alising filter


**KEEP in MIND**:

the integral of signal is k0 in k space, thus `measuring C0(total amount of signal) prior to injection will greatly improve 2D spatial resolution of c(x,y). Do you agree?`


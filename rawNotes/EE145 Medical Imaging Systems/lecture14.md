# CUE

# the source, aperture, detector model.

source <-> aperture <-> detector

$$
m_a = \frac{d}{z}\\
m_s = \frac{d-z}{z}
$$

consider for a $\Delta x$ in aperture plane

$$
I_d(x) = \sum_{p} \Delta x A(p\Delta x) \frac{1}{m_s} S(\frac{-x+p\Delta x m_a}{m_s})
$$

make this into integration
$$
p\Delta x \rightarrow u \quad \Delta x \rightarrow du
$$

$$
\int_{-\infty}^{\infty} a(u)\frac{1}{m_s}S\left( \frac{-x+um_a}{m_s} \right) du
$$

let $\psi = m_a u$

thus it becouse 
$$
\int_{-\infty}^{\infty} \frac{1}{m_a}A(\frac{\psi }{m_a})\frac{1}{m_s}S(\frac{-x+\psi}{m_s}) d\psi 
$$
which is 

$$
\frac{1}{m_a}A(\frac{x}{m_a})*\frac{1}{m_s}S(-\frac{x}{m_s})
$$

> We can also derive the same result from the opposite direction.

## how the x-ray interact with human tissue

3 Dominant constract mechanisms? 
$$
a(x) = e^{-\mu(x)}\Delta z
$$


> Ioning radiation has probability of causing cancer
### 1
**coherent scatter**
- $5-10\%$ of all interation
  - bones have 钙
  - other tisssues just like water
- No $e^{-}$ Ejected
  - ionizing radiation could cause cancer
  - no cancer risk
- Direction random
- The probability for this $\propto (E_{\text{eff}})^{\frac{8}{3}}/E^{2}$

**compton scattering**
- Ioning radiation
- scatter over all angle
- independent of $z$, $E$
- hurts constract
- Dominate $>80KeV$ 

**photo electronic effect**
- X ray absorbed
- k or L $e^-$ emmited "photo electron" 
- > here K and L are the 原子电子层的轨道
- M shell fills in lower energy (inversible)

$$
\text{prob}(p)\propto \frac{z^3}{E^3}
$$




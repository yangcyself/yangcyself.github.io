# CUE

# the FWHM of the signal and spacial impuse response

FWHM 约等于 FWHM + FWHM

# K space(Fourier) vs. x space

$$
F(k) = \int_{-\infty}^{\infty}f(x) e^{-2j\pi kx} dx
f(x) = \int_{-\infty}^{\infty}F(x)e^{2\pi kx} dk
$$

## Area theorem
$$
\int_{-\infty}^{\infty} f(u) du = F(0)\\
\int_{-\infty}^{\infty} F(u) du = f(0)
$$

## shift theorem

$$
\mathcal{F}\{f(x-\delta)\} = e^{-i2\pi ka}F(k)
$$

$$
\mathcal{F}\{f(\frac{x}{a})\} = |a|F(ka)
$$

## Convolution theorem

derivation
$$
\mathcal{F}\{f(x)*g(x)\}  =F(k)G(k)
$$

this is because
$$
\int_{-\infty}^{\infty}\left[ \int_{-\infty}^{\infty} f(u)g(x+u)du \right]e^{-2\pi kx}dx\\
= \int_{-\infty}^{\infty}f(u)\int_{-\infty}^{\infty}g(x+u)e^{-2\pi kx}dx du\\
= \int_{-\infty}^{\infty} f(u)\left[ G(k)e^{-2ipiku} \right] du
= G(k)F(k)
$$

## Useful function
Sinc(K)


Transform of Gaussian:

**Self transfering**




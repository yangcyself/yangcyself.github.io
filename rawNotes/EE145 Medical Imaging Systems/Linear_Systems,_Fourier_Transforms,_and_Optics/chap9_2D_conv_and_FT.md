
## convolution with delta functions
It is interesting to note that when a two-dimensional function f(x, y) is convolved with a delta function of the line-mass type discussed in Sec. 3-5, the result is effectively an integral of the profile of f(x, y) lying along the line mass. 

$$
\begin{array}{l}{f(x, y) * * \delta\left(x-x_{0}\right)=\int_{-\infty}^{\infty} f\left(x-x_{0}, \beta\right) d \beta} \\ {f(x, y) * * \delta\left(y-y_{0}\right)=\int_{-\infty}^{\infty} f\left(\alpha, y-y_{0}\right) d \alpha}\end{array}
$$

$$
\begin{aligned} f(x, y) * \delta\left(a_{1} x+b_{1} y+c_{1}\right) &=\frac{1}{\left|a_{1}\right|} \int_{-\infty}^{\infty} f\left(x+\frac{b_{1} \beta+c_{1}}{a_{1}}, y-\beta\right) d \beta \\ &=\frac{1}{\left|b_{1}\right|} \int_{-\infty}^{\infty} f\left(x-\alpha, y+\frac{a_{1} \alpha+c_{1}}{b_{1}}\right) d \alpha, \quad(9.17) \end{aligned}
$$

## 2D fourier transformation
$$
F(\xi, \eta)=\iint_{-\infty}^{\infty} f(\alpha, \beta) e^{-j 2 \pi(\alpha \xi+\beta \eta)} d \alpha d \beta
$$

$$
f(x, y)=\iint_{-\infty}^{\infty} F\left(\alpha^{\prime}, \beta^{\prime}\right) e^{j 2 \pi\left(\alpha^{\prime} x+\beta^{\prime} y\right)} d \alpha^{\prime} d \beta^{\prime}
$$

### when x and y are separable
$$
F(\xi, \eta)=\mathscr{F} \sigma\left\{f_{1}(x) f_{2}(y)\right\} = F_{1}(\xi) F_{2}(\eta)
$$
$$
g(x)=f(x, 0), \quad H(\xi)=F(\xi, 0)
$$

### transformation of convolution with delta
$$
f(x, y) * * \delta(x)=\int_{-\infty}^{\infty} f(x, \beta) d \beta \stackrel{\mathscr{S}}{\rightarrow} F(\xi, 0)
$$

$$
v(y)=f(x, y) * * \delta(y)=\int_{-\infty}^{\infty} f(\alpha, y) d \alpha \stackrel{\mathscr{F}}{\rightarrow} F(0, \eta)
$$

## THE HANKEL TRANSFORM 
> the Hankel transform is self-reciprocal because the kernels of the transform and inverse transform are identical. 
$$
\begin{array}{c}{G(\rho)=2 \pi \int_{0}^{\infty} g\left(r^{\prime}\right) J_{0}\left(2 \pi \rho r^{\prime}\right) r^{\prime} d r^{\prime}} \\ {g(r)=2 \pi \int_{0}^{\infty} G\left(\rho^{\prime}\right) J_{0}\left(2 \pi r \rho^{\prime}\right) \rho^{\prime} d \rho^{\prime}}\end{array}
$$
where 
$$
f(x, y)=g(\sqrt{x^{2}+y^{2}})
$$

this is because:

substitude the x,y,kx,ky with  r theta, rho, alpha. 
we get

$$
F(\rho \cos \phi, \rho \sin \phi)=\int_{0}^{\infty} \int_{0}^{2 \pi} g\left(r^{\prime}\right) e^{-j 2 \pi \rho r^{\prime} \cos \left(\theta^{\prime}-\phi\right)} r^{\prime} d r^{\prime} d \theta^{\prime}
$$

$$
\int_{0}^{2 \pi} e^{-j a \cos \left(\theta^{\prime}-\phi\right)} d \theta^{\prime}=2 \pi J_{0}(a)
$$


## Hankel transform of order $v$

$$
U(\rho ; \nu)=2 \pi \int_{0}^{\infty} u\left(r^{\prime}\right) J_{\nu}\left(2 \pi \rho r^{\prime}\right) r^{\prime} d r^{\prime}
$$

the nenotation

$$
\mathcal{H}_{\nu}\{u(r)\}=U(\rho ; \nu), \quad u(r)=\mathcal{H}_{\nu}\{U(\rho ; \nu)\}
$$

we have 

**The relationship between different orders**
$$
\begin{array}{l}{r^{k} f(r) \leftrightarrow\left(\frac{1}{2 \pi}\right)^{k} \frac{1}{\rho^{\nu+k}} \frac{d^{k}}{d \rho^{k}}\left[\rho^{\nu+k} F(\rho ; \nu+k)\right]} \\ {r^{k} f(r) \stackrel{\mathscr{X}_{\nu}}{\hookrightarrow}\left(\frac{-1}{2 \pi}\right)^{k} \rho^{\nu-k} \frac{d^{k}}{d \rho^{k}}\left[\frac{1}{\rho^{\nu-k}} F(\rho ; \nu-k)\right]}\end{array}
$$


$$
\begin{array}{l}{\frac{f(r)}{r} \stackrel{X_{v}}{\rightarrow} 2 \pi \rho^{-\nu} \int_{0}^{2 \pi \rho}\left(\rho^{\prime}\right)^{\nu} F\left(\rho^{\prime} ; \nu-1\right) d \rho^{\prime}} \\ {\frac{f(r)}{r} \leftrightarrow 2 \pi \rho^{\nu} \int_{2 \pi \rho}^{\infty}\left(\rho^{\prime}\right)^{-\nu} F\left(\rho^{\prime} ; \nu+1\right) d \rho^{\prime}}\end{array}
$$


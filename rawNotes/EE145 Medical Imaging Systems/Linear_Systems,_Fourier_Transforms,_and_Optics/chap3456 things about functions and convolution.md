# CUE
- what is the definition of sinc? 
- what are sinc and sinc^2 corresponding to?
- what is the relationship between the area of sinc and sinc^2
- what is the function of gauss?
- what is the so called Sombrero function?
- f(x) conv delta^(k)(x) = ?
- what is the definition of cross correlation, complex cross correlation and auto correlation?
- what the is the maximum point of auto_correlation?
# Typical functions

## sinc function and sinc^2 functions

**sinc**

$$
\operatorname{sinc}\left(\frac{x-x_{0}}{b}\right)=\frac{\sin \pi\left(\frac{x-x_{0}}{b}\right)}{\pi\left(\frac{x-x_{0}}{b}\right)}
$$

Note this way the width between the two zeros are $2b$, and the maximum is unit

sinc $\leftrightarrow$ rect

sinc^2 $\leftrightarrow$ triangle

**sinc^2**

**Note: the integral of the sinc function and the sinc^2 function are same**

### Gauss

$$
\operatorname{Gaus}\left(\frac{x-x_{0}}{b}\right)=\exp \left[-\pi\left(\frac{x-x_{0}}{b}\right)^{2}\right]
$$

## delta function
$$
\delta\left(\frac{x-x_{0}}{b}\right)=|b| \delta\left(x-x_{0}\right)
$$

NOTE $\delta^2(x-x_0)$ is not defined

**comb**

$$
\operatorname{comb}\left(\frac{x-x_{0}}{b}\right)=|b| \sum_{n=-\infty}^{\infty} \delta\left(x-x_{0}-n b\right)
$$


## 2D function
### Sombrero function

**It is the polar-coordinate counterpart of the two-dimentional sinc function**

$$
\operatorname{somb}\left(\frac{r}{d}\right)=\frac{2 J_{1}\left(\frac{\pi r}{d}\right)}{\left(\frac{\pi r}{d}\right)}
$$

where J_1 is the first-order *Bessel function* of the first kind. 

Both $somb$ and $somb^2$ has a volume of $4d^2\over\pi$


#### Bessel function
canoniical solution of the Bessel's differential equation

$$
x^2\frac{d^2y}{dx^2}+x\frac{dy}{dx} +(x^2+\alpha ^2) y = 0
$$

# Convolution

$$
f(x)*\delta^{(k)}(x) = f^{(k)}(x)
$$

其中上标意味着k阶导数

thus
$$
\begin{aligned} f^{(m)}(x) * h^{(n)}(x) &=\left[f(x) * \delta^{(m)}(x)\right] *\left[h(x) * \delta^{(n)}(x)\right] \\ &=f(x) * h(x) * \delta^{(m)}(x) * \delta^{(n)}(x) \\ &=g(x) * \delta^{(m+n)}(x) \\ &=g^{(m+n)}(x) \end{aligned}
$$

所以之后求导数和一个函数的卷积知道该怎么做了吧


## the convolution of sinc is sinc
$$
\operatorname{sinc}(x) * \operatorname{sinc}(x)=\operatorname{sinc}(x)
$$

if f(x) is band-limited, that is $F(K) = 0$ for $|K|>W/2$ and $W\leq|b|^{-1}$, then
$$
f(x) * \frac{1}{|b|} \operatorname{sinc}\left(\frac{x}{b}\right)=f(x)
$$

## scale of conv
$$
f\left(\frac{x}{b}\right) * h\left(\frac{x}{b}\right)=|b| g\left(\frac{x}{b}\right)
$$

## **Cross correlation and auto correlation**
Given the two complex-valued functionsf(x) and g(x), we define the cross correlation to be 
$$ 
f(x) \star g(x)=\int_{-\infty}^{\infty} f(\alpha) g(\alpha-x) d \alpha
 $$

**NOTE that this is similar to convolution but is not commute**
$$ f(x) \star g(x)=f(x) * g(-x) $$

### Complex cross correlation

$$ \begin{aligned} \gamma_{f g}(x) &=f(x) \star g^{*}(x) \\ &=\int_{-\infty}^{\infty} f(\alpha) g^{*}(\alpha-x) d \alpha \end{aligned} $$
$$ \gamma_{f g}(x)=f(x) * g^{*}(-x) $$

## autocorrelation
$$ \begin{aligned} \gamma_{f}(x) &=\left[a(x) e^{j \phi(x)}\right] \star\left[a(x) e^{-j \phi(x)}\right] \\ &=\int_{-\infty}^{\infty} a(\alpha) a(\alpha-x) \exp \{j[\phi(\alpha)-\phi(\alpha-x)]\} d \alpha \end{aligned} $$


With Schwarz's inequality we can see
$$ \left|\gamma_{f}(x)\right| \leqslant \gamma_{f}(0) $$


**correlation 的理解:**
想象这个函数是一个均值为0的时间序列,这样的话相当于是从两个时间点开始对比,得到的correlation. 一个函数让然是自己和自己的cov最大, 周期函数肯定也是隔一个周期然后cov达到最大值


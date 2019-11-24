# Machine learning ad medical imaging
an example:

用神经网络来处理MRI的信号，没有在MRI机器里面，照了一张空图片，结果得到一张心脏的图像

the problem is called *hallucination* in DSP jargon

# 2D fourier transform
> IMPORTANT, PUT TABLE 9-1 AND 9-2 IN THE CHEAT SHEET OF MID TERM

## some properties
$$
f(x) \leftrightarrow F_1(k_x)\delta(k_y)
$$
> **NOTE HERE the Ky's component is delta, not const 1**

$$
f(\frac{x}{a},\frac{y}{b}) = |ab|F(ak_x,bk_y)
$$

$$
(\frac{\partial ^2 }{\partial x^2 }+
\frac{\partial ^2 }{\partial y^2 })f(x,y) \longrightarrow
-4\pi ^2[k_x^2+k_y^2]F(k_x,k_y)
$$

a little question


$$
\frac{\partial ^n }{\partial x^n }+\dots+\frac{\partial ^1 }{\partial x }f(x) = g(x)
$$

which side is the input?

g(x) is the input and f(x) is the output, because we cannot get a resolution higher than the original image.

So every operation has to be a low-pass filter.

if g(x) is output, then g(x) is a high-pass filter, so it should be the other way around

$$
f(x,y)**h(x,y) \rightarrow F(k_x,k_y)H(k_x,k_y)
$$

# typical transformation pairs

$$
e^{\pm i\pi (x^2+y^2)} \rightarrow ie^{\mp i \pi (k_x^2+k_y^2)}
$$

> IMPORTANT! this is crutial for understanding how lens works

Hankel transform

for a function that symmetric in polor coordinate

$$
G(\rho) = 2\pi \int_{0}^{\infty} g(r)J_0(2\pi \rho r) r dr
$$

$$
g(r) = 2\pi \int_{0}^{\infty} G(\rho)J_0(2\pi r\rho)\rho d\rho
$$

To derive this, we can transform coordiante and get 
$$
\int_{0}^{2\pi}\int_{0}^{\infty}g(r)e^{-i2\pi r\rho[\cos (\theta - \phi)]} r dr d\theta
$$
Note the $\phi$ because that the interation only get one period, so the $\phi$ can be canceled and finally get the result.

So, watch out!
$$
\mathcal{F}\left\{f(\frac{r}{x}) \right\}\rightarrow x^2F(\rho x)
$$

# 2D sampling

$COMB(\frac{x}{\delta x}) COMB(\frac{y}{\delta y})$

...

at last:

$\delta x < \frac{1}{2k_{xmax}}$

$\delta y < \frac{1}{2k_{ymax}}$

> again, it is much easier to do sampling in the k space
假设使用库仑力成像一堆电子

$$
E(x)= \int_u\frac{1}{4\pi \epsilon }\frac{\epsilon(u)}{z^2+(x-u)^2}du
$$
this is a convolution

Q:
what is the FWHM of this system

A:2z

>小知识，硬盘的磁头和磁片之间的距离是2nm，就是因为这个公式决定

### Finite support
一个信号大于零的定义域，CS常用的概念，但是在这里不好用

## fourier theory
$$
f(x) = \int_{-\infty}^{\infty}F(k)e^{i2\pi kx}dk
$$

$$
\mathcal{F}\{f(x)\} = \int_{-\infty}^{\infty}f(x)e^{-i2\pi kx}dx    
$$
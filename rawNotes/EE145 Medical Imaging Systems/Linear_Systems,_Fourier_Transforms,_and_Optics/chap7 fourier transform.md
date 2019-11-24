# CUE
- Use integration to prove: $F^{-1}(F(f(x))) = f(x)$
- how to express delta(alpha-x) use integration form?
- Continuity and fourier transform
  - If f(x) is not impulsive, and if its mth derivative is the first to become impulsive, then, in general, how does F(K) behave in infinity?
- 以及为什么COMB 的傅里叶对是COMB
- Symmetry Properties of Fourier Transforms
- what is the symmetry property of The Fourier transformation of a hermitian function f?
- Transform of transform: F(F(f(x))) = f(?)
- Transform of Integral
- What is the fourier transformation of step function?
- Momentum theorem,
  - what does $\frac{F^{(k)}(0)}{(-j 2 \pi)^{k}}$ equal to ?
- Rayleigh theorem
  - what does $\int_{-\infty}^{\infty} f(\alpha) g^{*}(\alpha) d \alpha$ equals to when relating to fourier transformation
# Fourier transform

## inverse formula
我认为推一遍这个很有用

$$
\mathscr{F}^{-1}\{\mathscr{F}\{f(x)\}\}=f(x)
$$

to begin with:
$$
\mathscr{F}\{f(x)\}=\int_{-\infty}^{\infty} f(\alpha) e^{-j 2 \pi \xi \alpha} d \alpha
$$

Hence:
$$
\begin{aligned} \mathscr{F}^{-1}\{\mathscr{F}\{f(x)\}\} &=\int_{-\infty}^{\infty}\left[\int_{-\infty}^{\infty} f(\alpha) e^{-j 2 \pi \beta \alpha} d \alpha\right] e^{j 2 \pi \beta x} d \beta \\ &=\int_{-\infty}^{\infty} f(\alpha)\left[\int_{-\infty}^{\infty} e^{-j 2 \pi \beta(\alpha-x)} d \beta\right] d \alpha \end{aligned}
$$

by the orthogonality of the complex exponentials 

$$
\int_{-\infty}^{\infty} e^{-j 2 \pi \beta(\alpha-x)} d \beta=\delta(\alpha-x)
$$

we have 
$$
\begin{aligned} \mathscr{F}^{-1}\{\mathscr{F}\{f(x)\}\} &=\int_{-\infty}^{\infty} f(\alpha) \delta(\alpha-x) d \alpha \\ &=f(x) \end{aligned}
$$

### derive the orthogonallity of the complex exponentials

这个公式可以从$\delta(\alpha - x)$ 往傅里叶变换，然后再经过变换得到$e^{-2\pi i \beta \alpha}$, 然后再逆变换得到这个积分的式子 证明


### **Continuity and fourier transform**
The statement is:

If f(x) contains one or more impulses, $|F(\xi)|$ behaves as $|\xi|^0$ (i.e., a constant) for large $|\xi|$. 

 If f(x) is not impulsive, and if its mth derivative is the first to become impulsive, then, in general, $|F(\xi)|$behaves as $|\xi|^{-m}$ at infinity. 

### 以及为什么COMB 的傅里叶对是COMB

从$\delta(x-x_0)$的傅里叶公式$e^{-2\pi ix_0k}$出发, 第一个偏移了x0的脉冲的傅里叶变换（想象实部或者虚部）是一个波长为$\frac{1}{x_0}$的正余弦函数。然后再偏移了$2x_0$的是波长为$\frac{1}{2x_0}$的正余弦。这些东西一直叠加，用上前面一部分的$\int_{-\infty}^{\infty} e^{-j 2 \pi \beta(\alpha-x)} d \beta=\delta(\alpha-x)$
得证


## Symmetry Properties of Fourier Transforms
- complex, no symmetry    <->     Complex no symmetry
- Hermitian               <->     Real, no symmetry
- Antihermitian           <->     Imaginary, no symmetry
- Complex,even            <->     Complex, even
- Complex,odd             <->     Complex,odd
- Real, even              <->     Real,even
- Real, odd               <->     Imaginary, odd

the reverse is also true

List of properties:
- Linearity Property
- Central Ordinate 
  -  the area of a function is equal to the central ordinate of its Fourier transform 
- Scaling Property
- Shifting Property 
  - 记忆，想象delta
- Transform of Conjugate
  - 直接也conjugate
- Transform of transform
  - $\mathcal{F}\left \{\mathcal{F}\left \{f(x) \right\}  \right\}=f(-x)$
- Transform of Convolution
- Transform of product
- Transform of Derivative:
  - $f^{(k)}(x) \stackrel{\mathscr{F}}{\rightarrow}(j 2 \pi \xi)^{k} F(\xi)$
- Transform of Integral
  - $\int_{-\infty}^{x} f(\alpha) d \alpha \stackrel{\Im}{\rightarrow} \frac{1}{j 2 \pi \xi} F(\xi)+\frac{F(0)}{2} \delta(\xi)$
  - 需要死记硬背: $\operatorname{step}(x) \stackrel{\mathscr{F}}{\rightarrow} \frac{1}{j 2 \pi \xi}+\frac{1}{2} \delta(\xi)$

### Table of fourier transform pairs
书 201


## Other topics
### Moment Theorem
$$
\int_{-\infty}^{\infty} \alpha^{k} f(\alpha) d \alpha=\frac{F^{(k)}(0)}{(-j 2 \pi)^{k}}
$$

Thus the $F(0)$ is the area is just a special case of the Moment theorem

### Rayleigh theorem
$$
\begin{aligned} \int_{-\infty}^{\infty} f(\alpha) g^{*}(\alpha) d \alpha &=\int_{-\infty}^{\infty}\left[\int_{-\infty}^{\infty} F(\beta) e^{j 2 \pi \alpha \beta} d \beta\right]\left[\int_{-\infty}^{\infty} G\left(\beta^{\prime}\right) e^{j 2 \pi \alpha \beta^{\prime}} d \beta^{\prime}\right]^{*} d \alpha \\ &=\int_{-\infty}^{\infty} \int_{-\infty} F(\beta) G^{*}\left(\beta^{\prime}\right)\left[\int_{-\infty}^{\infty} e^{j 2 \pi\left(\beta-\beta^{\prime}\right) \alpha} d \alpha\right] d \beta d \beta^{\prime} \\ &=\int_{-\infty}^{\infty} \int_{-\infty} F(\beta) G^{*}\left(\beta^{\prime}\right) \delta\left(\beta-\beta^{\prime}\right) d \beta d \beta^{\prime} \\ &=\int_{-\infty}^{\infty} F(\beta) G^{*}(\beta) d \beta \end{aligned}
$$

note the second step uses:

$$
\int_{-\infty}^{\infty} G\left(\beta^{\prime}\right) e^{j 2 \pi \alpha \beta^{\prime}} d \beta^{\prime}
= 
\int_{-\infty}^{\infty} G^*\left(\beta^{\prime}\right) e^{-j 2 \pi \alpha \beta^{\prime}} d \beta^{\prime}
$$

this is referred to as power theorem.

$$
\int_{-\infty}^{\infty}|f(\alpha)|^{2} d \alpha=\int_{-\infty}^{\infty}|F(\beta)|^{2} d \beta
$$


When f(x) is periodic, its Fourier transform is given by an array of delta functions, 

$$
F(\xi)=\sum_{n=-\infty}^{\infty} c_{n} \delta\left(\xi-n \xi_{0}\right)
$$

thus,

$$
\int_{-\infty}^{\infty}|f(\alpha)|^{2} d \alpha=\sum_{n=-\infty}^{\infty}\left|c_{n}\right|^{2}
$$

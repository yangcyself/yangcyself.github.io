# CUE
## the rec function
我不知道latex怎么写，但是是一个“同”去了里面的口的样子
$$
n(\frac{x}{w}) \rightarrow |w| \operatorname{sinc}(wk)
$$

Sinc 这个函数的FWHM roughly $\frac{1}{w}$

# 一个问题
如果一个 **unfocused** system， 从输入图像直接把像传到输出图像上， 点到点的强度符合 exponential decay $e^{-\alpha r}$

FWHM 约等于 2z

## 如何解决
- lens
  - No length at x ray energy
- pin hole camera
  - 小孔成像
- "columnator"
  - 一堆垂直于图片方向的金属，会吸收斜向的电磁场还是光子啥的

# Reversibitity
**to recover a sin wave, we need two samples in one period**

Nyquist theorem

### COMB

$$
\operatorname{COMB}(x) = \Sigma\delta(x-n)
$$
就是周期脉冲

$\mathcal{F}\{COMB(x)\}=COMB(k)$


# CUE
- what are the three ways of definining jointly Gaussin
- How is the joint gaussian probabily density derived?
- THe shape of Isocontours of a joint guassian is a ellipsoid
  - What are the direction and length of its axis?
- what is the mean and var of the random varible $AZ$ where A is  a matrix and Z is a random variable

# Multivariate Gaussians
**jointly Gaussian Random Vector**
## definitions
1. $Z$ is JG(joint gaussian) when there exists a standard normal random vector $U$, a transition matrix $R$ and a mean vecotr $\mu$, such that $Z = RU+\mu$
2. $Z$ is JG if $\sum_{i=1}^{k}a_iZ-i$ is normally distributed for every $a = (a_1,2_3,...,a_k)^T\in \mathcal{k}$
3. A random vector Z is JG if $f_{\mathbf{Z}}(\mathbf{z})=\frac{1}{\sqrt{|\operatorname{det}(\mathbf{\Sigma})|}} \frac{1}{(\sqrt{2 \pi})^{k}} e^{-\frac{1}{2}(\mathbf{Z}-\boldsymbol{\mu})^{\top} \mathbf{\Sigma}^{-1}(\mathbf{Z}-\boldsymbol{\mu})}$
   - where $\Sigma = \mathcal{E}\left[ (Z-\mu)(Z-\mu)^T \right] = RR^T$

### Prove of (1) -> (3)
we can first show that 
$$
f_{\mathbf{U}}(\mathbf{u})=|\operatorname{det}(\mathbf{R})| f_{\mathbf{Z}}(\mathbf{R} \mathbf{u})
$$

Note that $Z = Ru$, thus如果$R$在拉伸u的面积的话，$f_Z$会很小，所以需要乘上一个$|\det R|$来放大回来。

thus 
$$
f_{\mathbf{Z}}(\mathbf{z})=f_{\mathbf{U}}\left(\mathbf{R}^{-1} \mathbf{z}\right)\left|\operatorname{det}\left(\mathbf{R}^{-1}\right)\right|=\frac{1}{|\operatorname{det}(\mathbf{R})|} f_{\mathbf{U}}\left(\mathbf{R}^{-1} \mathbf{z}\right)
\\
=\frac{1}{|\operatorname{det}(\mathbf{R})|} \frac{1}{(\sqrt{2 \pi})^{n}} e^{-\frac{1}{2}\left(\mathbf{R}^{-1} \mathbf{z}\right)^{\top}\left(\mathbf{R}^{-1} \mathbf{z}\right)}
\\
=\frac{1}{|\operatorname{det}(\mathbf{R})|} \frac{1}{(\sqrt{2 \pi})^{n}} e^{-\frac{1}{2} \mathbf{z}^{\top}\left(\mathbf{R} \mathbf{R}^{\top}\right)^{-1} \mathbf{z}}
$$

therefore
$$
f_{\mathbf{Z}}(\mathbf{z})=\frac{1}{\sqrt{\operatorname{det}\left(\mathbf{\Sigma}_{Z}\right)}} \frac{1}{(\sqrt{2 \pi})^{n}} e^{-\frac{1}{2} \mathbf{z}^{\top} \mathbf{\Sigma}_{Z}^{-1} \mathbf{z}}
$$

## Isocontours
find the level set $f(x) = k$ is equivalent to find $x^T\Sigma^{-1}x = c$

this is a ellipsoid with axis $v_1$, $v_2$ ... $v_d$ with length $\sqrt{\lambda_1}$,$\sqrt{\lambda_2}$ ... ,$\sqrt{\lambda_d}$


# The property of random variable multiply with a matrix
$$
\mathbf{A Z} \sim \mathcal{N}\left(\mathbf{A} \boldsymbol{\mu}_{\mathbf{Z}}, \mathbf{A} \boldsymbol{\Sigma}_{\mathbf{Z}} \mathbf{A}^{\top}\right)
$$

Proof:
$$
\begin{aligned} \boldsymbol{\Sigma}_{\mathrm{AZ}} &=\mathbb{E}\left[(\mathbf{A} \mathbf{Z}-\mathbb{E}[\mathbf{A} \mathbf{Z}])(\mathbf{A} \mathbf{Z}-\mathbb{E}[\mathbf{A} \mathbf{Z}])^{\top}\right] \\ &=\mathbb{E}\left[\mathbf{A}(\mathbf{Z}-\mathbb{E}[\mathbf{Z}])(\mathbf{Z}-\mathbb{E}[\mathbf{Z}])^{\top} \mathbf{A}^{\top}\right] \\ &=\mathbf{A} \mathbb{E}\left[(\mathbf{Z}-\mathbb{E}[\mathbf{Z}])(\mathbf{Z}-\mathbb{E}[\mathbf{Z}])^{\top}\right] \mathbf{A}^{\top} \\ &=\mathbf{A} \boldsymbol{\Sigma}_{\mathbf{Z}} \mathbf{A}^{\top} \end{aligned}
$$

注意这里是左乘$A$右乘$A^T$

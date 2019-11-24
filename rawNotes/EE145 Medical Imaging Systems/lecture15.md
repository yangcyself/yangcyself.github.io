# CUE
- what is the essense of MGF(moment generating function)
- how to compute the probability density of the sum of independ random variables
- derive the equation of rotation in x-space and the correcponding change in k-space
- write the expression projection at angle $\theta$ with distance $l$ to the center
# conv in statics

$$
\text{PROB}(x_{1}+x_{2}+\dots+x_{n} ) = P_{1}(x_{1})*P_{2}(x_{2})*\dots*P_{n}(x_{n})
$$

this is called **MGF**:

moment generating function(it is just the fourier tansformation of the prob density function)

# CT imaging equation

assume parallel bean of x-ray source

the FT of the fourier transformation

$$
\int_{-\infty}^{\infty}\int_{-\infty}^{\infty} u(x,\sigma )d\sigma  e^{-2\pi i k_xx} dx
=
\mathcal{F}\left \{u(x,y) \right\} |_{k_{y}} =0
$$


we need a general rotation theorem of 2D projection


> the noise property of $ln(\frac{I_0(x)}{I_0})$ is not that analysible

in general coordinate
$$
\left[\begin{array}c x' \\y' \end{array}\right] 
= 
\mathbb{R}(\theta ) \left[\begin{array}c x \\y  \end{array}\right] 
$$

the $\mathbb{R}$ is the rotation matrix

denote $\psi$ as the vector in new coordinate $\psi  = \mathbb{R}(\theta )x,x = \mathbb{R}^T(\theta )\psi$

thus 
($x,k$ are vectors)
$$
\mathcal{F}\left \{f(\mathbb{R}(\theta )x) \right\}(k) \\
= 
\iint f(\mathbb{R}(\theta )x) e^{-i2\pi k^Tx} dx
= 
\iint f(\psi )e^{-i2\pi k^T R^T(\theta) \psi }dx\\
=\mathcal{F}\left \{f(x) \right\}(\mathbb{R}(\theta )k) 
$$

> this means the rotation in x-space is the same as the rotation in k-space

### projection with angle $\theta$

$$
p_{\theta} (l) = \iint\mu (x,y)\delta (x \cos \theta + y \sin \theta -l) dx dy
$$

this is the projection at angle $\theta$ with distance $l$ to the center
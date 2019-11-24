# CUE
- explain regression in the way of MLE
- explain ridge regression in the point of view of MAP(Maximum a Posteriori)
- explain why ridge regression's variance is less than regression
  - what do variance in ridge regression standfor?
  - 使用decomposition求矩阵的逆
  - 证明加了ridge之后eigenvalue变大

the first two point is too trival and has been covered in SJTU ML courses.

# 我的发现！
### 推导variance
从minimiz的目标函数求导等于零得到:
$$
\hat{\mathbf{w}}_{\mathrm{RIDGE}}=\underset{\mathbf{w}}{\arg \min }\|\mathbf{y}-\mathbf{X} \mathbf{w}\|_{2}^{2}+\lambda\|\mathbf{w}\|_{2}^{2}
$$

$$
\theta  = (X^TX+\lambda I)^{-1}x^Ty
$$

Suppose y is gaussian ground the real data
$$
Y_{i} | \boldsymbol{\theta} \sim \mathcal{N}\left(h_{\boldsymbol{\theta}}\left(\mathbf{x}_{i}\right), \sigma^{2}\right)
$$

the variance of the learned $\theta_i$ would be:

$$
(((X^TX+\lambda I)^{-1}x^T)_iy)^2\\
= y^T X {(X^T+\lambda)^{-1}_i}^T {(X^T+\lambda)^{-1}}_i X^T y
$$

decompose the positive definitive matrix $(X^T+\lambda)^{-1}$ and get:

$$
y^T X U\Lambda_{X^{-1}}^2 U^T X^T y
$$

Thus, if the lambda $\Lambda_{X^{-1}}^2$, the eigen values of $(X^TX+\lambda I)^{-1}$ is smaller, then the variance will be smaller.

### 使用decomposition求矩阵的逆
Because of decomposition
$$
A = U^T \Lambda U
$$
we get 
$$
I = U^T \Lambda U U^T \Lambda^{-1} U
$$
Then that is how we get the inverse matrix

### 证明加了ridge之后eigenvalue变大
suppose $v$ and $\lambda_v$ are a pair of eigen vector and eigen value for X
$$
Xv = \lambda v\\
(X+aI)v = (\lambda+a)v
$$

thus...

Thus, ridge regression have larger eigenvalue, and its inverse have smaller eigenvalue, and smaller variance
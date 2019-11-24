# CUE

# summary
前面学的东西都是假设了每一个数据点的noise i.i.d的高斯， 同时假设了先验模型的参数也是i.i.d的高斯， 但是实际上并不应该如此
# Generalized Least Squares
the model is 
$$
\mathbf{Y}=\mathbf{X} \mathbf{w}+\mathbf{Z}
$$

where
$$
\mathbf{Z} \sim \mathcal{N}\left(\mathbf{0}, \mathbf{\Sigma}_{\mathbf{Z}}\right), \quad \mathbf{Y} \sim \mathcal{N}\left(\mathbf{X} \mathbf{w}, \mathbf{\Sigma}_{\mathbf{Z}}\right)
$$

the goal of regression is to:
$$
\hat{\mathbf{w}}_{\mathrm{GLS}}=\underset{\mathbf{w} \in \mathbb{R}^{d}}{\arg \max } \frac{1}{\sqrt{\operatorname{det}\left(\mathbf{\Sigma}_{\mathbf{Z}}\right)}} \frac{1}{(\sqrt{2 \pi})^{n}} e^{-\frac{1}{2}(\mathbf{y}-\mathbf{X} \mathbf{w})^{\top} \mathbf{\Sigma}_{\mathbf{Z}}^{-1}(\mathbf{y}-\mathbf{X} \mathbf{w})}
$$
which is equal to 
$$
\hat{\mathbf{w}}_{\mathrm{GLS}}=\underset{\mathbf{w} \in \mathbb{R}^{d}}{\arg \min }(\mathbf{y}-\mathbf{X} \mathbf{w})^{\top} \mathbf{\Sigma}_{\mathbf{Z}}^{-1}(\mathbf{y}-\mathbf{X} \mathbf{w})
$$

To minimize this, we can similarly try to find the derivative and solve
$$
\hat{\mathbf{w}}_{\mathrm{GLS}}=\left(\mathbf{X}^{\top} \mathbf{\Sigma}_{\mathbf{Z}}^{-1} \mathbf{X}\right)^{-1} \mathbf{X}^{\top} \mathbf{\Sigma}_{\mathbf{Z}}^{-1} \mathbf{y}
$$

## derive the ridge regression with dependent parameters

because:
$$
\begin{array}{l}{\mathbf{U}, \mathbf{V} \stackrel{\text { iid }}{\sim} \mathcal{N}(\mathbf{0}, \mathbf{I})} \\ {\left[\begin{array}{l}{\mathbf{Y}} \\ {\mathbf{W}}\end{array}\right]=\left[\begin{array}{ll}{\mathbf{R}_{\mathbf{Z}}} & {\mathbf{X} \mathbf{R}_{\mathbf{W}}} \\ {\mathbf{0}} & {\mathbf{R}_{\mathbf{W}}}\end{array}\right]\left[\begin{array}{l}{\mathbf{U}} \\ {\mathbf{V}}\end{array}\right]}\end{array}
$$
$Y = XW + \text{noise}$

we want to find posterior $W|Y = y$

its better if we write in this form
$$
\begin{array}{l}{\mathbf{U}^{\prime}, \mathbf{V}^{\prime} \stackrel{\text { iid }}{\sim} \mathcal{N}(\mathbf{0}, \mathbf{I})} \\ {\left[\begin{array}{l}{\mathbf{W}} \\ {\mathbf{Y}}\end{array}\right]=\left[\begin{array}{ll}{\mathbf{A}} & {\mathbf{B}} \\ {\mathbf{0}} & {\mathbf{D}}\end{array}\right]\left[\begin{array}{l}{\mathbf{U}^{\prime}} \\ {\mathbf{V}^{\prime}}\end{array}\right]}\end{array}
$$

thus 
$$
\begin{aligned} \mathbb{E}[\mathbf{W} | \mathbf{Y}=\mathbf{y}] &=\mathbb{E}\left[\mathbf{A} \mathbf{U}^{\prime}+\mathbf{B} \mathbf{V}^{\prime} | \mathbf{Y}=\mathbf{y}\right] \\ &=\mathbb{E}\left[\mathbf{A} \mathbf{U}^{\prime} | \mathbf{Y}=\mathbf{y}\right]+\mathbb{E}\left[\mathbf{B} \mathbf{D}^{-1} \mathbf{Y} | \mathbf{Y}=\mathbf{y}\right] \\ &=\mathbf{A} \underbrace{\mathbb{E}\left[\mathbf{U}^{\prime}\right]}_{\mathbf{0}}+\mathbb{E}\left[\mathbf{B D}^{-1} \mathbf{Y} | \mathbf{Y}=\mathbf{y}\right] \\ &=\mathbf{B} \mathbf{D}^{-1} \mathbf{y} \end{aligned}
$$

$$
\begin{aligned} \operatorname{Var}(\mathbf{W} | \mathbf{Y}=\mathbf{y}) &=\mathbb{E}\left[(\mathbf{W}-\mathbb{E}[\mathbf{W}])(\mathbf{W}-\mathbb{E}[\mathbf{W}])^{\top} | \mathbf{Y}=\mathbf{y}\right] \\ &=\mathbb{E}\left[\left(\mathbf{A} \mathbf{U}^{\prime}+\mathbf{B} \mathbf{D}^{-1} \mathbf{Y}-\mathbf{B} \mathbf{D}^{-1} \mathbf{Y}\right)\left(\mathbf{A} \mathbf{U}^{\prime}+\mathbf{B} \mathbf{D}^{-1} \mathbf{Y}-\mathbf{B} \mathbf{D}^{-1} \mathbf{Y}\right)^{\top} | \mathbf{Y}=\mathbf{y}\right] \\ &=\mathbb{E}\left[\left(\mathbf{A} \mathbf{U}^{\prime}\right)\left(\mathbf{A} \mathbf{U}^{\prime}\right)^{\top} | \mathbf{Y}=\mathbf{y}\right] \\ &=\mathbb{E}\left[\mathbf{A} \mathbf{U}^{\prime}\left(\mathbf{U}^{\prime}\right)^{\top} \mathbf{A}^{\top}\right] \\ &=\mathbb{A} \underbrace{\mathbb{E}\left[\mathbf{U}^{\prime}\left(\mathbf{U}^{\prime}\right)^{\top}\right]}_{=} \mathbf{A}^{\top} \\ &=\underset{=}{\mathbf{A}} \underbrace{\mathbb{E}\left[\mathbf{U}^{\prime}\left(\mathbf{U}^{\prime}\right)\right]}_{=\operatorname{Var}\left(\mathbf{U}^{\prime}\right)=\mathbf{I}} \mathbf{A}^{\top} 
\\ & = AA^T\end{aligned}
$$

这个note搞不下去了
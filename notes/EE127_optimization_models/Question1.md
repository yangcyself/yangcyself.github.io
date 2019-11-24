# CUE
- the axioms of the inner product
- Cauchy-Schwarz innequality
  - vector form
- How to calculate the gradient and hessian and jacobian
# Contents
## the inner product
the axioms of the inner product requires $f(x,x)\geq0$ and $f(x,x)=0$ if and only if $x = 0$

$$
\begin{array}{l}{\langle u+v, w\rangle=\langle u, w\rangle+\langle v, w\rangle} \\ {\langle\alpha v, w\rangle=\alpha\langle v, w\rangle} \\ {\langle v, w\rangle=\langle w, v\rangle} \\ {\langle v, v\rangle \geq 0 \text { and equal if and only if } v=0}\end{array}
$$
## Cauchy-Schwarz innequality
$$ |\langle\mathbf{u}, \mathbf{v}\rangle|^{2} \leq\langle\mathbf{u}, \mathbf{u}\rangle \cdot\langle\mathbf{v}, \mathbf{v}\rangle $$


## gradient and hessian and jacobian
我想通了, gradient, hessian 有两种方法

第一种是按照定义一步一步来：

gradient是列向量
$$
(\nabla g(x))_{i}=\frac{\partial g}{\partial x_{i}}(x), i=1, \ldots n
$$

$$
\left(\nabla^{2} g(x)\right)_{i j}=\frac{\partial^{2} g}{\partial x_{i} \partial x_{j}}(x), i=1, \ldots, n, j=1, \ldots, n
$$

第二种是通过雅克比矩阵

雅克比矩阵可以这样理解， 在一个列向量上面的小$\delta$如何经过这个函数反映到输出的维度上。 所以雅克比矩阵是$m*n$的, 行数m是输出的维度，列数n是输入的维度。 所以如果函数在嵌套，经过一个函数处理再经过下一个，那么矩阵也就由内到外左乘相应的雅克比矩阵。

**hessian就是gradient的雅克比**

所以比如$f(x) = y^TAx$

如果用定义来证明的话，可以
$$
\begin{align}
g(x) &= y^TAx\\
&= \sum_iy_i\sum_j A_{ij}x_j\\
&= \sum_j x_j \sum_i y_iA_{ij}\\
&= \sum_j x_j (A^Ty)_j\\
\end{align}
$$

但是如果雅克比的话, 可以通过 A视作一个函数的话，它的雅克比就是A， 同理y^T的雅克比也是y^T, 所以g的雅克比是 $y^TA$, 又因为gradient和单输入雅克比是行列相反的关系，所以是$A^Ty$

一个值得思考的例题

find jacobian of $g(x)=f(x) x$ where f : Rn →R is once-diﬀerentiable

定义方法:
$$
\begin{array}{c}{g(x)=f(x) x} \\ {(D g)_{i j}=\frac{\partial g_{i}}{\partial x_{j}}=\frac{\partial f(x) x_{i}}{\partial x_{j}}} \\ {=\left\{\begin{array}{c}{x_{i} \frac{\partial f(x)}{\partial x_{j}} j \neq i} \\ {x_{i} \frac{\partial f(x)}{\partial x_{i}}+f(x) \quad j=i}\end{array}\right.} \\ {D g=x D f(x)+f(x) I}\end{array}
$$

如果使用雅克比的操作有几点注意:
1. 所有乘法一定要是矩阵形式(m*n)，输入和输出的维度一定要对应上，
   - 在这里面$f(x)$和后面的常数乘法，一定要表示为$f(x)Ix$
2. 雅克比应对乘法和导数一样，也是分别求导然后再加照抄再相加。但是每一次的表示一定要写成函数操作的形式，比如 
   1. $D(f(x)Ix)$ 展开要写成$IxDf(x)+f(x)ID(x)$ D 代表雅克比
   2. 注意这里面有交换位置




**How to prove:**
$\mathcal{R}\left(A^{\top} A\right)=\mathcal{R}\left(A^{\top}\right)$
$$
\mathcal{R}\left(A^{\top}\right)=\mathcal{N}(A)^{\perp}=\mathcal{N}\left(A^{\top} A\right)^{\perp}=\mathcal{R}\left(\left(A^{\top} A\right)^{\top}\right)=\mathcal{R}\left(A^{\top} A\right)
$$


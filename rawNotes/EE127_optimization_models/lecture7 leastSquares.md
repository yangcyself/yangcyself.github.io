# CUE
- 如何计算least squares
- 如何计算 least norm solution
- 上面的解各自在矩阵A什么条件下解不唯一
- 化简constrained LS
# least squares
讲了和189一样的投影理解法

## 但是如果X full row rank
也就是样本的数量比feature的数量多

then $Ax = b$ 如何找到norm最小的那一个解

x should perpendicular to NULL space

$$
x^* \in \mathcal{N}(A)^\perp = \mathcal{R}(A^T) = A^T\theta
$$

thus 
$$
(AA^T)\theta = y
$$
thus 
$$
x^* = A^T (AA^T)^{-1}y
$$

# NOTE
least square 和 上面那个的解都不一定唯一，如果A不是行或满秩

# Other LS
## constrained LS
$$
\min \left\|Ax-b \right\|_2^2\\
s.t. Cx = y
$$

in this way we can transform it into unconstrained LS
$$
x = \tilde{x}+Nz\\
Ax-y = A\tilde{x}+ANz - y\\
$$
our objective function become
$$
\min_z (A\tilde{x}- y) + (AN)z
$$
## weighted LS


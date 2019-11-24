# CUE
- Vector calculus for the min squared error
  - yeild the definative form of w
  - Use Hessian to test convex
- Orthogonal projection for the min squared error
  - idempotent
  - prove for orthogonal projection |v − PSv| ≤ |v − s| for any s in S
- some matrix calculus
  - gradient of a^Tx
  - gradient of x^TAx
- why ridge regression, from numerical point of view
- Show the new optimizing problem is strong convex
- The insights
  - the meaning of product X^TX and X^TY
- different ways of derive (x^TX)^{-1}X^Ty
  - gradient = 0 & convex
  - orthogonal projection pov
  - solving with assume $\Delta w$
# summary

>Many contents can seen in the Note2

**design metrix**: the metrix formed by input sample, one row one sample


## some matrix calculus
$$
\begin{aligned} \nabla_{\mathbf{x}}\left(\mathbf{a}^{\top} \mathbf{x}\right) &=\mathbf{a} \\ \nabla_{\mathbf{x}}\left(\mathbf{x}^{\top} \mathbf{A} \mathbf{x}\right) &=\left(\mathbf{A}+\mathbf{A}^{\top}\right) \mathbf{x} \end{aligned}
$$

## orthogonal projection
The orthogonal projection onto S, denoted PS, is the linear operator that maps v to v_S in the decomposition of space

projection theorem:

$$
\|v - P_sv \| \leq \| v- u \|
$$

**idempotent**: $p^2 = p$

**idempotent**+**semmetric** -> althogonal projection matrix

### derive of the function with orthogonal projection
Our goal is $min \|Xw - y\|$

thus $Xw$ = $\argmin_u \|u-y\| \; u \in \mathtt{Range}(X)$

thus $y-u \in \mathtt{Range(X)}^{\perp}$ which means $y-u \in \mathtt{kernel}(X^T)$

(this is because the Range is the range of the X's column vectors, while the kerenel is $\{v | Xv = 0 \}$)

$x^T(y-u) = 0$

## Some insight in the lecture
### The meaning of Product

$X^TX$ is just how correlated are the features, like the correlation among features.

$X^TY$ is the correlation among feture to the label

thus $(X^TX)^{-1}X^TY$ The former part is how the features are correlated, if two features are correlated, then after inverse, they all get decreased importance. The $X^Ty$ part is how to get the feature.

### two point of view
the above are about the feature point of view

We can still see in the dual space, the data point of view.

when W is a vector in the projection space of $X$

$$
W^* = X^T . \alpha
$$

所以W就成为了所有样本的feature的一种组合， 回想一下SVM

## Another way of solving 
$$
w^* = argmin||Xw - y||^2
$$

equal to 
$$
||X(w^*+\Delta w) - y||^2 \geq ||Xw^* -y||^2
$$
where $\forall \Delta w$ following the definition of argmin.

equal to 
$$
||Xw^*- y + X\Delta w||^2 \geq ||Xw^* -y||^2
$$

By unrolling the L2 norm as inner product, the inequation equal to 
$$
2<Xw^* -y , X\Delta w> + ||X\Delta w ||^2 \geq 0 
$$

equal to 

$$
2<X'( Xw^* -y) , \Delta w> + ||X\Delta w ||^2 \geq 0 
$$

equal to 

$$
<X'( Xw^* -y ), \frac {\Delta w}{||\Delta w||}> + \frac{||X\Delta w ||^2}{||\Delta w||} \geq 0 
$$

equal to 
$$
X'(Xw^*-y) = 0
$$

The above step can be proved by contradiction. Suppose  $X'(Xw^*-y)\neq 0$, then we can take the $\Delta w$ be a vector on the direction of $- X'(Xw^*-y)$, and short enough so that  $\frac{||X\Delta w ||^2}{||\Delta w||}$ is smaller than $\|X'(Xw^*-y)\|$

the last step is get because $\Delta w$ can be any value, suppose it is the negative of the vector, and small enough, then it can always get less than 0.
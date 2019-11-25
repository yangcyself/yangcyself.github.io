# CUE
-  what is the first order condition for convex?
   -  How to prove
-  what is the second order condition?
   -  How to prove
   -  Prove p(x) = 4x_1^2 + 2x_2^2 3(x_1x_2)+4x_1+5x_2
-  restriction function to a line
   -  How to prove
   -  example: -log(det(X)) where X p.d symmetric 
-  Point-wise Max
   -  Prove 
   -  example: prove sum of kth largest elements
## some thing about mid term
> in mid-term you don't have to prove affine transfer convex sets is convex\
> most of the mid-term questions will be one-line-proof

# first order condition for convex function
$f$ is convex **iff**
$$
\forall x, y \in \operatorname{dom} f, f(y) \geq f(x)+\nabla f(x)^{\top}(y-x)
$$

the gradient divides the space into two subspace
$$
\begin{aligned} \mathcal{H}_{++}(x) &=\left\{y: \nabla f(x)^{\top}(y-x)>0\right\} \\ \mathcal{H}_{-}(x) &=\left\{y: \nabla f(x)^{\top}(y-x) \leq 0\right\} \end{aligned}
$$

and any point $y\in \mathcal{H}_{++}(x)$ is such that $f(y)>f(x)$

> 这个的意思是通过梯度的方向把整个空间切成了两个部分，所有比f(x)更大的在同一边

# Second-order condition

convex **iff** Hessian matrix positive semi-definite

## proof
$$
\Rightarrow
$$
$f$ is convex, let $z = x_0 + \lambda y$ 

$$
f(z) = f(x_0) + \lambda \nabla f^T(x_0)y + \frac{1}{2}\lambda^2y^THy+o(\lambda^3)
$$

thus

$$
\frac12y^THy  =\frac{1}{\lambda^2}\left[ f(z) - f(x_0) - \lambda\nabla f^T(x_0)y \right] 
$$
which is greater than 0



$$
\Leftarrow
$$

$$
f(y) = f(x) + \nabla f(x)^T(y-x)+ \frac{1}{2}(y-x)^TH(z)(y-x)
$$

Note that this is from 拉格朗日中值定理 (其实是泰勒中值定理)

Then this can be shown through first-order condition

## example

$$
p(x) = 4x_1^2 + 2x_2^2 +3(x_1x_2)+4x_1+5x_2
$$
compute $Hp$
$$
H_p = \left[\begin{array}c 8 & 3 \\3 &4 \end{array}\right]  
$$

to show $H_p \succ 0$

we show 
$$
\lambda_1 + \lambda_2 = 12\\
\lambda_1\lambda_2 = 23>0

$$

# Restriction function to a line
A function f is convex if and only if its restriction to any line is convex, where restriction to a line is 
$$
g(t)=f\left(x_{0}+t v\right)
$$
for a fixed $x_0$
> Note here the condition is to restrict to **any** line, that means for all different $x_0$ and $v$

## Proof

$$
\Rightarrow
$$

$$
\begin{aligned} g(\alpha t_1+(1-\alpha)t_2) &= f(x_0 + \alpha t_1v+(1-\alpha)t_2)\\ 
& = f(\alpha (x_0+t_1v)+(1-\alpha )(x_0+t_2v))\\
&\leq \alpha f(x_0+t_1v)+(1-\alpha )(x_0+t_2v)\\
&= g(\alpha t_1) + g((1-\alpha)t_2)
\end{aligned} 
$$

> 还能用二阶性质证明, 
> $$
> \frac{dg(t)}{dt} = \frac{df(x)}{dx} v
> $$
> $$
> \frac{d^2g(t)}{dt^2} = (Hv)^T v + 0 ...
> $$
(上面那个像不像lie derivative)

$$
\Leftarrow
$$
for any direction $y$

let $g(t) = f(x+t(y-x))$
$$
\begin{aligned} g(1-\alpha) &= f(x+(1-\alpha)(y-x))\\
 &=f(\alpha x_0+(1-\alpha )y)\\
 &=g(\alpha 0+(1-\alpha )1)\\
&\leq  \alpha g(0)+(1-\alpha )g(1)\\
&= \lambda f(x)+(1-\lambda )f(y)
 \end{aligned} 
$$

## Example:
Prove $f(X)$ is convex
$$
f(X)=-\log \operatorname{det} X \text{  where } X\in \mathbb{S}^{++}
$$

First show that $X\in \mathbb{S}^{++}$, $f(X)$ is defined

Then we use restriction to a line and compute $g(t) = -\log \operatorname{det}(X+tV)$

**Where V is an arbitrary matrix in $\mathbb{S}$** 
> 这一点是谬误陷阱，因为我一开始还在想V的定义域的事情

then 
$$
g(t)=-\log \operatorname{det}(X_0+tV)=  -\log \operatorname{det}(X_0^{\frac{1}{2}}x_0^{\frac{1}{2}}+tV)\\
 = -\log \operatorname{det}(\sqrt{X_0}\left[ I_0+tX_0^{-\frac{1}{2}}VX_0^{-\frac{1}{2}} \right]\sqrt{X_0})\\
 = -\log(\operatorname{det}X_0) - \log(\operatorname{det}(I+tZ))
$$
where $Z = X_0^{-\frac{1}{2}}VX_0^{-\frac{1}{2}}$

thus
$$
g(t) = -\log(\operatorname{det}X_0) - \log(\prod_{i=1}^n(1+t\lambda_i(Z)))
$$

each is a $\log(1+t\lambda_i(z))$ is a convex function


# Pointwise Maximum rule
> super helpful

If (fα)α∈A is a family of convex functions indexed by parameter α, and A is a set, then the pointwise max function $f(x)=\max _{\alpha \in \mathcal{A}} f_{\alpha}(x)$ convex over the domain: $\left\{\bigcap_{\alpha \in \mathcal{A}} \operatorname{dom} f_{\alpha}\right\} \cap\{x: f(x)<\infty\}$

## Proof

use the intersection of epigraph
## example

**$f(y,t) = \left\|y \right\|_2 -t$**

then it is 

$$
\max_{u:\left\|u \right\|_2 \leq1}u^Ty-t
$$
Thus convex

## example: sum of kth largest elements

$$
f(x)=\sum_{i=1}^{k} x_{[i]}
$$

where $x_{[i]}$ denotes the i-th largest element in x.

We have 
$$
f(x)=\max _{u} u^{\top} x: u \in\{0,1\}^{n}, \quad \mathbf{1}^{\top} u=k
$$

## example: largest eigen value of a symmetric matrix
$$
f(X)=\lambda_{\max }(X)
$$

$$
F(x)=\max _{u:\|u\|_{2}=1} u^{\top} X u
$$

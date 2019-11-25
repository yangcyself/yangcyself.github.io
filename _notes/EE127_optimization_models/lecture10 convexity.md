s# CUE
- what are the definitions of the hulls?
  - linear hull
  - convex hull
  - conic hull
- what is the definition of convexity
- Second order cone
  - what is a second order cone
  - How to represent as the intersection of hyper planes?
  - How to prove it is convex?
- How to represent the set of all PSD matrix as intersection of hyper planes?
- prove affine function $f$ on a Convex set $C$ is convex
- what are the two conditions for a function to be convex?
- f is convex iff epi(f) what?
- How to prove if $f$ is convex then sublevel set of f is convex set?
- How to prove the other way? if all sublevel set of f is convex then f is convex?
  - or find a counter example
- [\SS] Prove f(y) >= df(x)|x *(y-x) iff  f convex
# a lot of hulls 
## Linear hull
linear hull of a set of vector, let $P$ be a set of vectors in $R^n$
$$
P = \left\{x_1,...,M_m \right\}
$$
linear hull of these vectors are 
$$
x = \lambda_1x_1 + .... + \lambda_mx_m \quad \lambda_i\in \mathbb{R}
$$

## Convex hull
$$
\overline{CO}(\mathcal{P}) = \left\{x|x = \lambda_1x_1+\lambda_2x_2+\dots+\lambda_{m}x_{m} \right\}\\
\lambda_1+\lambda_2+\dots+\lambda_{m} = 1 \quad \lambda_i \geq 0
$$

## Conic hull
$$
\text{Conic}(x_1\dots x_n) = \left\{
    x = \lambda_{1}x_{1}+\lambda_{2}x_{2}+\dots+\lambda_{m}x_{m}\quad s.t. \lambda_i \geq 0
     \right\}
$$

# Convexity:
A set C is said to be convex iff
$$
\forall x_1,x_2\in C, \quad \lambda\in[0,1]
\\
\lambda x_1+(1-\lambda)x_2 \in C
$$

## Operations that preserve convexity:

if $C_{1},\dots,C_{m}$ are convex sets

then $\cap_i^m C_i$ is also convex set

### example: hyperplane
$$
\mathcal{H} = \left\{x_0 \in R^n| c^+x\leq d \right\}
$$
hyper plane is convex

the intersection of half planes is convex

### example: second ordered Cone 
second ordered cone in $R^{n+1}$

$$
K_n = \left\{(x,t)|x\in R^n, t\in R, \left\|x \right\|_2 \leq t \right\}
$$

#### **Prove this is convex**

$k_n$ is same as $\left\{(x,t)|x\in R^n, t\in R,\forall \left\|u \right\|_2 =1, x^Tu\leq t \right\}$

thus 
$$
k_n = \bigcap_{u:\left\|u \right\|_2\leq1 } \left\{(x,t) | x\in R^n, t\in R,u^Tx\leq t \right\}
$$

because the intersection of half planes is convex, thus..

### Example: Set of P.S.D matrices

$$
S_+^n = \bigcap_{u\in R^n}\left\{X \in S^n | u^TXu\geq 0 \right\}
$$
where $S^n$ is the set of all symmetric matrix.

this is also intersection of half planes.

## Other operations that preserves convexity
lets consider an affine function $f$
$$
f(x) = Ax+b
$$

thus for convex set $C$
$$
f(C) \hat{=} \left\{f(x)|x\in C \right\} \text{is convex}
$$

### Proof (direct proof)
> this is very standard proof, learn this!

Let $y_1$ and $y_2$ lie in $f(c)$, let we prove that $\lambda y_1 + (1-\lambda) y_2\in f(C), \forall \lambda\in [0,1]$

$$
\exist x_1,x_2 \quad s.t. \quad y_1 = Ax_1+b,\;y_2 = Ax_2+b
$$

$$
\lambda y_1+(1-\lambda )y_2 = A(\lambda x_1+(1-\lambda )x_2)+\lambda b+(1-\lambda )b
\\
= A(x_{\text{new}})+b
$$
where 
$$
x_{\text{new}} = \lambda x_1+(1-\lambda )x_2
$$
because of convexity of $C$, $x_{\text{new}}\in C$

thus $y_1 + (1-\lambda) y_2\in f(C)$


# Convex functions

## domain:
let $f$ be $\mathbb{R}^n\rightarrow \mathbb{R}$

then the domain of the function is 

$$
\text{dom}(f) = \left\{x\in R^n|-\infty < f(x) < \infty  \right\}
$$

## function convexity
A function $f$ is said to be convex iff
- $\text{dom}(f)$ is convex
- $\forall \lambda \in [0,1], \forall x,y \in \text{dom}(f)f(\lambda x+(1-\lambda )y)\leq \lambda f(x)+(1-\lambda )f(y)$

## Epigraph of convex function
**epigraph:**:
$$
\epsilon_{pi}(f) = \left\{(x,t)|x\in dom(f)\quad f(x)<t \right\}
$$

$f$ convex function $\Leftrightarrow$ $Epi(f)$ is a convex set

**Important!**

you can use both direction to prove things

## sublevel set of a function

let $f$ be a function

$$
S_\alpha  = \left\{x\in R^n|f(x)\leq \alpha  \right\}
$$
is called $\alpha$ sublevel sets

then **property:**

if $f$ is convex $\Rightarrow$ $S_\alpha$ is convex set

**proof**

direct prove..

**NOTE: THE OTHER WAY IS NOT TRUE**

counter example:

let $f(x) = \frac{x^2}{1+x^2}$

it is not convex but the alpha is always convex set

## Convexity and differential
$\forall (x,y) \in \text{dom}(f)$
$$
f(y) \geq f(x)+\nabla f(x)^T(y-x) \Leftrightarrow \text{f is convex}
$$

### proof:

**$\Leftarrow$**

$f$ is convex

let's compute $\frac{f(x+\lambda(y-x)) - f(x)}{\lambda}$ for $\lambda\in[0,1]$

$$
\frac{f(x+\lambda(y-x)) - f(x)}{\lambda} \leq  \frac{\lambda f(y)+(1-\lambda )f(x)-f(x)}{\lambda}\\
= f(y) -f(x)
$$

Note 
$$
\lim_{\lambda\rightarrow0} \frac{f(x+\lambda(y-x))-f(x)}{\lambda} = \nabla f^T(x)(y-x)
$$

therefore:
$$
f(y)\geq f(x)+\nabla f^T(x)(y-x)
$$

**$\Rightarrow$**

lets take $x,y\in \text{dom}(f),\lambda\in[0,1]$

$$
z = \lambda x+(1-\lambda )y
$$

we have 

1. $f(x) \geq f(z)+\nabla f^T(z)(x-z)$
2. $f(y) \geq f(z)+\nabla f^T(z)(y-z)$

$\lambda (1)+(1-\lambda )(2)$
we get 
$$
\lambda f(x)+(1-\lambda )f(y)\geq f(z)+\nabla f^T(z)(\lambda x+(1-\lambda )y-z) = f(z)
$$
thus 
$$
\lambda f(x)+(1-\lambda )f(y) \geq f(\lambda x+(1-\lambda )y)
$$
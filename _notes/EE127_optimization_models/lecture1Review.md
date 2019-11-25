# CUE
- Norm property(3)
- Affine sets
- Holder inequality
- Orthogonal decomposition theorem
- 
# review
## span
## addition of vector space
## basis
a collection of N independent vectors
## Norm
Norm property
- $||X|| \geq 0$ $||x|| = 0 only when x =0$
- $||x + y|| \leq ||x|| + ||y||$
- $\alpha ||x|| = ||\alpha x||$

## orthogonal and orthonormal


# introduction to optimization
## optimal set
The optimal set, or set of solutions, of problem (1) is defined as the set of feasible points for which the objective function achieves the optimal value:

But there are two cases that optimal set is empty:
- problem is infeasible
- optimal value can only be reached in the limit

## Sub-optimal
$$
p^{*} \leq f_{0}(x) \leq p^{*}+\epsilon
$$

numerical algorithms can only compute suboptimal solutions.

## Some special models
**convex**
- Least-Squares (LS)
- Linear Programs (LP)
- Convex Quadratic Programs (QP)
- Geometric programs (GP)
- Second-order cone programs (SOCP)
- Semi-definite programs (SDP).

**non convex**
Boolean/integer optimization

Cardinality-constrained problems

Non-linear programming

## vector and matrix basis
### Affine sets
$\mathcal{A}=\left\{x \in \mathcal{X} : x=v+x^{(0)}, v \in \mathcal{V}\right\}$

subspaces are just the affine space containing the origin

## H¨older inequality

$$
\left|x^{\top} y\right| \leq \sum_{k=1}^{n}\left|x_{k} y_{k}\right| \leq\|x\|_{p}\|y\|_{q}
$$

## Orthogonal decomposition 
X = S ⊕ S^⊥ for any subspace S ⊆ X .


The idea of projection is central in optimization, and it corresponds to the problem of finding a point on a given set that is closest (in norm) to a given point.

## Projection on a vector span

$$
\begin{aligned}\left(x-x^{*}\right) \perp \mathcal{S} & \Leftrightarrow\left\langle x-x^{*}, x^{(k)}\right\rangle= 0, k=1, \ldots, d : \\ & \sum_{i=1}^{d} \alpha_{i}\left\langle x^{(k)}, x^{(i)}\right\rangle=\left\langle x^{(k)}, x\right\rangle, \quad k=1, \ldots, d \end{aligned}
$$

however, if the set of vector is span of orthonormal vectors,
simply

$\alpha_{k}=\left\langle x^{(k)}, x\right\rangle, \quad i=1, \ldots, d$

## functions and maps
### epigraph
epi f
$\text { epi } f=\left\{(x, t) \in \mathbb{R}^{n+1} : x \in \mathbb{R}^{n}, \quad t \geq f(x)\right\}$



A function f is affine if and only if the function f˜(x) = f (x) − f (0) is linear (affine = linear + constant

A function f : R^n → R is affine if and only if it can be expressed as f (x) = ax + b, for some unique pair (a, b), with a in R^n and b ∈ R.

**gradients**

$$
\nabla f(x)=\left[\begin{array}{ccc}{\frac{\partial f(x)}{\partial x_{1}}} & {\cdots} & {\frac{\partial f(x)}{\partial x_{n}}}\end{array}\right]^{\top}
$$


**affine approximation of non-linear functions**

$$
f(x)=f\left(x_{0}\right)+\nabla f\left(x_{0}\right)^{\top}\left(x-x_{0}\right)+\epsilon(x)
$$

where the error term (x) goes to zero faster than first order



# CUE

# notions
halfspace

**polyhedron**

$$
a_{i}^{\top} x \leq b_{i}, \quad i=1, \ldots, m
$$

if the region is bounded, it is called **polytope**

## The LP model
Linear optimization problems admits several standard forms.
$$
\begin{array}{rl}{p^{*}=\min _{x}} & {c^{\top} x+d} \\ {} & {\text { s.t.: } \quad A_{\mathrm{eq}} x=b_{\mathrm{eq}}} \\ {} & {A x \leq b}\end{array}
$$

**optimal**

$$
x_{f} \in \mathcal{X} \text { is optimal for } \mathrm{LP} \Leftrightarrow c^{\top} x \geq c^{\top} x_{f}, \forall y \in \mathcal{X}
$$

the objective can be imporved if one can find 
$$
c^{\top}\left(x-x_{f}\right)<0
$$

## polyhedral function

if the epigraph is polyhedron

Polyhedral functions include in particular functions that can be expressed as a maximum of a finite number of affine functions:

$$
f(x)=\max _{i=1, \ldots, m} a_{i}^{\top} x+b_{i}
$$

Then the epigraph can be expressed as the polyhedron
$$
\operatorname{epi} f=\left\{(x, t) \in \mathbb{R}^{n+1}: \max _{i=1, \ldots, m} a_{i}^{\top} x+b_{i} \leq t\right\}\\
\text { epi } f=\left\{(x, t) \in \mathbb{R}^{n+1}: a_{i}^{\top} x+b_{i} \leq t, i=1, \ldots, m\right\}
$$

Can also be expressed as sum of max
$$
f(x)=\sum_{j=1}^{q} \max _{i=1, \ldots, m} a_{i j} x_j+b_{i j}
$$

The condition $(x, t) \in \text { epi } f$ is equivalent to 
> like slack variable
$$
\exist u \in R^q \quad\sum_{j=1}^{q} u_{j} \leq t, \quad a_{i j}^{\top} x+b_{i j} \leq u_{j}, i=1, \ldots, m ; j=1, \ldots, q
$$

## Exmaple:
$\left\|x \right\|_\infty$ is polyhedral since it can be written as the maximum of 2n affine functions:
$$
f(x)=\max _{i=1, \ldots, n} \max \left(x_{i},-x_{i}\right)
$$

The l1-norm function $f = \left\|x \right\|_1$, is polyhedral since it can be written as
the sum of maxima of affine functions:

$$
f(x)=\sum_{i=1, \ldots, n} \max \left(x_{i},-x_{i}\right)
$$

The problem of minimizing a polyhedral function, under linear equality or inequality constraints, can be cast as an LP

$$
\min _{x} f(x) \quad \text { s.t.: } A x \leq b
$$

$$
\min _{x, t} t \quad \text { s.t.: } A x \leq b, \quad(x, t) \in \text { epi } f
$$

# Examples:
skipped

# conic optimization
$f: C \rightarrow \mathbb{R}$ $C$ defined on a convex cone, and an affine subspace $\mathcal{H}$

## linear programming
$$
\begin{array}{ll}{\min _{x \in \mathbb{R}^{n}}} & {c^{\top} x} \\ {\text { s.t.: }} & {A x \leq b, \quad C x=d}\end{array}
$$


## Quadratic programming
$$
\begin{array}{cl}{\text { minimize }} & {x^{\top} Q x+c^{\top} x} \\ {\text { subject to: }} & {A x \leq b, \quad C x=d}\end{array}
$$

When $Q\succ 0$ (positive-definite), $QP$ is a regularized version of $LP$, 

## Quadratically constrained quadratic programming
$$
\begin{array}{ll}{\min _{x}} & {x^{\top} Q_{0} x+a_{0}^{\top} x} \\ {\text { s.t.: }} & {x^{\top} Q_{i} x+a_{i}^{\top} x \leq b_{i}, \quad i=1, \ldots, m}\end{array}
$$

## second order cone optimazation
$$
\begin{array}{ll}{\min _{x \in \mathbb{R}^{n}}} & {c^{\top} x} \\ {\text { s.t. }} & {\left\|A_{i} x+b_{i}\right\|_{2} \leq c_{i}^{\top} x+d_{i}, \quad i=1, \ldots, m}\end{array}
$$

## Robust optimzation
$$
\begin{array}{cl}{\min _{x}} & {\max _{u \in \mathcal{U}} f_{0}(x, u)} \\ {\text { s.t. }} & {\forall u \in \mathcal{U}, \quad f_{i}(x, u) \leq 0} \\ {} & {i=1, \ldots, m}\end{array}
$$

## semidefinite programming
It includes SOCP as a special case.

**Convex optimization is beyond the Conic optimization**


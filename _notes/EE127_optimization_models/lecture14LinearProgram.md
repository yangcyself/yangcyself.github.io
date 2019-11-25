# CUE
- what is the standard form of linear programming?
- What is the definition of a polyhedral function
- what are the other forms of polyhedral functions?
  - how are they corresponded to L1 and Linf
- How to cast Polyhedral (epigraphical form) functions to LP
- Cast the Linf and L1 regression problem into LP
- Use the LP to solve network flow problem
- What is the form of a quadratic program?
- What are the three cases to determine the solution and the bound of a QP (suppose no constraints)

**Road map**
a few classes of programs

- recognize
- transform

## a quick mid-term clarification

convex program/problem

we will accept

$$
min_x f_0(x) \\
s.t. f_i(x)\leq 0
$$

$$
min_x f_0(x) \\
s.t. \quad x\in C
$$

you will not get credit if you leave some inactive unconvex constraints

note that if you have $(x-1)^2=0$ you cannot only put it here, because this constraint is not CONVEX you have to say $x = 1$

# linear programs


## example

$$x\in \mathbb{R}^3 \quad a_{1}x_{1}+a_{2}x_{2}+a_{3}x_{3}\leq v$$

**graph1**
> x1 x2 x3 坐标轴上面点三个点, 分别是 $\frac{v}{a_1},\frac{v}{a_2}，\frac{v}{a_3}$连成一个三角形

you get a **polyhedron**

> Note this is not necessaryly bounded
> this could be empty

### example probolibity simplex

$$
P = \left\{x \in R^n | x\geq 0 \quad \sum_{i = 1}^nx_i = 1 \right\}
$$

## example 

$$
l_1 \text{  ball}:  
B_{l1}(0,1) = \left\{x | x\in \mathbb{R}^n : \left\|x \right\|_1 \leq 1 \right\}
$$
recall that
$$
\left\|x \right\|_1  = \sum_{i=1}^{n}|x_i| = \sum_{i=1}^{n} \max_{s_i\in \left\{-1,1 \right\}} s_i x_i = \max_{s_i\in \left\{-1,1 \right\}} \sum_{i=1}^{n}  s_i x_i
$$

thus 

$$
B_{l1}(0,1) = \left\{x | x\in \mathbb{R}^n : \sum_{i=1}^{n} s_i x_i   \leq 1
\quad s_i \in [1,-1]
\right\}
$$

thus this is polyhedron and convex



## Linear Program
$$
P^* = \min_{x} c^Tx +d \\
s,t. \quad A_{\text{eq}}x = v_{\text{eq}}\\
Ax \leq v
$$

when you show sth is linear program, you show this form
> professor once solved for 60,000,000 dimension x 15 years ago because linear program

**Geometric interpretation of L.P.**

$\left\{x | Ax \leq v \right\}$ feasible set of the LP

bring the gradient

**graph2**
A polyhedron which is a feasible set, and draw a line representing the objective function, the direction of $c$ is just the direction of the gradient, and the minimum is got at vertex or edge

The geometric answer to Lp is always end up to sth at the vertex or the face

## example

$$
\min_{x\in R^2} 3 x_1 +  1.5x_2\\
s.t. -1\leq x_1 \leq 2\\
0 \leq x_2 \leq 3
$$


the constraint can be rewrite as 
$$
\left[\begin{array}c 1 & 0 \\ -1 & 0 \\ 0 & 1\\ 0 & -1 \end
{array}\right] x \leq 

\left[\begin{array}c 2\\-1\\3\\0 \end{array}\right] 
$$

## Polyhedral functions
we say $f$ is polyhedral if it epigraph is polyhedron
$$
\text{epi}(f) = \left\{(x,t)\in R^{n+1} | C \left[\begin{array}c x \\t \end{array}\right] \leq d\right\}
$$

Polyhedral functions include in particular functions that can be expressed as a **maximum of a finite number of affine** functions
$$
f(x) = \max_{i=1}^m(a_i^Tx + v_i)
$$

$$
\text{epi}(f) = \left\{ (x,t) | \max_{i=1}^m a_i^T v_i \leq t \right\}
$$

Or polyhedral functions can also be expressed as **sum of maxima** of affine functions.
$$
f(x)=\sum_{j=1}^{q} \max _{i=1, \ldots, m} a_{i j}^{\top} x+b_{i j}
$$

### other example:
inf norm

$$
f(x) = \left\|x \right\|_\infty = \max_{i=1}^n \max \left\{x_i,-x_i \right\}
$$
so this is maximum of $2n$ affine functions
, convex and polyhedral

> when we ask you wherther this is polyhrdornal in test just two lines

example 1

so to prove that L1 is convex

you show $\left\|x \right\|_1  = \sum_{i=1}^{n} \max \left\{x_i,-x_i \right\}$

sum of maxima affine functions 

Polyhedral (epigraphical form) functions can be casted as LP

$$
\left\{\begin{aligned} 
\min_x f(x) \\
s.t. Ax \leq v
 \end{aligned}\right. 

 \qquad

 \left\{\begin{aligned} 
 \min_{x,t} t \\
 s.t. Ax \leq l \\
 (x,t)\in epi(t)
  \end{aligned}\right. 
$$

## another example

L inf regression problems

$$
\min_{x}\left\|Ax -v \right\|_\infty \quad A\in R^{m\times n},l\in R^n
$$

this is equivalent to (with slack variable)

$$
\left\{\begin{aligned} 
\min_{x,t}t \\
s.t. \quad \left\|Ax -v \right\|_\infty \leq t

 \end{aligned}\right. 
$$


$$
\left\{\begin{aligned} 
\min_{x.t} t\\
s.t. \quad   a_i^T x - v_i \leq t\\
a_i^T x - v_i \geq -t\\

 \end{aligned}\right. 
$$

### L1 regression problem

$$
\min_x \left\|Ax-v \right\|_1 
$$

is equal to 
$$
\left\{\begin{aligned} 
\min_{x,u} \sum_{i=1}^{m}u_i\\
s.t. \quad   a_i^T x - v_i \leq u_i\\
a_i^T x - v_i \geq -u_i\\

 \end{aligned}\right. 
$$

which can be rewriteed as 
$$
\left\{\begin{aligned} 
\min _{x,u} 1^T u\\
s.t.\quad  a_i^T x - v_i \leq u_i\\
a_i^T x - v_i \geq -u_i\\
 \end{aligned}\right. 
$$


## Example: Network flows

consider the incidence matrix, for exmaple
$$
A=\left[\begin{array}{cccccccc}{1} & {1} & {0} & {0} & {0} & {0} & {0} & {-1} \\ {-1} & {0} & {1} & {0} & {0} & {0} & {0} & {1} \\ {0} & {-1} & {-1} & {-1} & {1} & {1} & {0} & {0} \\ {0} & {0} & {0} & {1} & {0} & {0} & {-1} & {0} \\ {0} & {0} & {0} & {0} & {0} & {-1} & {1} & {0} \\ {0} & {0} & {0} & {0} & {-1} & {0} & {0} & {0}\end{array}\right]
$$

The Problem of network flow can be treated as a linear programming problem

For example, the minimum cost network flow problem
$$
\min _{x}: c^{T} x: A x=b, \quad I \leq x \leq u
$$

Or the maximum flow problem
$$
\min _{x, t}: t: A x=t e, \quad I \leq x \leq u
$$
where $e^{T}=(1,0, \ldots, 0,-1)$

> Note, we will find $t$ a negtive value.

# Begin of quadratic programming

quadratic optimization problems is a slightly broader class

## Quadratic function

$$
f_0(x) = \frac{1}{2}x^T H x+  c^Tx +d\\
d \in R\\
c\in R^n\\
H\in R^{n\times n} symmetric
$$

linear program is a quadratic function

$$
\min f_0(x)\\
s.t.\quad A_{eq} x = v_{eq}\\
f_i(x)\leq 0
$$

where $f_0$ and $f_i$ are linear or quadratic

## recap

$$
p^* = \min_{x\in R^n} c^Tx + d = \left\{\begin{aligned} -\infty \quad  c\neq 0\\ d \end{aligned}\right. 
$$


## The bound of QP program
consider the problem 
$$
p^{*}=\min _{x \in \mathbb{R}^{n}} f(x) \doteq \frac{1}{2} x^{\top} H x+c^{\top} x+d
$$
**if** $H\succ 0$ we can write 
$$
f(x)=\frac{1}{2}\left(x-x_{0}\right)^{\top} H\left(x-x_{0}\right)+\alpha \geq \alpha
$$

$$
x_{0} \doteq-H^{-1} c, \alpha \doteq d-x_{0}^{\top} H x_{0}
$$

**if** $H$ is not invertible and $c\in R(H)$ then the solution
$$
\left\{-H^{\dagger} c+\zeta, \quad \zeta \in \mathcal{N}(H)\right\}
$$

**if** H is not invertible and $v\notin R(H)$ then the problem is unbounded below


## L2 regression
$$
f_0(x) = \left\|Ax-v \right\|_2 ^2
$$

we can rewrite it as 
$$
f_0(x) = x^TA^TAx - 2v^TA x + v^Tv
$$

this is standard quadratic form



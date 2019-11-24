# CUE
- write down a general quadratic constraind quadratic program
  - show the condition for this to be convex
- when the object function is quadratic(p.s.d.) and constraint is linear
  - transform this to an unconstrained quadratic problem
  - show the new p.s.d. property of it
- what are the different cases for the solution of a general quadratic objective program? (unconstrained)
- what is the LQR problem
- how to transfer it into a quadratic problem?

# Quadratic constraind quadratic program

$$
\begin{aligned}
p^* =& \min_x x^T H_0x + 2 c_0^T x+ d_0\\
\text{s.t.}\quad & x^T H_ix + 2 c_i^T x+ d_i \leq 0 \quad i=1...\\
& x^T H_jx + 2 c_j^T x+ d_j = 0 \quad j=1...\\
\end{aligned}
$$
> in general this is not convex

In order for this to be convex:
$$
\left\{\begin{aligned} H_0 \succeq 0 \\
H_i \succeq 0 \\
H_j = 0
\end{aligned}\right. 
$$


**Note:** $H_j$ should be $0$, otherwise it is not convex

Imageine No quadratic constraints (just for this example)
$$
p^* = \min_x x^T H_0x + 2 c_0^T x+ d_0\\
Ax = v
$$

the constraint $Ax = v$  is a set of linear equations

- $v \notin \mathcal{R}(A)$ 
  - the problem is not feaisble
  - $p^* = +\infty$
- $v \in \mathcal{R}(A)$
  - $x = \bar{x}+Nz$ $N$ is the null space matrix
  - then we can do the optimization over $z$, then the constraint can be ignored
  
Question be, what is the corresponding unstrainted quadratic program look like?

$$
p^* = \min_x (\bar{x}+Nz)^T H_0(\bar{x}+Nz) + 2 c_0^T (\bar{x}+Nz)+ d_0
$$
this is quadratic form
$$
z^TN^TH_0Nz + 2 (\bar{x}^TH_0N+C_0^TN)z + \bar{x}^T\bar{x} + 2 c_0^T\bar{x} + d_0
$$

> Note you have to say that this is leagle because $H_0$ p.s.d. so $N^TH_0N$ is also p.s.d.

## Generic solution to QP

$$
P^* = \min _x \frac{1}{2} x^THx +c^Tx +d
$$

cases:

**1.** $H$ has a negative eigenvalues

$\exist \lambda_1 \in  \text{spec}(H) \text{s.t.}\quad \lambda_1 <0$

let $e_1$ be the corresponding eigenvector

$$
f_0(\alpha e_1) = \frac{1}{2}\alpha ^2 e_1^THe_1 + \alpha c^Te_1 +d 
$$
in this way $p^* = -\infty$

example 
$$
f_0(x,y) = -xy = (x,y)\left[\begin{array}c 0 & -1 \\ -1 & 0 \end{array}\right] \left[\begin{array}c x \\y \end{array}\right] 
$$

this function is not only bad as a objective, but also bad as a constraint for example:
$$
f_0(x) \leq d
$$
this will have a 双曲线 and not convex

### **case2**

if $\forall \lambda_i \in \text{spec}(H) \quad \lambda _i \leq 0 \Rightarrow f_0 \text{convex}$

$$
\nabla f_0   (x^*) = 0 \text{ at the optimum}
$$


$$
\nabla f_0(x) = Hx+c = 0
$$

thus, if here is a minimum it should satisfy:
$$
Hx+c = 0
$$

### **case 2.a**
$$
c \notin R(H)
$$

there is no solution for this linear equation

$$
P^* = -\infty 
$$

example:
$$
p^* = \min_x  \left[\begin{array}c x & y \end{array}\right] \left[\begin{array}c 1 & 0 \\ 0 & 0 \end{array}\right] \left[\begin{array}c x \\ y \end{array}\right]  + \left[\begin{array}c 0 \\ -1 \end{array}\right] \left[\begin{array}c x \\y \end{array}\right]  + 5
$$

### **case 2.b**
$$
C\in R(H)
$$

thus 
$$
x^* = -H^\dagger c + \zeta \quad \zeta \in \mathcal{N}(H)
$$

thus 
$$
H(x^* + \zeta) = Hx^* + H\zeta 
= H^* = c
$$

### **Case 2.b*** special case

if $H$ is invertible $H\succ 0$

In this case, you can invert $H$ 
$$
x^* = - H^{-1} c\quad \text{unique solution}
$$


## applications

> A little story, a stanford professor mathmatically proved that for an air craft, to get the steepest climb, you have to dive first. Talked to general in the airspace, don't believe, but found his way to let pilot to try it.


**LQR problem**


for a system
$$
\left\{\begin{aligned}
x_{t+1} &= Ax_t + Bu_t\\
x_0  &= x_{\text{given}}
 \end{aligned}\right. 
$$

$$
A \text{ dynamics }\in R^{n\times n}\\
u_t : \text{control vector}
$$

**Question:** How to determine $u_t, \; t = 1...N$ to achieve optimal performance



**How do you define performance**

the most performance is the combination of three things

$$
J(u) = \sum_{\tau = 1}^{N}\left( \underbrace{x_\tau ^T Q x_\tau}_{\text{penalty the cummulative error}} + \underbrace{u_\tau ^T R u_\tau }_{\text{penalty of feul}}  \right)+ \underbrace{x_N^TQx_N}_{\text{final error}}
$$

where $R,Q \succeq 0$

$$
LQR: \min_{u_{1},u_{2},\dots,u_{n}} \sum_{\tau = 1}^{N}\left( x_\tau ^T Q x_\tau + u_\tau ^T R u_\tau   \right)+ x_N^TQx_N\\
\text{s.t.}\quad x_{t+1} = Ax_t + Bu_t \\
u_t \in [0,u_{\text{max}}] \forall t
$$

$$
\left[\begin{array}c x_{1}\\x_{2}\\\dots\\x_{n} \end{array} \right]  = 
\left[\begin{array}c B \\ AB & B \\ A^2B & AB & B  \end{array}\right] 
\left[\begin{array}c u_0 \\ \dots \\ u_{n-1} \end{array}\right] + 
\left[\begin{array}c A^{1}\\A^{2}\\\dots\\A^{n} \end{array}\right] x_0
$$

thus 
$$
\Chi = G\mathbb{U} + \mathbb{H}X_0
$$

$$
\min \mathbb{\Chi }^T\left[\begin{array}c \sqrt{Q} && \\ & \ddots &\\ &&\sqrt{Q}  \end{array}\right] 
\left[\begin{array}c \sqrt{Q} && \\ & \ddots &\\ &&\sqrt{Q}  \end{array}\right]\Chi \\

+  \mathbb{U}^T \left[\begin{array}c \sqrt{R} && \\ & \ddots &\\ &&\sqrt{R}  \end{array}\right] 
\left[\begin{array}c \sqrt{R} && \\ & \ddots &\\ &&\sqrt{R}  \end{array}\right] \mathbb{U}
$$

$$
\min J(u) = \left\|\text{diag} (\sqrt{Q},\dots,\sqrt{Q}) (GU+Hx_0)\right\|_2^2 + \left\|\text{diag} (\sqrt{R},\dots,\sqrt{R}) \mathbb{U}\right\|_2^2  
$$

> Note here $\Chi, \mathbb{U}$ are vectors, but they are the concatenation of the state vectors and inputvectors. 
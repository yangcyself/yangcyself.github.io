# CUE

# Sion's Minimax theorem

Let $x\subset R^{n}$ be convex

Let $t\subset R^{n}$ be concact

F: 
$$
x\times y \rightarrow R\\
\text{s.t.}\quad F(.,y) \text{ is convex, cts}\\
\qquad\quad F(x,y) \text{ is concave, cts}
$$

then 
$$
\max _{y\in Y} \min _{x\in X} F(x,y) = \min _{x\in X}  \max _{y \in Y} F(x,y)
$$

## examples: LASSO

$$
p^{*} = \min _{x} \frac{1}{2} \left\|Ax-b \right\|_2 ^{2} + \lambda \left\|x \right\|_1 
$$

$$
\mathcal{L}(x) = f(x)
$$
then the dual problem

it is just the original problem

Add a dummy variable

$$
p^{*} = \min _{x,z} \frac{1}{2}\left\|z \right\|_2 ^{2} + \lambda \left\|x \right\|_1 \\
\text{s.t.}\quad z=Ax-b
$$

stata condition holds -> strong duality holds( Since convex)

> why since convex

$$
p^{*} = \min _{x,z} \max _{\upsilon } \mathcal{L}(x,z,\upsilon)\\
= \min _{x,z} \max _{\upsilon }  \frac{1}{2}\left\|z \right\|_2 ^{2} + \lambda \left\|x \right\|_1 + \upsilon ^{T} (z - Ax+b)
$$

by strong duality 

$$
=  \max _{\upsilon } \underbrace{\min _{x,z} \frac{1}{2}\left\|z \right\|_2 ^{2} + \lambda \left\|x \right\|_1 + \upsilon ^{T} (z - Ax+b)}_{g(\upsilon )}
$$
separate the min of x and the min of z
$$
g(\upsilon ) = \upsilon ^{T} b + \min _{x} \lambda \left\|x \right\|_1  - x^{T} A^{T} \upsilon + \min _{z} \frac{1}{2}\left\|z \right\|_2 ^{2} + \upsilon ^{T} z
$$


process the $\min z$

$$
z^{*}  = -\upsilon , \min _{z}  = -\frac{1}{2}\left\|\upsilon  \right\|_2 ^{2} 
$$

process the $\min x$

$$
\min _{x} \lambda \left\|x \right\|_1   - x^{T} A^{T} \upsilon \\
= \left[ \max _{x} x^{T} (A^{T} \upsilon )-\upsilon \max_{y:\left\|y \right\|_\infty \leq 1}  y^{T} x\right]
$$

this is another min max

$$
= - \left[ 
    \max _{x} \min _{y:\left\|y \right\|_\infty \leq 1}  x^{T} (A^{T} \upsilon  - \lambda y)
     \right]\\
= -\left[ 
     \min _{y:\left\|y \right\|_\infty \leq 1} \max _{x} x^{T} (A^{T} \upsilon  - \lambda y)
     \right]\text{ by sion's}
$$

$$
= -\left[ 
     \min _{y:\left\|y \right\|_\infty \leq 1} 
     \left\{\begin{aligned} 
     &0 \qquad A^{T} v - \lambda y=0 \\
     &\infty  \qquad  otherwise
      \end{aligned}\right. 
     \right]
$$

$$
 = \left\{\begin{aligned} 
 &0 & \left\|A^{T} \upsilon  \right\|_\infty \leq \lambda \\
 &-\infty 
 
  \end{aligned}\right. 
$$



$$
\max _{\upsilon }g(\upsilon ) = \max _{\upsilon }\upsilon ^{T} b-\frac{1}{2}\left\|\upsilon  \right\|_2  ^{2} \\
\text{s.t.}\quad \left\|A^{T} \upsilon  \right\|_\infty \leq \lambda 
$$


# Dual norms

For a norm on $R^{n}$ the dual norm of it is 
$$
\left\|. \right\|_* = \max _{\left\|z \right\| \leq 1 }z^{T} x 
$$



For Lp norms

dual of $L_{p}$ norm is $L_{q}$ where 
$$
\frac{1}{p}+\frac{1}{q} = 1
$$

## example square-root- LASSO

$$
p^{*} = \min _{x} \frac{1}{2} \left\|Ax-b \right\|_2 ^{2} + \mu  \left\|x \right\|_1 
$$

$$
= \min _{x} \max _{\mu ,\upsilon } \mu ^{T} (Ax -b) + \upsilon ^{T} x\\
\text{s.t.}\quad \left\|\mu  \right\|_2 \leq 1\\
\left\|v \right\|_\infty \leq \mu 
$$

it is affine if we hold $\mu$ or $\upsilon$ constant

because of the Sion's 

$$
=  \max _{\mu ,\upsilon } \min _{x}\mu ^{T} (Ax -b) + \upsilon ^{T} x\\
\text{s.t.}\quad \left\|\mu  \right\|_2 \leq 1\\
\left\|v \right\|_\infty \leq \mu \\
= \max _{u,v} \left\{\begin{aligned} &b^{T} u& A^{T} u = b\\
&-\infty & o.w  \end{aligned}\right. 
$$

$$
p^{*} = \max _{u} b^{T} u\\
\text{s.t.}\quad \left\|u \right\|_2 \leq 1\\
\left\|A^{T} u \right\|_\infty \leq u\\
\left\|u \right\|_\infty \leq  v
$$
> this form is wrong
git rid of v
$$
p^{*} = \max _{u} b^{T} u\\
\text{s.t.}\quad \left\|u \right\|_2 \leq 1\\
\left\|A^{T} u \right\|_\infty \leq u
$$

change the inf norm

$$
p^{*} = \max _{u} b^{T} u\\
\text{s.t.}\quad \left\|u \right\|_2 \leq 1\\
|a_i^{T} u | \leq u
$$

> ...

this is called **safe featrue elimination**


# KKT

$$
p^{*}  = \min _{x} F_{0} (x)
\\

\text{s.t.}\quad F_{1} (x)\leq 0, \\
h_{i} (x) = 0
$$

the lagrangeian fproblem

the dual problem

$$
p^{*} = \min _{x} \max _{\lambda \geq 0, \gamma  } L(x,\lambda ,\upsilon )
\\
d^{*} =  \max _{\lambda \geq 0, \gamma  }\min _{x} L(x,\lambda ,\upsilon )
$$

Assume storng duality

let $x^{*}$ be primal solution, $\lambda ^{*},\upsilon ^{*}$ be dual solution

$$
f_{0} (x^{*}) = g(\lambda ^{*} ,\upsilon ^{*}) \text{ S.D.}\\
= \min _{x} f_{0} (x)+ \sum_{}^{}\lambda f_{i} (x) + \sum_{}^{}\upsilon h(x) \\
\leq f_{0} (x)+ \sum_{}^{}\lambda f_{i} (x) + \sum_{}^{}\upsilon h(x)\text{ defn of }\min _{x}\\
\leq f_{0} (x^{*} ) \text{ by feasibility}
$$

Then we can find this should be equlality

then
$$
\Rightarrow \sum_{}^{}\lambda f_{i} (x^{*} ) = 0\\
$$

this is called **complementatiory slackness**

KKT conditions

Assume additionally a convex program
1. primal feasi
2. Dual feasi
3. stationarity $\Leftrightarrow \nabla_{x}(L(x,\lambda ^{*},\upsilon ^{*}  ))|_{x=x^{*}}  = 0$
4. complementary slactness


## complementary slackness

We know that 
$$
\lambda _{i} ^{*} f_{i} (x^*) =0
$$
there are two cases
### case1

- constraint $f_{i}$ is inactive
- $\lambda _{i}^{*}=0$ 
- constriant can be perturbed without effect on optimal value

### case2
- $f_{i}=0$ is tight or active
- if we change the $f$ the optimal value of can be changed

$\lambda _{i}^{*}$ tells us the sensitivity of the optimal value to the perturbation in $f$

**shasow price**

## Sensitivity interpretation of dual variables

consier perturbed problem:

$$
p^{*} (t,u) = \min _{x} f_{0} (x)\\
\text{s.t.}\quad f_{i} (x) \leq t_{i} \\
h_{i} (x)= u_{i} 
$$


p^{*} (0,0) recovers  the original problem

Assume strong dality
$$
\forall x \in X_{t,u} \\
p^{*} (0,0) = g(\lambda ^{*} ,\upsilon ^{*} )\leq L(x,\lambda ^{*} ,\upsilon ^{*} )

\\
\leq f_{0} (x) + \lambda ^{*T}  t+\upsilon ^{*T} u
$$

thus 
$$
f_{0} (x) \geq p^{*} (0,0) - \lambda ^{*T}  t- \upsilon ^{*T} u, \forall x \in X_{t,u} 
$$

holds for $x^{*} (t,u)$

$$
f_{0} (x^{*} (t,u)) = p^{*} (t,u)
$$

gives a lower bound of the pertubed problem

$$
p^{*} (t,u)\geq p^{*} (0,0) - \lambda ^{*T} t - \upsilon ^{*T} u
$$

if $t_{i}<0$ $\lambda _{i} >>0$ then the lowerbound increase quickly 
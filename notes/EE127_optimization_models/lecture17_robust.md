# CUE
- what does the robust optimization mean?
- Transform the linear objective with box uncertainty into a LP, and conclude that this is SOCP
  - why do we only care about the linear objective
- Transform the sphere uncertaintity to the SOCP
- Transform the ellipsoid uncertaintity to the SOCP
- What if the constraint is probabilistic

robust: sustain the perturbation

# Robust optimization
consider a problem

$$
\min_x f_0(x)\\
f_i(x) \leq 0 \quad \forall i = 1,\dots, m
$$

you have to admit **imperfection exist in your model**

Robust counterpart to

$$
\min_x \max _{u\in U} f_0(x,u) \\
f_i(x) \leq 0 \quad \forall i = 1,\dots, m
$$
the $u$ is pusing you to the other direction

imagine $f_0(x,u)$ is convex in $x$

then **good news** convexity is inherited

### **Scenrio based uncertainty**
for example in linear problem

$$
a_i^T x \leq b\\
a_i \in u_i
$$

the problem 
$$
\min c^Tx\\
\text{s.t.}\quad a_i^T x \leq b \qquad \forall a_i \in u_i
$$

**uncertainty in objective**

$$
\min _x \max  c^Tx\\
c\in U
\\
a_{i} ^{T} x \leq b_{i} 
$$

> this means optimizing in the **worst case**

make a slack and it backs to scenerio based uncertainty

## Box uncertainty:
Assume the uncertainty is a box
$$
u = \left\{a|\left\|a -\hat{a} \right\|_\infty \leq \rho \right\}\\
= \left\{\hat{a}+\rho \mu   | \left\|\mu  \right\|_\infty \leq 1 \right\}
$$

$$
\max_{a\in u}(a^Tx) = \max_{u|\left\|u \right\|_\infty \leq 1}\left\{[\hat{a}+\rho u]^T x \right\}\\
= \hat{a}^Tx + \max_{u|\left\|u \right\|_\infty \leq 1}(\rho u^Tx)\\
= \hat{a}^Tx +\rho \left\|x \right\|_1 
$$

back to the problem

it is equal to
$$
\min c^Tx\\
\text{s.t.}\quad \hat{a}^T x + \rho \left\|x \right\|_1  \leq b
$$

thus Box uncertainty $\Rightarrow$ LP

## sphere uncertainty

$$
a = \hat{a} + \rho \left\|u \right\|_2 
$$

thus it is equal to 

$$
\max _{u|\left\|u \right\|_2 \leq 1 }a^Tx\\
\max _{u|\left\|u \right\|_2 \leq 1 }\left[ \hat{a}^Tx+ \rho u^Tx \right]\\
= \hat{a}x+ \left\|x \right\|_2 
$$

so the constraint
$$
a^Tx \leq b\\

\hat{a}^Tx + \rho \left\|x \right\|_2 \leq b
$$

this is **SOCP**

## Potato uncertainty

consider ellipsoid


$$
\epsilon  = \left\{a|(a-\hat{a})^TP^{-1}(a-\hat{a})\leq 1  \right\}
$$

still the problem
$$
a = \hat{a} + Ru | \left\|u \right\|_2 \leq 1
$$

where $R$ is get from Cholosky decomposition $RR^T = P$

thus 
$$
(\hat{a} + Ru )^Tx \leq b
$$


then we get 

$$
\hat{a}^Tx +  \left\|R^Tx \right\|_2 \leq b
$$

this is again, SOCP 

### most general form of the ellipoid uncertainty

$$
\min _x c^Tx\\
\text{s.t.}\quad \forall a_i \in \epsilon _i\\
a_{i} ^T \leq b^{i} 
$$

then 
$$
\min _x c^Tx\\
\hat{a}^Tx +  \left\|R^Tx \right\|_2 \leq b
$$

# Chance constraint

## example of LP

$$
\min c^Tx\\
\text{s.t.}\quad a_{i} ^Tx\leq  b_{i} 
$$

where $a_{i}$ is a gaussian $E[a_{i}] = \bar{a}, var[a_{i}] = \Sigma$

Note that 
$$
E[a_{i} ^Tx] = \bar{a}_{i} ^T x\\
\text{var}(a_{i} ^Tx) = x^T\Sigma x
$$

you can normalize it

$$
\sigma _{i} (x) = \sqrt{x^*\Sigma_ix}\\
P(\sigma _{i} (x)\leq \tau _{i} (x))\geq P_{i} 
$$

the earth function?


$$
\text{erf}(x) = \frac{2}{\sqrt{\pi}}\int_{0}^{x}e^{-t^{2} dt}
$$

thus
$$
\frac{b_i - \bar{a_i}^Tx}{\sqrt{x^T\Sigma_i x}}  \geq \Phi^{-1} (P_{i} )
$$


thus we get
$$
b_i - \bar{a_i}^Tx \geq  \sqrt{x^T\Sigma_i x} \Phi^{-1} (P_{i} )
$$

this is **SOCP**, see

$$
\left\|\Sigma^{\frac{1}{2}} x  \right\|_2 \Phi^{-1} (P_{i} ) \leq b_i - \bar{a_i}^Tx 
$$

## example **robust least square**

assume an imperfect model

$$
\min _x \left\|Ax-y \right\|_2 A\in R^{m\times n}  y \in R^{m} 
$$

A is not perfect
$$
\left\|A - \hat{A} \right\| \leq \rho 
$$

> Note the A is not a square matrix so the norm is SVD norm

### the svd norm recap

$$
A \in  R^{m \times n} 
\left\|A \right\|  = \sup _x    \frac{\left\|Ax \right\|_2 }{\left\|x \right\|_2 }
$$

by SVD: the svd norm is the max singular value

let $A = \hat{A} + \Delta$ and $\left\|\Delta  \right\|\leq \rho$ is the pertubation

the robust becomes 
$$
\min _x \max _{\left\|\Delta  \right\|\leq \rho} \left\|(\hat{A}+\Delta )x - y \right\|_2 
$$

can we reformulate the problem as a known problem

triangular ineq:

$$
\left\|(\hat{A}+\Delta )x - y \right\|_2  \leq   \left\|\hat{A}x - y \right\|_2 + \left\|\Delta x \right\|_2 
$$

by the matrix norm

$$
\left\|\Delta x \right\|_2 \leq \rho \left\|x \right\|_2 
$$

thus 
$$
\max _{\left\|\Delta  \right\|\leq \rho} \left\|(\hat{A}+\Delta )x - y \right\|_2  \leq  \left\|\hat{A}x - y \right\|_2 + \rho \left\|x \right\|_2 
$$

It turns out that **this inequality is TIGHT** it is possible to have equality

> **Tight**: $\exist \Delta ^*$ that achieve equality

and good news, this $\Delta ^*$ can be computed explicitly
$$
\Delta ^* = \frac{\rho }{\left\|\hat{A}x - y \right\|_2 \left\|x \right\|_2 }\left( \hat{A}x - y \right) x^T
$$

proof this is the worst case (plug in and verify)

$$
(\hat{A}+\Delta ^*)x -y = \left[ \hat{A} + \frac{\rho }{\left\|\hat{A}x - y \right\|_2 \left\|x \right\|_2 }\left( \hat{A}x - y \right) x^T \right]x -y\\
= \left[ \hat{A}x + \frac{\rho }{\left\|\hat{A}x - y \right\|_2  }\left( \hat{A}x - y \right) \right] - y\\
= \left[( \hat{A}x -y )+ \frac{\rho }{\left\|\hat{A}x - y \right\|_2  }\left( \hat{A}x - y \right) \right]\\
= \left[ \frac{\hat{A}x -y}{\left\|\hat{A}x -y \right\|_2 } \right]\left[ \left\|\hat{A}x -y \right\| + \rho \left\|x \right\|_2  \right]
$$
then 
$$
\left\|(\hat{A}+\Delta ^*)x -y \right\|_2  = \left\|\hat{A}x -y \right\| + \rho \left\|x \right\|_2
$$
this is worst

> QUESTION: what if the $\hat{A}x - y = 0$\
> II I think in this case, every $\left\|\Delta \right\| = \rho$ do. So we don't have to choose the direction, (other wise the $\hat{A}x - y = 0$ term is used for choosing direction)


then, this is L2 regularized LS problem, (sum of norms problem)

$$
\min _x \mu + \rho \upsilon \\
\left\|\hat{A}x - y \right\|  \leq \mu \\
\left\|x \right\|_2 \leq   \upsilon 
$$

then this is ***SOCP***


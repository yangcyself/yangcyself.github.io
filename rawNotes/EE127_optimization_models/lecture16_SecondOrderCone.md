# CUE
- what is the second order cone model?
- how to transform the constraint where x^Tx leq 2yz
- what is the standard form of second order cone program?
- what is the relationships between LQ, convex QP, QCQP, SOCP
- how to express quadratic constraint as SOCP form?
- express the max and sum of norms in SOCP form
- rewrite inventory control prblem (hx + cd/x) as SOCP
- what is Facility location problem and express it as SOCP
- express Square root lasso as SOCP
- understand the Examplar selection's objective SOCP
- express the least square problem with $\lambda |w|^{\frac{3}{2}}$ regularization term as SOCP

> LQR in general is completely uncractable, because it is too large

> we will talk about how to solve it recursive later (Dynamic programming solution)

>watch EE363 on youtube


# second order cone models

## defn of a cone

$$
k_n = \left\{(x,t) | x\in R^n\; t\in R \; \left\|x \right\|_2 \leq t \right\}
$$

### **second order cone**

### **rotated second order cone**

$$
K_n^r = \left\{(x,y,z)| x\in R^n \; y \in R \; z\in R
\quad
x^Tx \leq 2yz, y \geq 0\; z \geq 0
 \right\}
$$

**allgebraic lemma**
consider 
$$
\left\|\left[\begin{array}c 
x \\
\frac{1}{\sqrt{2}}(y-z)
 \end{array}\right]  \right\|_2 

 \leq  \frac{1}{\sqrt{2}} (y+z)
$$

take square
$$
\left\|x \right\|_2 ^2  + \frac{1}{2}(y-z)^2 \leq  \frac{1}{2}(y+z)^2\\
\left\|x \right\|_2 \leq 2yz 
$$

let this remind you ratation matrix in $R^2$

$$
R_\theta = \left[\begin{array}c \cos \theta & - \sin \theta \\ \sin \theta & \cos \theta \end{array}\right] 
$$

**note the equivalent commonly used in SOCP**

$$
\left\|x \right\|_2 ^2 \leq 2yz , y\geq 0, z\geq 0 \\
\Leftrightarrow \\
\left\|\left[\begin{array}c 
x \\
\frac{1}{\sqrt{2}}(y-z)
 \end{array}\right]  \right\|_2 

 \leq  \frac{1}{\sqrt{2}} (y+z)

$$
this from the 3-step-lemma


**assemble** them together
$$
\underbrace{\left\|\left[\begin{array}c 
x \\
\frac{1}{\sqrt{2}}(y-z)
 \end{array}\right]  \right\|_2 
}_{\left\|w \right\|_2 }
 \leq  \underbrace{\frac{1}{\sqrt{2}} (y+z)}_t

$$
thus,

$$
(x, y, z) \in \mathcal{K}_{n}^{r} \text{ iff }  (w, t) \in \mathcal{K}_{n}
$$
where 
$$
w=(x,(y-z) / \sqrt{2}), \quad t=(y+z) / \sqrt{2}
$$

in matrix form
$$
\left[\begin{array}c 
x \\
\frac{1}{\sqrt{2}}(y-z)\\
\frac{1}{\sqrt{2}}(y+z) 
 \end{array}\right] 
 =
 \left[\begin{array}c I & 0 & 0\\ 0 & \frac{1}{\sqrt{2}} &-\frac{1}{\sqrt{2}} \\0 & \frac{1}{\sqrt{2}} &\frac{1}{\sqrt{2}}
  \end{array}\right] 
  \left[\begin{array}c x \\ y\\z \end{array}\right] 
$$
the middle one is a rotation matrix

thus

$$
\left[\begin{array}c w \\t \end{array}\right]  =
R \left[\begin{array}c x \\ y \\z \end{array}\right] \\
\left[\begin{array}c x \\ y \\z \end{array}\right]  = R^{-1} \left[\begin{array}c w \\t \end{array}\right]
$$

> if you express the cone in the second format it is really helpful, because $yz$ is not convex



**although $yz$ is not convex, but it is a cone**

> $\left\|x \right\|_2^2 \leq 2yz$ always refered as hyperbolic constraints




> rotated second order cone is just a special case for the SOCP
## Second-order cone programs


See the standard optimazation form

$$
\left\{\begin{aligned} 
p^* = \min f_0 (x)\\
\text{s.t.}\quad f_i(x)\leq 0
 \end{aligned}\right. 
$$

the standard S.O.C constraint 
$$
\left\|Ax+b \right\|_2 \leq c^Tx +d
$$
A second-order cone program is a convex optimization problem having linear
objective and SOC constraints

formulate second order conic program in standard form

$$
\left\{\begin{aligned} 
\min_{x\in R^n} c^Tx\\
\text{s.t.}\quad \left\|A_ix+b_i \right\|_2 \leq c_i^Tx+d_i \\
i = 1 \dots m

 \end{aligned}\right. 
$$

## the clases
$$
\text{LP} \subset \text{convex QP} \subset \text{convex QCQP} \subset \text{SOCP}\subset \text{robotst} \subset \text{convex}
$$



Trival: why is an LP a SOCP

because it is same as 
$$
\left\{\begin{aligned} 
A_i = 0\\
b_i = 0\\
c_i = -\alpha _i \\
d_i = \beta _i
 \end{aligned}\right. 
$$

what about the quadratic constraint?

$$
x^TQx + c^Tx \leq t
$$

this constraint can be dexpressed as 
$$
\left\|\left[\begin{array}c 
\sqrt{2}Q^{\frac{1}{2}}x \\

t - c^Tx - \frac{1}{2}

 \end{array}\right]  \right\|_2 
 \leq 
 t - c^Tx +\frac{1}{2}
$$

prove:
do the three steps

> but three steps is only intuition, **it is ILLEGAL, you cannot square back and forth**

> by putting the things in the norm(unsqurared) form,  ypu are convex, but the squared form may not be convex (because the might be negtive)



$$
\min_x x^TQx+ c^Tx\\
\text{s.t.}\quad x^Tx \leq v_i
$$



Generic QP 
$$
\min _x x^TQ_0x + a_0^T x\\
\text{s.t.}\quad  x^TQ_ix + a_i^T x\leq  v_i
$$
is rewritten as:
$$
\min    a_0^Tx +t\\
\text{s.t.}\quad \left\|\left[\begin{array}c 2 Q_0^{\frac{1}{2}}x\\t-1 \end{array}\right]  \right\|_2 \leq t+1\\
\left\|\left[\begin{array}{c}{2 Q_{i}^{1 / 2} x} \\ {b_{i}-a_{i}^{\top} x-1}\end{array}\right]\right\|_{2} \leq b_{i}-a_{i}^{\top} x+1, \quad i=1, \ldots, m
$$

## example of SOCP

### example 1
**sum of norms or max of norms**

$$
\min _x \sum_{i=1}^{p}\left\|A_ix+b_i \right\|_2 
$$

this is sum of convex funcion is convex

rewrite
$$
\min_{x,y} \sum_{i=1}^{p}y_i\\
\text{s.t.}\quad \left\|A_ix+b_i \right\|_2 \leq y_i
$$
this becomes SOCP

$$
\min \max_{i=1}^p \left\|A_ix -b_i \right\|_2 
$$

this si gneeral convex

rewrite
$$
\min_{x.y} y \\
\text{s.t.}\quad \left\|A_ix - b_i \right\|  \leq y \; \forall i = 1 \dots p
$$

### **Inventory control**

Hannis 1913

$$
\min_{x>0} \left[ hx + \frac{cd}{n} \right]
$$

h: annal cost of storage
c: cost of delivery
d: dimension
n: quantitis of stullff

**you have bunch of things**

$$
\min_x   \sum_{i=1}^{n}h_ix_i + \frac{c_id_i}{x_i}
\\
b^Tx\leq b_0\\
l \leq x \leq u
$$
this is gneeral convex form


rewrite in SOCP form

$$
\min _{x,y} \sum_{i=1}^{n} h_ix_i + {c_id_i}{y_i}\\
b^Tx\leq b_0\\
l \leq x \leq u\\
y_ix_i \geq 1
$$

this is because $y_i \geq \frac{1}{x_i}$

Note the $y_ix_i \geq 1$ is not convex but you can transform it into 

$$
\left\|\left[\begin{array}c 2\\y_i - x_i  \end{array}\right] \right\|_2 

\leq y_i+x
$$
this is SOCP constraint

> 为什么可以把unconvex搞成convex的啊？
> > 我觉得没有说它不convex，$\frac{c_id_i}{x_i}$在正半轴也是convex的，只不过我们换了一个方向看它，变成cone了

> 所以SOCP是不是只有有$yz>$的形式的时候才是一个cone，如果是$yz<$的话就不行？


## Facility location problem

put the facility to a location that the maxmium to go to targets is the as small as possible
> 这不是算法那个问题嘛
> > 不是，那个是K个center
$$
\min _x \max _{i=1}^m \left\|x - y_i \right\|_2 
$$

rewrite 
$$
\min t\\
\text{s.t.}\quad \left\|x - y)i \right\|_2 \leq t \\
\forall i = 1 \dots m
$$

if you want to minimize the avg
$$
\min_x  \frac{1}{m}\sum_{i=1}^{m} \left\|x-y_i \right\|_2 
$$

this still SOCP

$$
\min_{x,t} \frac{1}{m} \sum_{i = 1}^{m}t_i\\
\text{s.t.}\quad \left\|x - y)i \right\|_2 \leq t_i
$$

### **LASSO problem**

$$
\min_w \left\|X^Tw -y \right\|_2 + \lambda \left\|w \right\|_1 
$$

$$
\min_t t+ \sum_{}^{}u_i \lambda \\
\text{s.t.}\quad \left\|X^Tw -y \right\|_2 \leq t SOCP\\
w_i \leq  u_i\\
-u_i \leq  w_i\\
$$

### **examplar selection**
we want to select a subset of datapoint to linearly fit the whole dataset

$$
\forall i \in\{1, \ldots, n\}: x_{i} \approx \sum_{j \in \mathcal{J}} x_{j} w_{i j}
$$
The optimization program is:
$$
\min _{W=\left[w_{1}, \ldots, w_{m}\right]}\left\|X-X W^{T}\right\|_{F}: \sum_{j=1}^{m}\left\|w_{j}\right\|_{2} \leq \kappa
$$
> still not fully understood
### **general regression problems**

$$
p^{*}:=\min _{w}\left\|X^{T} w-y\right\|_{2}+\lambda \sum_{i=1}^{n}\left|w_{i}\right|^{\alpha}
$$

take $\alpha  = \frac{3}{2}$ as exmaple, $t\geq u^{\frac{3}{2}}$ for $u\geq 0$ is equivalent to exist $v\geq 0$ s.t.
$$
v t \geq u^{2}, \quad u \geq v^{2}
$$

thus the problem where $\alpha =\frac{3}{2}$ is 
$$
p^{*}=\min _{w, v, u, t}\left\|X^{T} w-y\right\|_{2}+\lambda \sum_{i=1}^{n} t_{i}: \quad \begin{array}{r}{t \geq 0, \quad u \geq|w|} \\ {v_{i} t_{i} \geq u_{i}^{2}, \quad u_{i} \geq v_{i}^{2}, \quad i=1, \ldots, n}\end{array}
$$

> **Have not understood, but I have to move ON**
> > Now I understood(2019-11-10 10:18:04), to get the iequivalent$v t \geq u^{2}, \quad u \geq v^{2}$, write them as inequalities of $v$: $v \leq u^{\frac{1}{2}}, v \geq \frac{u^2}{t}$, so $v$ exists iff the original constraint is satisfied. And we have to put it into the orders of 1 and 2. 


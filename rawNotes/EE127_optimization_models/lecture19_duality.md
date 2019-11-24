# CUE
- prove that max min f(x,y) <= min max f(x,y)
- Given a standard problem, construct its lagrangian, dual problem.
- What is the slata condition for strong duality?
- when will the optimal point reached?
- KKT condition
- Sion's min/max theorem
# Warm up exercise

Let us consider 
$$
F: \mathcal{X}\times \mathcal{Y} \rightarrow \mathcal{R}\\
\max _{y\in Y} \min _{x} F(x,y)\leq \min_{x} \max _{y} F(x,y)
$$

## Proof

fix $x_{0} ,y_{0}$


we have 
$$
\underbrace{\min _{x} F(x,y_0)}_{g(y_{0} )} \leq F(x_{0}, y_0)\\
F(x_{0}, y_0) \leq \underbrace{\max_{y} F(x_{0}, y) }_{g(x_{0} )}
$$

thus 
$$
\forall (x_{0} ,y_{0} ) h(y_{0} ) \leq g(x_{0} )\\
\max _{y_{0} } h(y_{0} ) \leq \min _{x_{0} } g(x_{0} )
$$


> to rationalizae this thing, you think that the inner loop goes first\
> "It also has to do prisoner dillema"?

# Duality

start from the **primal problem**
$$
p^* = \min _{x} f_{0} (x)\\
\text{s.t.}\quad f_{i} (x)\leq 0\\
g_{i} (x) = 0
\tag{1}
$$

call the domain of the program $\mathcal{D}$

**Construct a dual problem**
> importantly, this is ***always convex***
> It also is a lower bound of the objective

- When the primal is convex, under ertain condition, the two coincide, and solving the second is easier
- In some cases, the solution to the primal can be recoverd from the dual

# Lagrangian
it is an operator
$$
\mathcal{L}: \mathcal{D}\times \underbrace{R^{m} \times R^{q}}_{\text{the constraints}} \rightarrow R
$$

$$
\mathcal{L}(x,\lambda ,\gamma ) = f_{0} (x)+ \sum_{i=1}^{m}\lambda _{i} f_{i} (x) + \sum_{j=1}^{q} \gamma _{i} g_{i} (x)
$$

Note that you need no assumption of covexity of $f_{i}$ and $g_{i}(x)$

$\lambda$ and $\gamma$ are called *Lagrange multipliers*

## lagrange dual function

$$
g(\lambda ,\gamma)  = \inf _{x\in \mathcal{D}} \left[ 
    f_{0} (x)+ \sum_{i=1}^{m}\lambda _{i} f_{i} (x) + \sum_{j=1}^{q} \gamma _{i} g_{i} (x) \right]
    \forall \lambda _i  \geq 0
$$


Note that 
> Note that $g(.,.)$ is the lagrange dual..\
> $g(.)$ is the constraint

Note that $g(\lambda ,\gamma )$ could be unbounded below

### proposition

- $g(\lambda  ,\gamma )$ is concave if $\lambda ,\gamma$
- $g(\lambda ,\gamma )\leq p^*$,  $\forall \lambda \geq 0$

### Proof1
$$
g(\lambda ,\gamma)  = \inf _{x\in \mathcal{D}} \left[ 
    \alpha (x)+ \lambda ^{T} \beta (x) + \gamma ^{T} \nu (x) \right]
$$

this can be seen as a minimum of affine function, so this is concave

> why is this affine in $\lambda,\gamma$ is x related with them?
> > NoNo this means the minimum of all functions, and each function is affine -> concave

### proof2

let us consider the x feasible
$$
\lambda _{i} f_{i} (x)\leq 0\\
g_{i} (x) = 0
$$

thus 
$$
\mathcal{L}(x,\lambda ,\gamma ) = f_{0} (x)+ \underbrace{\sum_{i=1}^{m}\lambda _{i} f_{i} (x)}_{\leq 0} + \underbrace{\sum_{j=1}^{q} \gamma _{i} g_{i} (x)}_{=0}

\forall \lambda \geq 0
$$



thus 
$$
g(\lambda ,\gamma) = \inf _{x\in \mathcal{D}} \mathcal{L}(x,\lambda ,\gamma) \leq 
\mathcal{L}(x,\lambda ,\gamma) \leq 
f_{0} (x)\\
\forall x \in \mathcal{D} \; \forall \lambda \geq 0 \; \forall \gamma$$

thus 
$$
g(\lambda ,\gamma) \leq \min_{\mathcal{D}}f_{0} (x ) = p^*\\
\forall \lambda \geq 0\; \forall \gamma
$$

> we will talk about duallity gap later

## Dual problem
$$
d^* = \underbrace{\max g(\lambda ,\gamma )}_{\text{dual problem}} \leq \underbrace{\min _{\mathcal{D}} f_{0} (x)}_{prior problem} = p^*\\
\lambda \geq 0
$$

Think as the prior is pushing down, and dual is pushing up

**in general,** there is a **duality gap** $\delta ^{*}$

## strong duality:
$$
\delta ^{*} =0 \qquad p^* = d^*
$$

>老师的祖父上过jordan的课（jordan form）的那个

> 老师之前一直以为 Lagrange is a French mathmatician, 后来才知道是这个是意大利人

## The condition for strong duality
**Constraint qualification**

slata constraints
> slata is germen

consider the convex problem
$$
\min_{x} f_{0} (x)
\\
\text{s.t.}\quad f_{i} (x) \leq 0
\\ Ax = b\\
$$

$$
\exist x \in \text{relative interior}(D) \text{s.t.}\quad  f_{i} (x)<0 \forall i
$$

Note that here the constraint should be **strictly feasible**

Moreover, if $p^* > -\infty$ then the dual optimal value is attained
$$
\exist \lambda ^*, \gamma ^* \quad \text{s.t.}\quad  g(\lambda ^*, \gamma ^*)  = d^*  = q^*
$$


### **relative interia**
$$
\text{Relint}(s) = \left\{x\in S | \exist \epsilon > 0  , B(x,s)\cap \operatorname{affine}(S) \subset S \right\}
$$

The $B$ means a ball

Then strong duality holds $p^* = d^*$

**when the set is convex**

$$
\operatorname{Relint}(C) = \left\{x\in C | \forall y \in C , \exist \lambda > 1 \; \lambda x+(1-\lambda )y\in C \right\}
$$
> this means, that along the line, but outside of the two points.


## example: dual of a LP

for the program:
$$
p^* = \min_{x} c^Tx
\\
\text{s.t.}\quad Ax \leq b
$$

by lagrangine

$$
\mathcal{L}(x,\lambda) = c^Tx + \lambda ^T [Ax-b]\\
g(\lambda) = \inf _{x\in D} \mathcal{L}(x,\lambda )
$$


$$
g(\lambda ) = \left\{\begin{aligned} 
&-\infty & \text{if } c^T + \lambda ^T A \neq 0\\
&-\lambda ^Tb & \text{if } c^T + \lambda ^T A = 0
 \end{aligned}\right. 
$$
> ?? Here $D$ is not the feasible set Otherwise how to we say the unbounded below?

Then the dual problem

$$
\max g(\lambda) \qquad \lambda \geq 0\\
-d^* = \min _{\lambda }(\lambda ^Tb) \\
\text{s.t.}\quad \lambda ^TA + c = 0\\
\lambda \geq 0
$$

this is another LP, we can **take the dual form of the dual.**

$$
\mathcal{d}(\lambda ,\eta ,\gamma ) = b^T\lambda + \eta ^T(-\lambda )+ \gamma ^T(A^T\lambda +c)
$$

lagranginan function

$$
g_d(\eta ,\gamma ) = \inf _{\lambda } \left[ 
    (b^T - \eta ^T + \gamma ^T A^T )\lambda + \gamma ^T c
     \right]
$$

$$
g(\lambda ) = \left\{\begin{aligned} 
&-\infty & \text{if } b^T - \eta ^T + \gamma ^T A^T \neq 0\\
&-\lambda ^Tb & \text{if } b^T - \eta ^T + \gamma ^T A^T = 0
 \end{aligned}\right. 
$$

so the dual of the dual
$$
-dd^* = \max _{v,\eta } c^T\gamma \\
\text{s.t.}\quad b + A \gamma  = \eta \\
\eta \geq 0
$$

the $\eta$ can be treated as slack variable and canceled, and get
$$
\max _{\gamma } c^T \gamma \\
\text{s.t.}\quad b + A \gamma \geq 0 
$$
this is same as let $w = -\gamma$
$$
\min _w c^T w\\
\text{s.t.}\quad Aw \leq b
$$

Thus the Dual of the dual is primal

Then we have 
$$
p^*  = dd^* \leq d^* \leq q^*
$$

thus, it is strong duality


> TODO: Prove it for the QP

# KKT: find the solution for strong duality

consider the optimal solution and assume strong duality

we have 
$$
f_{0} (x^{*})=_\text{S.D.} g(\lambda ^{*} ,\upsilon ^{*} ) =_\text{def} \inf _{x\in  D} L(x, \lambda^{*} ,\upsilon ^{*} )\leq L(x, \lambda^{*} ,\upsilon ^{*} ) \leq_{\text{feasible}} f_{0} (x^{*})
$$

thus the above is all equal

thus $\lambda _{i} ^{*} f_{i} (x^{*} )=0\qquad\forall i$ 

This proposition is called **Complementary slackness**

## KKT
for a problem whose objective and constraints are differentiable 

consider 
$$
\left\{\begin{aligned} 
&x^{*} & \text{primal solution}
\\
&(\lambda ^{*} ,\upsilon ^{*} ) & \text{dual  solution}
 \end{aligned}\right. 
$$

and assume strong duality, then the $x^{*}$ minimizes $\mathcal{L}(x,\lambda ^{*} ,\upsilon ^{*})$

The necessary condition for $f(x)$ to be optimals
$$
\left\{\begin{aligned} 
&f_{i} (x^{*} ) \leq 0 & \forall i=1\dots m\\
&h_{j} (x^{*} ) = 0 & \forall j=1\dots q\\
& \lambda _{i}^{*} \geq 0 & \text{dual variable}\\
& \lambda _{i}^{*} f_{i} (x*) =0  & \text{Complementary  slackness}\\
& \nabla_{x} \mathcal{L}(x^{*} ,\lambda ^{*} ,\upsilon ^{*} ) = 0 & \text{stationary condition}
 \end{aligned}\right. 
$$

> Note that there is no convexity assumption for KKT condition

## Sion's min\max theorem

let $\mathbb{F}: \mathbb{X} \times \mathbb{Y} \rightarrow \mathbb{R}$ be a function s.t.
- $\forall y \in \mathbb{Y}, F(.,y)$ convex over $\mathbb{X}$
- $\forall x \in \mathbb{X}, F(x,.)$ concave over $\mathbb{Y}$

then 
$$
\max _{y} \min _{x} F(x,y) = \min _{x} \max _{y}  F(x,y)
$$
> this is useful to prove strong duality


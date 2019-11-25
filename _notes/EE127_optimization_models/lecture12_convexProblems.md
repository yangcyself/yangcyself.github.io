# CUE
- How to prove a problem is a convex problem? (four steps)
- definition of 
  - unconstraind
  - unbounded below
  - minimizer
  - active constraints
  - optimal set
- give an example where:
  - feasible problem, have optimal value, but the optimal set is empty
- what is the form of introducing slack veriables
- what is the condition for equvalence of substiting the equal constaints to the inequality constraint?


# general optimization problem
$$
\left\{\begin{aligned} &p^* = \min_{x}f_0(x)\\ &s.t. \; f_i(x)\leq 0 \end{aligned}\right. 
$$

> To prove this is a convex optimization problem, prove
> 1. $f_0$ is convex
> 2. Domain($f_0$) is convex
> 3. $f_i$ is convex
> 4. Domain($f_i$) is convex

## Feasible set
$$
\Chi \in \mathcal{Dom}(f_0)\cap(\bigcap_{i=1}^m\mathcal{Dom}(f_i))
$$

example of convex problems
$$
\min c^T x\\
s.t. \qquad \left\|A_ix+b \right\|_2 \leq c_i^T+d
$$

## some notions
**unconstraind**

**minimizer**

if there exists $x^*$  such that $p^* = f(x^*)$, such point is minimizer

Note $x^*$ is not unique in general

**infeasible minimizer is +inf**
(this is convension)

(don't be confused with unbounded below)
if feasible and $p^*=-\infty$ (still feasible but no optimal solution exist)


**Active constraints**

if $x^*\in \mathcal{X}_{\mathrm{opt}}$ and $f_i(x^*)<0$, this constriant is inactive/slack

otherwise $f_i(x^*)=0$ -> active 

**optimal set**

## Theorem: 
consider $\min_{x\in \chi }f_0(x)$, $f_0$ convex, $\chi$ convex, then any local optimal solution is also a global optimization, also $X_{\text{opt}}$ is convex

## exmaple
**feasible problem, have optimal value, but the optimal set is empty**
$$
\begin{array}{cc}{p^{*}=\min _{x \in \mathbb{R}}} & {\mathrm{e}^{-x}} \\ {\text { subject to: }} & {x \geq 0}\end{array}
$$

# Problem transformations:
- monotone transformation of the objective (e.g., scaling, logarithm, squaring) and constraint functions;
- change of variables;
- addition of slack variables;
- epigraphic reformulation; #??
- replacement of equality constraints with inequality ones;
- elimination of inactive constraints;
- discovering hidden convexity;

**equivalent**: same objective value and optimal solutions


## Theorem:

consider
$$
g^* = \min_{x \in R^n} f_0(x)\\
s.t. f_i(x) \leq 0
$$

for a $\phi: \mathbb{R}\rightarrow \mathbb{R}$$ 
strictly increasing over $\mathbb{R}$
then 
$$
g^* = \min_{x \in R^n} \phi (f_0(x))\\
s.t. f_i(x) \leq 0
$$
have the same set of optimal solutions

# introduce slack variable
when the problem is of sum of terms
$$
\begin{array}{rl}{p^{*}=\min _{x}} & {f_{0}(x)=\sum_{i=1}^{r} \varphi_{i}(x)} \\ {\text { s.t. }} & {x \in \mathcal{X}}\end{array}
$$

we can introduce the slack variable
$$
\begin{aligned} g^{*}=\min _{x, t} & \sum_{i=1}^{r} t_{i} \\ \text { s.t. } & x \in \mathcal{X} \\ & \varphi_{i}(x) \leq t_{i} \quad i=1, \ldots, r \end{aligned}
$$


**problems are equivalent in the following sense**

- feasible $\Leftrightarrow$ feasible
- optimal $\Leftrightarrow$ optimal
- g* = p*

**the aim:**    
reformulate into linear objective
$$
\begin{aligned} t^{*}=\min _{x \in \mathbb{R}^{n}, t \in \mathbb{R}} t & \\ \text { subject to: } & f_{i}(x) \leq 0, \quad i=1, \ldots, m \\ & h_{i}(x)=0, \quad i=1, \ldots, q \\ & f_{0}(x) \leq t \end{aligned}
$$
> "referred as epigraphic reformulation

# substituting constraints
not always equal, can change non-convex into convex problem

necessary condition $g^* = p^*$
1. $f_0$ is nonincreasing over $\chi$ i.e. $f_{0}(x) \leq f_{0}(y) \Leftrightarrow x \geq y \text { elementwise }$
2. $b$ is nondecreasing over $\chi$
3. the optimal value p* is attained at some optimal point x* and g* is .... $\tilde{x}^*$

> 直觉很好理解，直接反正

>Note under thess conditions, we have p* = g* and every optimal solution is also the solution of ineq cosntraint one, but **the inverse may not hold**, it holds only if the objective is strictly monotone

# CUE
- Use the lagrange method to do the minimum norm problem
  - min norm(x) s.t. Ax = b
- Use the KKT condition to maxize the entropy
  - H(q) = sum_i (q_i)log(q_i)
# Quick recap duality

min/max property:

$$
\min_x \max_y F(x,y) \geq \max_{y} \min _{x} F(x,y)
$$

primal and dual

$$
\left\{\begin{aligned} 
p^* = \min _{x} f_{0} (x)\\
\text{s.t.}\quad f_{i} \leq 0   \\ h_{i} (x) = 0
 \end{aligned}\right. 
$$

dual 
- info on primal(lower bound)
- always convex
- sometimes can be solved

lagrangian:

$$
\mathcal{L}(x,\lambda ,\upsilon ) f_{0} (x)+ \sum_{i=1}^{m}\lambda _{i} f_{i} (x)+ \sum_{j=1}^{g}\upsilon _{i} h_{i} (x)\\
\lambda _{i} , \upsilon _{j}  \text{ lagrange multipliers}
$$

Lagrangie dual functions

$$
g(\lambda ,\upsilon ) = \inf _{x\in D} \left[ f_{0} (x)+ \sum_{i=1}^{m}\lambda _{i} f   _{i} (x)+ \sum_{j=1}^{g}\upsilon _{i} h_{i} (x)
\right]
$$

propositions 

- $g(\lambda ,\upsilon )$ is concave in $\lambda ,\upsilon$
- $g(\lambda ,\upsilon)\leq p^*$, $\forall \lambda \geq   0,\forall \upsilon$

> pf of the second 
>$$
>g(\lambda ,\upsilon) \leq  \mathcal{L}(x,\lambda ,\upsilon )\leq f_{0} (x) \qquad \forall x \in D, \forall \upsilon \forall \lambda \geq 0
>$$

duality gap

$$
d^* = \max_{\lambda ,\upsilon }g(\lambda ,\upsilon ) \leq \min _{x s.t.} f_{0} (x) = p^*
$$


slata condition

condition 
$$
\left\{\begin{aligned} 
\min _{x\in D}  f_{0} (x)\\
\text{s.t.}\quad f_{i} (x)\leq 0\\
Ax = b\text{Affine}

 \end{aligned}\right. 
$$
if 
$$
\exist x \in \text{relint}(D) \text{s.t.}\quad f_{i}(x)<0 \forall i
$$
then the strong duality holds

furthermore, if
$$
p^* > -\infty, \text{ then the dual optimal value is attend}\\
\exist \lambda^* , \upsilon ^* \text{s.t.}\quad q(\lambda ^*, \upsilon ^*) = d^* = p^*
$$

# minimum norm problem
$$
p^* = \min _{x} \left\|x \right\|_2^{2} \\
\text{s.t.}\quad Ax = b
$$

the lagrange 
$$
\mathcal{L}(x,\upsilon ) = \left\|x \right\|_2 ^{2} +  \upsilon ^{T} (Ax -b)
$$
When computing the lagrange dual function $g$, takes the min over $x$

$$
\mathcal{L}(x,\upsilon ) = x^{T} x + \upsilon^{T}  (Ax-b)
$$

$$
\nabla_{x} \mathcal{L}(x,\upsilon ) = 0\\
2x + A^{T} \upsilon  = 0
$$

because $x^{T}x>0$(strictly pos )  we know that $x^*$ is **unique**

$$
g(\upsilon) = \inf _{x} \mathcal{L}(x,\upsilon)\\
= - \frac{1}{4} \upsilon ^{T} AA^{T} \upsilon - \upsilon ^{T} b
$$
dual problme

$$
d^{*} = \max _{\upsilon } \left[ - \frac{1}{4} \upsilon ^{T} AA^{T} \upsilon - \upsilon ^{T} b \right]
$$

assmme $A$ is full rank, so 
$$
AA^{T} \succ 0
$$
solve the dual problem

$$
\nabla _{\upsilon }  \left[ -\frac{1}{4}\upsilon ^{T} AA^{T} \upsilon - \upsilon ^{T} b  \right]\\
= - \frac{1}{2}AA^{T} \upsilon -  b=0
$$

because A is full rank
$$
\upsilon ^{*}  = -2(AA^{T} )^{-1} b
$$

thus 
$$
d^{*}  = g(\upsilon ^{*} ) = -\frac{1}{4}\upsilon ^{*T}  (AA^{T} )v^{*}  - \upsilon ^{*T} b\\
\dots\\
= b^{T} (AA^T)^{-1} b 
$$

Go Back to the slataio condition

- convex$\sqrt{}$
- only linear constraint$\sqrt{}$
- check the feasibility$\sqrt{}$

Because $A$ is full rank so we have $A\tilde{x} = b$

So we have strong duality and 
$$
p^{*} = d^{*} \\
x^{*}  = -\frac{1}{2}A^{T} v^{*} \\
x^{*}  = A^{T} (AA^{T} )^{-1} b
$$

> if $b$ is not in the range of $A$, $p^{*}$ and $d^{*}$ will be $+\infty$

> TODO: understand slatar condition

## Complementary  slackness, and KKT
primal problem
$$
\left\{\begin{aligned} 
p^* = \min _{x} f_{0} (x)\\
\text{s.t.}\quad f_{i} \leq 0   \\ h_{i} (x) = 0
 \end{aligned}\right. 
$$
and dual
$$
\left\{\begin{aligned} 
d^{*} = \max _{\lambda ,\upsilon }  (g(\lambda ,\upsilon ))\\
\lambda \geq 0

 \end{aligned}\right. 
$$

assume strong duality

assume $x^{*}$ is attained 

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


## example using KKT

for the entropy function
$$
H (x) = - \sum_{i=1}^{n}p_{i} \log (p_{i})
$$
use KKT condition to derie the condition for maximum entropy

$$
\min \sum_{i=1}^{n}p_{i} \log p_{i} \\
\text{s.t.}\quad \sum p_{i} =1, p> 0
$$

we have 
$$
\mathcal{L}(p,\lambda ,\upsilon ) = f_{0} (p) - \lambda ^{T} p+\upsilon (1-1^{T} p) \qquad \lambda >0
$$

The KKT condition is 
$$
\left\{\begin{aligned} 
& p >0 \quad 1^{T} p = 1\\
&\lambda \geq 0\\
&\lambda _{i} p_{i}  = 0 \quad \forall i &\text{Complementary  slackness}\\ 
& \log p_{i} - \lambda _{i} + \upsilon  + 1 = 0 & \text{stationary condition}
 \end{aligned}\right. 
$$

Because $p_{i}>0$, from the Complementary slackness, we conclude $\lambda _{i}=0$. And we see that $p_{i}$ does not depend on $i$, which means that they should be all the same
$$
1^{T} p = 1 \Rightarrow p_{i}^{*} = \frac{1}{n}
$$
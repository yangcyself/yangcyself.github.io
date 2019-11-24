# CUE
- how to understand the definition of eigenvalues:
  - lambda_k = min_{U:dimU=k} max_{x in U} Rayleigh quotient
- the different matrix representing graphs
  - adj
  - laplace
  - normed laplace
- CUT edges and matrix
  - How to represent the cut and count the cut edges
  - How to use Laplace matrix to derive it
  - what is the rank and the smallest eigen vector?
  - what if lambda_k is zero? how is this related to the number of connected components
- bipartite connected components (normed laplacian matrix)
  - derive the function of the rayleigh quotient with normed laplacian
- Spectral Graph Drawing
  - how to represent the spectral graph drawing problem
  - how to choose the embedding of x and y


# define the lambda
## define the rayleigh quotient
$$
R_{M}(x)=\frac{x^{\top} M x}{x^{\top} x}
$$
thus the eigen values
$$
\lambda_{k}=\min _{U : \operatorname{dim} U=k} \max _{x \in U} \frac{x^{\top} M x}{x^{\top} x}
$$
with $\lambda_{1} \leq \lambda_{2} \ldots \lambda_{n}$


## 理解
min_ max的做法是这样的，我给定任意一个空间，我在这个空间里面去找Rayleigh 最大的那一个值。 然后我是通过调整我空间的大小改变我能找到的最大的特征值。

也就是k为一的时候，我就令空间U为最小的特征向量的那个空间，这样得到的结果超不过最小的特征值。如果k等于2，我不得不增加一个维度，只能增加第二个特征值的对应的维度

# Some matrix define
Adjacent matrix

$$
A_{u, v}=\left\{\begin{array}{ll}{1} & {(u, v) \in E} \\ {0} & {\text { otherwise }}\end{array}\right.
$$

D be a diagonal matrix such that $D_{u,v} = deg(v)$

## laplace matrix
$$
L = D - A
$$

## normed laplace matrix
$$
L_{N}=D^{-1 / 2} L D^{-1 / 2}
$$

# CUT edges and matrix

representing a cut(dividing vectexes into different groups)
$$
x_{v}=\left\{\begin{array}{ll}{1} & {v \in S} \\ {0} & {\text { otherwise }}\end{array}\right.
$$

## claim
The numerator of the Rayleigh quotient of x with respect to the Laplacian is exactly **equalled to the number of edges across the cut** $S|V −S$

### proof
$$
\begin{aligned} \partial(V, V-S) &=\sum_{(u, v) \in E}\left(x_{u}-x_{v}\right)^{2} \\ &=\sum_{(u, v) \in E} x_{u}^{2}-2 x_{u} x_{v}+x_{v}^{2} \\ &=\sum_{v \in V} \operatorname{deg}(v) x_{v}^{2}-\sum_{(u, v) \in E} 2 x_{u} x_{v} \\ &=\sum_{v \in V} \operatorname{deg}(v) x_{v}^{2}-\sum_{u} \sum_{v} x_{u} x_{v} * 1\{(u, v) \in E\} \\ &=x^{\top} D x-x^{\top} A x \\ &=x^{\top} L x \end{aligned}
$$

## Theorem
(of the laplacian matrix) If λ1 ≤ λ2 ≤ ...λn are the eigenvalues of L, the λk = 0 iﬀ G has at least k connected components.

### Proof
use the definition of min eigenvalue above

$$
\lambda_{k}=\min _{U : \operatorname{dim} U=k} \max _{x \in U} \frac{x^{\top} L x}{x^{\top} x}
$$

To argue that there exists a space that have k dim and every vector makes zero

# bipartite connected components (normed laplacian matrix)
## theorem
As if I haven’t abused notation enough, let λ1 ≤,...λn be the eigenvalues of LN. λN = 2 iﬀ G has at least one bipartite connected component.

$$
\begin{aligned} \frac{x^{\top} L_{N} x}{x^{\top} x} &=x^{\top}\left(I-\frac{1}{d} A\right) x \\ &=x^{\top} x-\frac{1}{d} x^{\top} A x \\ &=x^{\top} x-\frac{1}{d} \sum_{u} \sum_{v} x_{u} x_{v} 1\{(u, v) \in E\} \\ &=x^{\top} x-\frac{1}{d} \sum_{(u, v) \in E} 2 x_{u} x_{v} \\ &=x^{\top} x-\frac{1}{d} \sum_{(u, v) \in E}\left(x_{u}+x_{v}\right)^{2}-x_{u}^{2}-x_{v}^{2} \\ &=x^{\top} x+\frac{1}{d}\left(\sum_{v \in V} \operatorname{deg}(v) x_{v}^{2}\right)-\frac{1}{d} \sum_{(u, v) \in E}\left(x_{u}+x_{v}\right)^{2} \\ &=2 x^{\top} x-\frac{1}{d} \sum_{(u, v) \in E}\left(x_{u}+x_{v}\right)^{2} \end{aligned}
$$

Thus, we have
$$
\begin{aligned} \lambda_{n} &=\max _{x} \frac{x^{\top} L_{N} x}{x^{\top} x} \\ &=\max _{x} \frac{1}{x^{\top} x}\left(2 x^{\top} x-\frac{1}{d} \sum_{(u, v) \in E}\left(x_{u}+x_{v}\right)^{2}\right) \\ &=2-\min _{x} \frac{\sum_{(u, v) \in E}\left(x_{u}+x_{v}\right)^{2}}{x^{\top} x} \end{aligned}
$$

because x cannot all be zero, we let $A=\left\{v : x_{v}>0\right\} \text { and } B=\left\{v : x_{v}<0\right\}$. Thus for the set that not zero, it must be the two end points belongs to one in A and one in B for edges.  -> a bipartite component


## Spectral Graph Drawing
suppose we want to draw a graph in 2 or 3 dimensions in a way that we can visualize nicely. Ideally, we would want to stretch the edges as little as possible
$$
\begin{aligned} \min _{f} \sum_{u, v \in E}\|f(u)-f(v)\|_{2}^{2} &=\min _{x, y \in \mathbb{R}^{n}} \sum_{u, v \in E}(x(u)-x(v))^{2}+(y(u)-y(v))^{2} \\ &=\min _{x, y} x^{\top} L x+y^{\top} L y \end{aligned}
$$

lambda 最小是全一向量，所以取第二和第三小的向量即可
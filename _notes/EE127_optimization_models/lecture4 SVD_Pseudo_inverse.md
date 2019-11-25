# CUE
- Dyad
  - 如何把两个任意的矩阵相乘表示为dyad的和
- SVD theorem
- prove (A^TA)v = 0 => Av = 0
- In spectral theorem Av = av, in SVD, what is the result of Av, and what is the result of u^TA?
- find from U and V the basis for kernel space and range of $A$ and $A^T$
- How can the febonaci norm, euclidean norm and nuclear norm be represented with SVD
- how to compute condition number
- what is the definition of pseudoinverse
- How to compute Moore-Penrose pseudoinverse
  - Note the position of u and v
- prove that when A is full column rank, then $A^{\dagger} = (A^TA)^{-1}A^T$
- What is the projection matrix on Range A, Range AT, NULL A, NULL A^T
- How to indicates what fraction of the total variance (Frobenius norm) in A is explained by the rank k approximation of A.
- How to compute the distance to rank deficiency
- What is Regularized PCA and what is the closed form of it?

# Takeaway
- 证明SVD的时候的思路是: 从ATA出发, 找到能够 U^TAV = 对角的形式， 然后再逆到等号右边即可
- 证明SVD的相关性质的时候，常把V^TV 或者U^TU消掉， 然后中间的对角矩阵相乘


# Dyad
a matrix can be called Dyad if it can be written as 
$$
A=p q^{\top}, A\in R^{m,n}
$$

**singular value decomposition theorem** states that every matrix can be written as sum of dyads
$$
A=\sum_{i=1}^{r} p_{i} q_{i}^{\top}
$$
for vectors $q_i$ and $p_i$ that are mutually orthogonal

Note 两个矩阵相乘, 左边的看列向量，右边的看行向量的时候
$$
\left[\begin{array}{llll}{\uparrow} & {\uparrow} & {\dots} & {\uparrow} \\ {\mathbf{x}^{1}} & {\mathbf{x}^{2}} & {\dots} & {\mathbf{x}^{n}} \\ {\downarrow} & {\downarrow} & {\cdots} & {\downarrow}\end{array}\right] \left[\begin{array}{c}{\leftarrow \mathbf{x}_{1}^{\top} \rightarrow} \\ {\leftarrow \mathbf{x}_{2}^{\top} \rightarrow} \\ {\vdots} \\ {\leftarrow \mathbf{x}_{n}^{\top} \rightarrow}\end{array}\right] 
$$
这可以表示为
$$
\sum_k x^k x_k^T
$$
**这个和行和列是不是orthogonal无关**

## SVD theorem
$A$ can be factored
$$
A=U \tilde{\Sigma} V^{\top}
$$
$$
\tilde{\Sigma}=\left[\begin{array}{cc}{\Sigma} & {0_{r, n-r}} \\ {0_{m-r, r}} & {0_{m-r, n-r}}\end{array}\right], \quad \Sigma=\operatorname{diag}\left(\sigma_{1}, \ldots, \sigma_{r}\right) \succ 0
$$

Note that here $V\in R^{n,n}$, $U\in R^{m,m}$, all $\sigma>0$

And note satisfies:
$$
A v_{i}=\sigma_{i} u_{i}, \quad u_{i}^{\top} A=\sigma_{i} v_{i}, \quad i=1, \ldots, r
$$

$u$ and $v$ are eigen vectors of $A^TA$ and $AA^T$ respectively.

### A construction Proof
prove by construction

idea & intuition: compute matrix $A^TA$

by spectral theorem, it can be diagonalized $A^TA = U\Lambda V^T$

the eigen vector
$$
A^TAv = \lambda v
$$

Left multiply $A$ get:
$$
AA^T(Av)= \lambda Av
$$

We can get $u$ from $v$, let
$$
u_i = \frac{Av_i}{\sqrt{\lambda}}
$$

Then we can have 

$$
u_i^T A v_i = \sqrt{\lambda}\\
u_i^T A v_j = 0 \quad i\neq j
$$

Then we can construct a diagnal matrix by left Mul U and right Mul V

$$
U^T A V = \Sigma_r
$$

We can extend this from $r$ (rank of A) to m and n, by adding vectors in the NULL space

and we have a little lemma:
$$
(A^TA)v = 0 \Rightarrow Av = 0
$$

so We have

$$
U^T A V = \tilde{\Sigma}
$$

$\tilde{\Sigma}$只有左上角$r*r$是对角，其他都是0


## Matrix properties via SVD
- rank: the cardinality of the nonzero singular values
- the orthonomal basis spanning $\mathcal{N}(A)$ the last n-r columns of V
- the orthomoraml basis spanning of range A is the first r columns of U

### norms
$$
\|A\|_{F}^{2}=\operatorname{trace} A^{\top} A=\sum_{i=1}^{n} \lambda_{i}\left(A^{\top} A\right)=\sum_{i=1}^{n} \sigma_{i}^{2}
$$
- the squared spectral matrix norm is the maximum eigenvalue of $A^TA$

- the nuclear norm is sum of singular values

$$
\|A\|_{*}=\sum_{i=1}^{r} \sigma_{i}, \quad r=\operatorname{rank} A
$$

### Condition number
the ratio between the largest and smallest singular value
$$
\kappa(A)=\frac{\sigma_{1}}{\sigma_{n}}=\|A\|_{2} \cdot\left\|A^{-1}\right\|_{2}
$$

- represents how close A is to being singular
- the sensitivity of the solution of a system of linear equations to changes in the equation coefficients

# Pseudo-inverse
given $A\in R^{m,n}$, a pseudoinverse is:
$$
\begin{aligned} A A^{\dagger} A &=A \\ A^{\dagger} A A^{\dagger} &=A^{\dagger} \\\left(A A^{\dagger}\right)^{\top} &=A A^{\dagger} \\\left(A^{\dagger} A\right)^{\top} &=A^{\dagger} A \end{aligned}
$$

Moore-Penrose pseudoinverse is only a specific pseudoinverse

$$
A^{\dagger}=V \tilde{\Sigma}^{\dagger} U^{\top} \in \mathbb{R}^{n, m}
$$

## special cases
If A is square and nonsingular, then $A^{\dagger}=A^{-1}$

If $A \in R^{m,n}$ is full column rank, that is $r = n leq m$

$$
A^{\dagger} A=V_{r} V_{r}^{\top}=V V^{\top}=I_{n}
$$
That is, $A^{\dagger}$ is a left inverse of A, and it has the explict expression
$$
A^{\dagger}=\left(A^{\top} A\right)^{-1} A^{\top}
$$

similarli:
if A is full row rank
$$
A A^{\dagger}=U_{r} U_{r}^{\top}=U U^{\top}=I_{m}
$$

$$
A^{\dagger}=A^{\top}\left(A A^{\top}\right)^{-1}
$$

# Projectors
Matrix $P_{\mathcal{R}(A)} \doteq A A^{\dagger}=U_{r} U_{r}^{\top}$ is an orthogonal projector onto $\mathcal{R}(A)$

Similarly, $P_{\mathcal{N}\left(A^{\top}\right)} \doteq\left(I_{m}-A A^{\dagger}\right)$ is an orthogonal projector onto $\mathcal{R}(A)^{\perp}$

similarly

$$
P_{\mathcal{N}(A)} \doteq I_{n}-A^{\dagger} A
$$

$$
P_{\mathcal{N}(A)^{\perp}} = P_{\mathcal{R}(A^T)}  \doteq A^{\dagger} A
$$

> use the projector's defn $A A^{\dagger}A A^{\dagger} = A A^{\dagger}$ to prove this is a projector
> and the range of it is just the range of $A$

# Approximation
$$
\eta_{k}=\frac{\left\|A_{k}\right\|_{F}^{2}}{\|A\|_{F}^{2}}=\frac{\sigma_{1}^{2}+\cdots+\sigma_{k}^{2}}{\sigma_{1}^{2}+\cdots+\sigma_{r}^{2}}
$$

indicates what fraction of the total variance (Frobenius norm) in A is explained by the rank k approximation of A.


## the Minimum "distance" to rank deficiency
solve
$$
\begin{array}{cl}{\min _{\delta A \in \mathbb{R}^{m, n}}} & {\|\delta A\|_{F}^{2}} \\ {\text { s.t.: }} & {\operatorname{rank}(A+\delta A)=n-1}\end{array}
$$

$$
\delta A^{*}=-\sigma_{n} u_{n} v_{n}^{\top}
$$

so that the distance to rank deficiency is $\sigma_n$

## Generalized Low-rank models
$$
\min _{L, R}\left\|X-L R^{T}\right\|_{F} : L \in \mathbb{R}^{p \times k}, \quad R \in \mathbb{R}^{m \times k}
$$

把一个$p*m$的矩阵分解成 $p*k$ 和 $m*k$的矩阵, (还记得当时学的推荐系统嘛)

this is the same as
$$
\min _{L, R} \sum_{i, j} \mathcal{L}\left(X_{i j}, l_{i}^{T} r_{j}\right) : l_{i} \in \mathbb{R}^{k}, i=1, \ldots, p, r_{j} \in \mathbb{R}^{k}, j=1, \ldots, m
$$
where 
$$
\mathcal{L}(a, b)=(a-b)^{2}
$$

generalized low-rank model solves:
$$
\min _{I, R} \sum_{i, j} \mathcal{L}\left(X_{i j}, l_{i}^{T} r_{j}\right)+\sum_{i} p_{i}\left(l_{i}\right)+\sum_{j} q_{j}\left(r_{j}\right)
$$


### Regularized PCA
$$
\min _{L, R}\left\|X-L R^{T}\right\|_{F}^{2}+\gamma\left(\|L\|_{F}^{2}+\|R\|_{F}^{2}\right) : L \in \mathbb{R}^{p \times k}, \quad R \in \mathbb{R}^{m \times k}
$$
Closed-form solution:
$$
\begin{array}{l}{\text { Given the SVD of } X=U \Sigma V^{T}, \text { we set }} \\ {\tilde{\Sigma}_{i i}=\max \left(0, \Sigma_{i i}-\gamma\right), \quad i=1, \ldots, k}\end{array}
$$
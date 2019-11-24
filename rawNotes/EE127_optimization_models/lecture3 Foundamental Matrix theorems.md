# CUE
- ellipsoid
- spectral theorem(3)
- Rayleigh quotient
- cholesky decomposition
  - $A =B^2$
- How to compute the matrix Gain of the L2 norm
- PCA and covariance matrix
  - How well is data approximated by its projections on the successive subspaces?
- Cholesky decomposition
- Schur complement theorem
  - what is schur complement?
  - prove why a matrix PSD property is the same as its schur complement?
- QR decomposition
- PSD
  - for a matrix in Rmn, when is A^TA positive definite
  - Eplain why we call PSD set a convex CONE?
  - paritial order $\prec$


## special matrix
**ellipsoid**
$$
\epsilon := \{x|x^TP^{-1}x\leq1 \}
$$
where
$$
P \succ 0
$$

because this is equal with
$$
\{x | x^TA^TAx\leq1\}
$$


**Note:** the long and short axis are the first and second large eigenvalue

## spectral theorem

>Any symmetric matrix is orthogonally similar to a diagonal matrix. This is stated in the following so-called spectral theorem for symmetric matrices.


use this everytime when the matric is symmetric

let $A\in R^{n\times n}$, symmetric, let $\lambda_i$ be eigenvalue of $A$

then there exists a set of orthonomal vector such that 

$$
A = U\Lambda U^T
$$

### theorem 1
Let $A ∈ R^{n,n}$ be symmetric, let $λi ∈ R, i = 1, . . . , n$ be the eigenvalues of A (counting multiplicities). Then, there exist a set of orthonormal vectors ui ∈ $R^n$, i = 1, . . . , n, such that $Au_i$ = $λ_iu_i$. Equivalently, there exist an orthogonal matrix $U = [u1 · · · un]$ (i.e.,UU^T = U^TU = I_n) such that
$$
A=U \Lambda U^{\top}=\sum_{i=1}^{n} \lambda_{i} u_{i} u_{i}^{\top}, \quad \Lambda=\operatorname{diag}\left(\lambda_{1}, \ldots, \lambda_{n}\right)
$$

### Rayleigh quotient. and theorem 2
**Rayleigh quotient**
$$
\frac{x^{\top} A x}{x^{\top} x}
$$
theorem
$$
\lambda_{\min }(A) \leq \frac{x^{\top} A x}{x^{\top} x} \leq \lambda_{\max }(A), \quad \forall x \neq 0
$$

### Matrix Gain
the gain respect to L2 norm is 
$$
\|A\|_{2}=\max _{x \neq 0} \frac{\|A x\|_{2}}{\|x\|_{2}}
$$

therefore 
$$
\|A\|_{2}=\max _{x \neq 0} \frac{\|A x\|_{2}}{\|x\|_{2}}=\sqrt{\lambda_{\max }\left(A^{\top} A\right)}
$$

## About positive definite
A in Rmn
$$
\begin{array}{l}{A^{\top} A \succ 0 \text { if and only if } A \text { is full-column rank, i.e., rank } A=n \text { ; }} \\ {A A^{\top} \succ 0 \text { if and only if } A \text { is full-row rank, i.e., rank } A=m \text { . }}\end{array}
$$


### PSD cone and parital order

## cholesky decomposition
$A=B^2$

this can be got from expand the eigen matrix into the sqrt of its values. And add $U^TU$ in between.


### schur complements theorem
consider the symmetric block matrix
$$
M=\left[\begin{array}{ll}{A} & {X} \\ {X^{\top}} & {B}\end{array}\right]
$$
Let $S \doteq A-X B^{-1} X^{\top}$

then 
$$
M \succeq 0(\text { resp. } M \succ 0) \Leftrightarrow S \succeq 0(\text { resp. } S \succ 0)
$$


### **understanding of schur complement**
$$
\begin{array}{l}{A x+B y=a} \\ {C x+D y=b}\end{array}
$$

thus 
$$
\left(A-B D^{-1} C\right) x=a-B D^{-1} b
$$

## PCA and covariance matric

the convariance matrix is 
$$
\frac{1}{m}\sum_{i=1}^m(u^T(x_0)-u^T\hat{s})^2\\
u^T(\frac{1}{m}\sum^m_{i=1}(x_i-\hat{s})(x_i\hat{s})^T)u
$$


### about the eigenvalues and variance

How well is data approximated by its projections on the successive subspaces?

Explained variance: measured by the ratio

Approach: compare sum of variances contained in the k directions found, with
total variance.

$$
\frac{\lambda_{1}+\ldots+\lambda_{k}}{\lambda_{1}+\ldots+\lambda_{p}}
$$

## QR decomposition
recall the process of Gram-Schmidt([wikipedia](https://en.wikipedia.org/wiki/Gram%E2%80%93Schmidt_process))

$$
\begin{array}{ll}{\mathbf{u}_{1}=\mathbf{v}_{1},} & {\mathbf{e}_{1}=\frac{\mathbf{u}_{1}}{\left\|\mathbf{u}_{1}\right\|}} \\ {\mathbf{u}_{2}=\mathbf{v}_{2}-\operatorname{proj}_{\mathbf{u}_{1}}\left(\mathbf{v}_{2}\right),} & {\mathbf{e}_{2}=\frac{\mathbf{u}_{2}}{\left\|\mathbf{u}_{2}\right\|}} \\ {\mathbf{u}_{3}=\mathbf{v}_{3}-\operatorname{proj}_{\mathbf{u}_{1}}\left(\mathbf{v}_{3}\right)-\operatorname{proj}_{\mathbf{u}_{2}}\left(\mathbf{v}_{3}\right),} & {\mathbf{e}_{3}=\frac{\mathbf{u}_{3}}{\left\|\mathbf{u}_{3}\right\|}} \\ {\mathbf{u}_{4}=\mathbf{v}_{4}-\operatorname{proj}_{\mathbf{u}_{1}}\left(\mathbf{v}_{4}\right)-\operatorname{proj}_{\mathbf{u}_{2}}\left(\mathbf{v}_{4}\right)-\operatorname{proj}_{\mathbf{u}_{3}}\left(\mathbf{v}_{4}\right),} & {\mathbf{e}_{4}=\frac{\mathbf{u}_{4}}{\left\|\mathbf{u}_{4}\right\|}} \\ {\vdots} & {\vdots} \\ {\mathbf{u}_{k}=\mathbf{v}_{k}-\sum_{j=1}^{k-1} \operatorname{proj}_{\mathbf{u}_{j}}\left(\mathbf{v}_{k}\right),} & {\mathbf{e}_{k}=\frac{\mathbf{u}_{k}}{\left\|\mathbf{u}_{k}\right\|}}\end{array}
$$

We can found that 

$$
\begin{array}{ll}{\mathbf{v}_{1}}=\mathbf{u}_{1} \\ 
{\mathbf{v}_{2} = \mathbf{u}_{2}+\operatorname{proj}_{\mathbf{u}_{1}}\left(\mathbf{v}_{2}\right)} 
\\...
\\ {\mathbf{v}_{k}=\mathbf{u}_{k}+\sum_{j=1}^{k-1} \operatorname{proj}_{\mathbf{u}_{j}}\left(\mathbf{v}_{k}\right)} \end{array}
$$

We can use this to construct the upper-triangular matrix $R$.

Thus, we let $v_i$ be the $i$th  column of $A$. And calculate $e_i$ according to Gram-Schmidt. Then 
$$
U = \left[ e_1,e_2...e_n \right]\\
G_{i,j} = \operatorname{proj}_{e_i}(v_j)
$$
Because $v_j$ is only decompose to basis $\{e_i|i<j\}$, thus the matrix $G$ is upper-triangular matrix.

Note If the matrix is not full rank, i.e. there are zero columns in $U$, $G$ is still an upper-triangle matrix.


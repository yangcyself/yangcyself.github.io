this folder contains the knowledge learned from doing homework

## Gaussion
- prove that x is a gaussion $(0,\sigma^2)$, then $\mathbb{E}\left[e^{\lambda X}\right]=e^{\sigma^{2} \lambda^{2} / 2}$

- using Markov’s inequality in combination with the result of the previous part to prove that 
$$
\mathbb{P}(X \geq t) \leq \exp \left(-t^{2} / 2 \sigma^{2}\right)
$$
for $X \sim N\left(0, \sigma^{2}\right)$

- let $X=\left(X_{1}, \ldots, X_{d}\right)$ be a vector of i.i.d gaussians

vectors $u, v \in \mathbb{R}^{d}, u \perp v$

Prove $u_{x}=\langle u, X\rangle$ and $v_{x}=\langle v, X\rangle$ are independent

## Linear Algebra

### How to decompose semi-definite matrix?

[Cholesky_decomposition](https://en.wikipedia.org/wiki/Cholesky_decomposition)

A symetric semipositive matrix can be decomposed as $A = UU^T$ where $U$ are upper or lower triangle.

To compute this, can use the idea similar to 高斯消元


## Covariance
Prove that the covariance matrix is always positive semi-definite.

Hint: Use linearity of expectation.
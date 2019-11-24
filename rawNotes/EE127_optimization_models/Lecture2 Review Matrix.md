# CUE
- why is determinant the product of eigen values?
- when the trace of a matrix equal to the summantion of eigenvalues?
- The eigenalizable condition?
- matrix norms

## matrix is a transformation from one space to another space
### transformation and package matrics
P is a package matrix from A to B iff $B=P^{-1}AP$

## Foundaional Theorem of diagonalizibility
- charastic polynomial
- the Null space dim of eigen vector of one eigenvalue is less than or equal to the eigenvalue multiplicity
- if $\nu_i=\mu_i$ for all eigenvalues, then the matrix is eigenalizable

$$
A = U \Lambda U^{-1}
$$

## Matrix norms

### F norm
$$
\|A\|_F = \sqrt{trace(AA^T)} = (\sum_{ij}|A_i|^2)^{\frac{1}{2}}
$$
it satisfies the properties of norm


also because:

**if A is symmetric, then the trace is the sumation of eigenvalues**

it can be written as:

$$
\|A\|_F = \sqrt{\sum_i\lambda_i(AA^T)}
$$

### P norm
$$
\|A\|_p = \max_u \frac{\|Au\|_p}{\|u\|_p} = \max_{\|u\|_p=1} \|Au\|_p
$$

determinant is the product of eigen values
why?


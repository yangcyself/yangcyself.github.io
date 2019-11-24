# CUE
- the set solution of LS problem can be expressed as (?+Nx), where N is the null space
- how to express the following problem as classical least square?
  - weight LS
  - regularized 
  - Auto regression
  - kernel trick?
# 小故事

一个fecalty 不知道怎么提到他的， 可能算是提出了
$$
\min \eta = \sum_{t=0}^T\text{cost }t\\
\text{s.t. }X_{t+1}  =A_{x_t}+Bu_t
$$
后来这个人对抗癌症，也算是一种最优，cost代表期望寿命

## corollary

the set of solutions of LS problem
$$
p^* = \min_x \left\|Ax-y \right\|_2 
$$
can be expressed as 
$$
A^\dagger y + \mathcal{N}(A)z
$$

## other kinds of least squares
### weighted LS
can be changed into
$$
\min \left\|AWx - yW \right\|_2^2 
$$
note that $W$ is diag(w_1,...w_n)
### Regularized least squares
how to reform this into a classical least square?
$$
\left\|\left[\begin{array}c A\\\sqrt{\lambda}I_n \end{array}\right] x - \left[\begin{array}c y \\ 0_n \end{array}\right]  \right\|_2^2 
$$

### Auto regressive model
ARmodel

$$
y_k = w_1y_{k-1}+ ... + w_n y_{k-n} + e_k
$$
this is a predictive model

### kernel trick
feature vectors
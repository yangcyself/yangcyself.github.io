# CUE
- 回忆当时课上做的实验，全班同学选过的课进行PCA，第一个维度是什么
- How to solve Ax = b via SVD method
# CUE的答案
我记得第一个维度把研究生和本科生分成了两类，特征向量是本科生+本科生得课，也就是说，相关性高得东西，会被PCA聚到一起

# Linear equations
$$
Ax=b
$$

$S = \{x|x = \bar{x}+N_z\}$
约定$\bar{x}\in\mathcal{R}A^T$

# Solve this via SVD

$$
U\tilde \Sigma V^T x = y \\
\tilde \Sigma V^T x = U^Ty \\
$$

denote $V^Tx$ as $\tilde{x}$

denote $U^Ty$ as $\tilde{y}$

then $\tilde{x_i} = \frac{\tilde{y_i}}{\sigma_i}$

所以求解的过程:
- SVD A
- complete ui
- $\tilde{x_i} = \frac{\tilde{y_i}}{\sigma_i}$
- go back to complete x

**注意： 第三步记得验证有解**
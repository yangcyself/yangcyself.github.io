# CUE
- 手推pesudo inverse construction
- 对比SVD以及EVD的性质
- 
# review
compact form SVD
$$
A = \sum_{i=1}^r \sigma_i u_i v_i^T =  U_r \Sigma V_r^T \\
Av_i = \sigma_i u_i\quad u_i^TA  = \sigma_iu_i
$$

老师今天手推了**pesudo inverse construction**, 我觉得不用赘述了

# insight recap
## SVD vs. EVD
什么时候用SVD什么时候用EVD？

如果矩阵是对称方阵，就用EVD，否则用SVD

回想PCA， 我们研究PCA的协方差矩阵的时候，$X^TX$是一个半正定对称阵，这个时候就可以使用EVD

同样，如果直接对数据矩阵进行处理，可以直接用SVD
# CUE
- prove the theorem that big-step semantics and the denotational semanttic are equivalent

# prove the theorem that big-step semantics and the denotational semanttic are equivalent
-> direction

**the WHILE COMMAND**

if we have a derivation D: that (D1: b,\sigma -> true), (D2: c,\sigma -> sigma1), (D1: while b do c ,sigma1 -> sigma')\over while b do c sigma -> sigma'

from the hypothesis of D1, D2, D3 we can get $B\llbracket b \rrbracket = true$ and $C\llbracket c \rrbracket\sigma = \sigma_1 \neq \perp$ and from D3 we get $W(\sigma_1)=\sigma '\neq \perp$ -> there exists a smallest k

通过这个smallest k我们可以说明两件事:
- 可以终止
- 最后可以得到结果$\sigma'$


<- direction

仍然研究WHILE的证明

这里面一个很重要的思想是找到按照什么迭代， 实际上是按照 $W_k$ 从 k=0往上迭代， 证明给定一个denotational semantics 之后可以得到凑出一棵树
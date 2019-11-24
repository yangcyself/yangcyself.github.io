# CUE
- why does mathematical induction work
- use induction to prove that when $\sigma(x)\leq6$, $\langle\text{while} x \leq 5 \text{do} x:=x+1 ,\sigma\rangle \Downarrow \sigma[x:=\sigma]$
- Prove deterministic for expression
- Prove deterministic for command

# Induction
## why does mathematical induction work
There are no infinite descending chains. It has to stop somewhere

## Example
use induction to prove that when $\sigma(x)\leq6$, $\langle\text{while} x \leq 5 \text{do} x:=1 ,\sigma\rangle \Downarrow \sigma[x:=\sigma]$


proof:

let $\sigma_i(i\geq0)$ represent $\sigma[x]=6-i$

Base case when i = 0

/*:
$$
{{{\sigma_0(x)=6}\over{\langle x,\sigma_0 \rangle \Downarrow 6}}
\langle 6\leq5,\sigma_0 \rangle  \Downarrow \text{false}}
\over{\langle x\leq 5 ,\sigma_0 \rangle \Downarrow \text{false}
\over \langle \text{while} x\leq5 \text{do}x:=1+1,\sigma_0 \rangle \Downarrow\sigma_0}
$$
*/

Induction step

$$
\forall i\in N, \langle w,\sigma_i \rangle \Downarrow \sigma_0 \Rightarrow \langle w,\sigma_{i+1} \rangle \Downarrow \sigma_0
$$

## well founded relation

> the structure inductions can work almost the same with (small/big) semantics

## Another example, proof of deterministic
证明如果输入的程序一样，程序状态一样，那么结果一样
- Proof for experssion
  - prove $P(e)$ for any expression e
- Proof for command
  - Prove $P(D)$ for any derivation D
  - 一个derivation是: 我有一个程序， 存在一个证明的树（如同上例）可以证明。
    - 然后可以说这些树形成更大的树也能够证明，只是多了一层

### prove that there is a tree D
$$
D::{
    D1::\langle b,\sigma \rangle \Downarrow True, D_2 :: \langle c,\sigma \rangle \Downarrow \sigma_1 , D_3:: \langle \text{while b do c},\sigma \rangle \Downarrow \sigma'
    \over
    \langle \text{while b do c},\sigma \rangle \Downarrow \sigma'
}
$$

## Q\A
- 为什么我们没有说明我们的所有command有一个partial order?

原因是我们command的定义过程，就是这样树状生成的，所以自带partial order

- 有人问： 这里面是对所有的expression 或者 command递归，那么如果递归的是rules? 可以嘛？

忘了老师什么回答了，
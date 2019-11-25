# CUE
- basic form of denotational semantics
- rules for $A_{exp}$
- rules for denotational Command
- How to define whlie command in a uncompositioned manner
# denotational semantics

**Also called**
- fixed-point semantic
- mathematic semantic
- (一个人名)semantic

rough idea of denotational semantics

A[·]:Aexp -> ($\Sigma$->Z)
$$
A \llbracket . \rrbracket : A_{\text{exp}} \rightarrow (\Sigma \rightarrow Z)
$$

A: the arithmetic expression
exp: the expression in programming language
$\Sigma \rightarrow Z$: Map from current program state to an integer

也就是说:

A作为一个函数， 输入一个程序，输出一个函数：这个函数输入一个program state， 输出一个结果

$$
A\llbracket e_1+e_2 \rrbracket\sigma = A\llbracket e_1 \rrbracket\sigma \mathbf{+}A\llbracket e_2 \rrbracket\sigma
$$

### Define command
$$
C\llbracket . \rrbracket: C_{\text{com}} \rightarrow (\Sigma \rightarrow \Sigma)
$$

This is from a program state to another program state

**Here we introduce a special element $\perp$ called bottom**  meaning non-termination


we have the following rules:

$$
C\llbracket skip \rrbracket\sigma = \sigma\\
C\llbracket x:=e \rrbracket]\sigma = \sigma[x:A\llbracket e \rrbracket\sigma]\\
C\llbracket c_1;c_2 \rrbracket = C\llbracket c_2 \rrbracket(C\llbracket c_1 \rrbracket\sigma)\\
$$
if then else 也很容易推出

## 解决While
先定义一个while_k 和 forever

let $W_k$ be shorthand for $C\llbracket \text{whilek b do c} \rrbracket$

W_k 代表可以在k轮循环之内结束，否则forever

define :
-  W_0(sigma) is bottom state
-  for k >=0 $w_k(\sigma)$ if B[b]$\sigma$ then $W_{k-1}(C\llbracket c \rrbracket \sigma)$ else $\sigma$
   -  Here 如果k-1是non-terminal的话wk也是non terminal


这样我们就可以定义while了
$$
W(\sigma) = \left\{ 
    \begin{aligned}
        \perp \;\;\;& \text{if}   \forall k, W_k(\sigma) = \perp\\
        W_k(\sigma)\quad& \text{k is the smallest such that} W_k(\sigma)\neq \perp
    \end{aligned}
     \right.
$$

**Domain theory will build the mathematical foundations of high order functions**

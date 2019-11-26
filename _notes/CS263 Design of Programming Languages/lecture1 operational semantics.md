---
# collection: notes
title: lecture1 operational semantics
order: 2
---

This is a description of lecture1 operational semantics.


# CUE
- concrete and abstract syntax 
- big-step-operational semantics
  - expression and commands rules
  - rules for inference
  - how to read thess rules
  - while command
  - syntax directed
  - two disadvantages
- small step memantics
- discussion between them
  - 各自用处
- contextual semantics
  - redex
  - H[r]
  - Decomposition teorem
  - Can while loop be redex?


# concrete and abstract syntax
concrete syntax -> conctetely how you type

abstract syntax -> how to represent parse tree

for the language IMP,

which consists 
- expression
  - no side effect
- commands
  - all about side effect
  - assign value, print...
# big-step-operational semantics
## expresssion
$$
<e,\sigma> \Downarrow n
$$
means expression $e$ yield result $n$ given the *program state* $\sigma$

### rules for inference
evaluation rules
$$
 \over <n,\sigma>\Downarrow n
$$

add rules
$$
<e_1,\sigma>\Downarrow n_1 <e_2,\sigma>\Downarrow n_2
\over
<e_1+e_2,\sigma>\Downarrow n_1+n_2
$$

### how to read thess rules
- forward -> implies
- backwards -> how to evaluate the result for the interpreter

## commands
$<c,\sigma>\Downarrow \sigma'$
means the program state changes after the command

### rules for inference
**assign command**

$$
<e,\sigma>\Downarrow n
\over
<\text{x:=e},\sigma>\Downarrow \sigma[x:=n]
$$

Note here we define 
$$
\sigma[x:=n] \;\;\;(x)=n\;\;\;(y) = \sigma(y)
$$

**sequence command**
$$
<c_1,\sigma_1>\Downarrow \sigma_2 \quad <c_2,\sigma_2>\Downarrow \sigma_3
\over
<\text{c1;c2},\sigma_1>\Downarrow \sigma_3
$$


this means the n is looked up first.

**sequence rule**
$$
<c_1,\sigma_1>\Downarrow \sigma_2 \quad <c_2,\sigma_2>\Downarrow \sigma_3
\over
<\text{c1;c2},\sigma_1>\Downarrow \sigma_3
$$

**一个比较有意思的是 while command**

$$
{\langle b,\sigma \rangle \Downarrow False
\over
\langle \text{while b Do c}, \sigma \rangle  \Downarrow \sigma}
$$
means do nothing

$$
\langle b,\sigma \rangle \Downarrow True,  \langle \text{c},\sigma \rangle\Downarrow \sigma'' , \langle \text{ while b Do c}, \sigma'' \rangle \Downarrow \sigma'
\over
\langle \text{while b do c}, \sigma \rangle  \Downarrow \sigma'
$$
## *syntax directed*
syntax directed 的概念就是这个规则可以用来指到 operational syntax。 其它的rule都是syntax directred的， 因为直接在语法树里面找模式匹配，然后替换就可以一点一点解释到底

但是 while的规则就不行，因为这个一个是展开会没完，再一个是条件里面隐含一个假设是while会结束，但是如果不会结束的话，while不可能有上面的条件

### disadvantags of big step semantix
- it is hard to talk about commands whose evaluation does not terminate
- it does not give us a way to talk about intermediate states

## small step memantics
sequance: atomic execution step

$$
<c,\sigma> \rightarrow <c',\sigma'>
$$

## discussion
- small step can guide an interpreter
- big-step can prove some property

example of while
$$
\over <\text{while b do c},\sigma> \rightarrow 
<\text{if b then c; while b do c else skip},\sigma>
$$ 

Note: this rule does not assume termination

We do not evaluate the bollean condition before rewrite the program


## contextual semantics

### redex: 
expression or command that can be reduced in one atomic step

### General idea of contextual semantics

区分H: contex 和 redex: expression to be reduced

通常写作 H[r]，表示r存在在H里面

**Decomposition theorem**

if c is not "skip" then there exist unique H&r such that c is H[r]


Note: 

while loop cannot be a redex, we always reduce the body

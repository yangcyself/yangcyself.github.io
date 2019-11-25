# CUE
- what is the idea of proving completeness?
- what are the two properties that the weakest precondition should have?
- is it enough to say that this is totally complete? what assumption do we need? is there any theorem against it? If it is, what is this kind of completeness called?
- How to define the weakest precondition on Loops?
- what is the rule for verificational semantics?
- How to model the state of memory?
- solve A: `{A} *x := 5 { *x + *y = 10 }`
# completeness of the axiomic semantics
### **good news:** 
for our language the Hoare triple are complete

### **bad news:** 
this is true only if the underlying logic is complete:

whenever $\vDash A$ we have $\vdash A$

we call this **relative completeness**

because we have *Gödel's completeness theorem*

## the Idea for proving the completeness
Find out all predicates $A'$, such that $\vDash \left\{A' \right\}c\left\{B \right\}$ we call this $\text{pre}(c,B)$

prove that $A\in \text{pre}(c,B)$

that is, **Find the weakest precondition**

### Formaly
completeness of axiomatic semantics is :
$$
\text { If } \vDash\{A\} c\{B\} \text { then }\vdash\{A\} c\{B\}
$$

**the wp we find should have the following properties:**
wp is the weakest precondition
$$
\text { If } \vDash\{A\} c\{B\} \text { then } \vDash A \Rightarrow w p(c, B)
$$
wp can be derived by hoare rules
$$
\vdash \{w p(c, B)\} c\{B\}
$$
then 
$$
\vdash A \Rightarrow w p(c, B)\vdash \{w p(c, B)\} c\{B\} \over \vdash \{A\} c\{B\}
$$

but we also need whenever $\vDash A$ then $\vdash A$

### 我的理解
我们想要说明，对于任意一个$\vDash\{A\} c\{B\}$, 都存在一个使用hoare triple的证明$\vdash\{A\} c\{B\}$

为了找到"对于任意的一个$\vDash\{A\} c\{B\}$", 我们去找weakest precondition, 然后我们说任何更弱一些的都是错的，然后这个weakest precondition 仍然能用我们的hoare triple证明出来，这样的话，所有对的$\vDash\{A\} c\{B\}$就都能被证明了

- wp is the weakest precondition
  - $\text{If} \vDash\{A\} c\{B\} \quad \text { then } \vDash A \Rightarrow w p(c, B)$
- wp is the precondition (according to hoare rules)
  - $\vdash\{w p(c, B)\} c\{B\}$
# Find wp inductively on c
**sequence**
$$
\frac{\{A\} c_{1}\{C\}}{\{A\} c_{1} ; c_{2}\{B\}}
$$
wp(c1; c2, B) = wp(c1, wp(c2, B))

**assign**
$$
\{[e / x] B\} x:=e\{B\}
$$
wp(x:=e, B)=[e / x] B

**if then else**
$$
\frac{\left\{A_{1}\right\} c_{1}\{B\} \left\{A_{2}\right\} c_{2}\{B\}}{\left\{E \Rightarrow A_{1} \wedge-E \Rightarrow A_{2}\right\} \text { if } E \text { then } c_{1} \text { else } c_{2}\{B\}}
$$

wp(if E then c1else c2, B) = E ⇒wp(c1, B) ∧¬E ⇒wp(c2, B)

## weakest precondition for loops
from operational semantics

while b do c    =  if b then (c; while b do c) else skip

we have:
$$
W=(b \Rightarrow w p(c, W)) \wedge(\neg b \Rightarrow B)
$$

where $W$ is the weakest precondition wp(w,B), 
w is the while command `while b do c`

这样就遇到了和denotational semantics一样的问题：
W有一个递归的表达式，而这个不像那种方程一样可以解出来

所以和denotational semantics一样的解决方法:
**Finite approximations**

定义 $\sigma \vDash W_{k}$ 的意思是: the execution of while in state srequires at least k iterations of the body, or it terminates in fewerthan k iterations in a final state that satisfies B (**i.e not terminate or satisfy B**)

thus:
$$
\begin{array}{l}{-W_{0} \equiv \text { true }} \\ {-W_{1} \equiv b \Rightarrow w p(c, \text { true }) \wedge-b \Rightarrow B} \\ {-W_{k} \equiv b \Rightarrow w p\left(c, W_{k-1}\right) \wedge-b \Rightarrow B}\end{array}
$$

### properties
$$
W_{k} \Rightarrow W_{k-1}
$$

monotonicity lemma:
$$
\text { If } \vDash B \Rightarrow B^{\prime} \text { then } \vDash w p(c, B) \Rightarrow w p\left(c, B^{\prime}\right)
$$

### then we can define W

$$
W=\land_{k \geq 0} W_{k}
$$

Can $\land_{k \geq 0} W_{k}$be expressed in our language of assertions?•In many cases yes (see Winskel); we’ll assume yes for now

# Verification conditions
WPs are impossible to compute (in general)

construct a verification condition: vc(c, B)

The loops are annotated with loop invariants

while construct includes an invariant

$$
\text{while}_{I} \text{b do c}
$$

The invariant formula must hold every time **before** b is evaluated

then 

$$
\begin{array}{c}{VC(\text { while } e \text { do } c, B)=} \\ {\quad I \wedge\left(\forall x_{1}, \ldots,x_n. I \Rightarrow(e \Rightarrow V C(c, I) \wedge \neg e \Rightarrow B)\right)}\end{array}
$$

x1, ..., xn are all the variables modified in c 

### 我的理解
no matter how x1--xn are modified, as long as ti satisfies the invariant, then xxxx follows

$e \Rightarrow VC(c,I)$是因为还要去循环下一次，所以执行结束的条件应该是I


# Hoare rules handling the Mutable reference
example:
`{ A } *x = 5 { *x + *y = 10 }`

这个使用目前的逻辑系统只能有`*y = 5` 但是其实还能`y=x`

## solve the problem

Model the state of memory as a symbolic mapping from addresses to values:


- **sel(M,E)**: denotes the contents of the memory cell  E
- **upd(M,E,V)**: denotes a new memory state obtained from Mby writing Vat address E
- where E denotes an address and M a memory state 

then the memory access rule:
$$
\operatorname{sel}\left(\operatorname{upd}\left(M, E_{1}, E_{2}\right), E_{3}\right)=\left\{\begin{array}{ll}{E_{2}} & {\text { if } E_{1}=E_{3}} \\ {\operatorname{sel}\left(M, E_{3}\right)} & {\text { if } E_{1} \neq E_{3}}\end{array}\right.
$$


### example:
{ A } *x := 5 { *x + *y = 10 }

then 

- A = [upd(μ, x, 5)/μ] (*x + *y = 10)
- = [upd(μ, x, 5)/μ] (sel(μ, x) + sel(μ, y) = 10)
- = sel(upd(μ, x, 5), x) + sel(upd(μ, x, 5), y) = 10(*)
- = 5 + sel(upd(μ, x, 5), y) = 10
- = if x = y then 5 + 5 = 10 else 5 + sel(μ, y) = 10
- = x = y or *y = 5


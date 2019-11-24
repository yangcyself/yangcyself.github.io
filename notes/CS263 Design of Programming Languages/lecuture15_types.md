# CUE
- explain why type system can help compiler to generate better codes?
- Write the formal expression of types
- what is the difference between dynamic semantics and static semantics of type?
- what is the soundness of that?
- write the syntax rules for F1
- write the type rules for F1
- Prove the soundness of it.
# types

A type is a description of a range of values

for type define *valid operations*, types are **closed** under valid operations

> here the **close** means under solid operation system, you input sth that is typed, you will get sth that is typed

> python has a version that is typed, and FB has found that after introducing typed python, the code commited with python increased.

type systems can be 
- dynamic
- static


> JVM type system is both dynamic and static

### type system can help compiler to generate better code

for example when you `x+y`

Compiler have to call different routines `addi` or `addf`, according to the type of `x` and `y`. If you don't have a type system, then it has to check it at run time.

> Monkey-patching: load methods at run time

# Formalizing a Type System

- syntax
  - Of expressions (programs)
  - Of types
  - issues of binding and scoping
- static semantics (type rules)
- dynamic semantics (operational)
- type soundness
  - is also called type preservation

## typing judgements

> here everything is just like that in axiomatic semantics


- truth value $\vDash J$
- derivation $\vdash J$


common form of judgement
$$
\Gamma \vdash e: \tau
$$

here $\Gamma$ is the typing context. It stores all type expressions
$$
\Gamma::=\emptyset | \Gamma, x: \tau
$$

the expression means, under this typing context $\Gamma$, we can derive the conclusion that $e$'s type is $\tau$

### typing rules
$$
\over \Gamma \vdash 1: \text { int }
$$
$$
\begin{array}{l}{x: \tau \in \Gamma}  \\\hline {\Gamma \vdash x: \tau}\end{array}
$$
$$
\frac{\Gamma \vdash e_{1}: \text { int } \quad \Gamma \vdash e_{2}: \text { int }}{\Gamma \vdash e_{1}+e_{2}: \text { int }}
$$

with this we have 
- type checking
- type inference

## Soundness

### define a value to have a type
$$
v \in \left\|\tau  \right\| 
$$

e.g. $5 \in \left\|\text{int} \right\|$

### define an expression to have a type

$$
e \in |\tau | \text{ iff } \forall  v (e \Downarrow v) v\in \left\|\tau  \right\| 
$$

### Then the soundness is
$$
\emptyset \vdash \text {e: } \tau \text { then } e \in|\tau|
$$

# first order type systems
first order type system means: **no type variables**

> a counter example for is is Template in C++

second-order type systems has 
- polymorphism
- abstract types

## simply typed lambda calculus

> this is so well studied that it is called F1

### syntax
just lambda calculus, but note this is annotated

$$
\begin{aligned}
    e ::=& x &| \lambda x:\tau .e &|e_{1} e_{2} \\
    &|n &| e_{1} + e_{2} &| \text{iszero} e\\
    &| \text{ture}&|\text{false} &|\text{not} e &| \text{if then else}

\end{aligned}
$$

**type**
$$
\tau ::= \text{int} | \text{bool} | \tau _{1} \rightarrow \tau _{2} 
$$

typing rules
$$
\frac{\Gamma, x: \tau \vdash e: \tau^{\prime}}{\Gamma \vdash \lambda x: \tau . e: \tau \rightarrow \tau^{\prime}}
$$

$$
\frac{\Gamma \vdash e_{1}: \tau_{2} \rightarrow \tau \quad \Gamma \vdash e_{2}: \tau_{2}}{\Gamma \vdash e_{1} e_{2}: \tau}
$$

## Prove the soundness

induction on the process of evaluation $e \Downarrow v$

# CUE
- **PCF** 
- typed lambda calculus
  - how to write typed lambda calculus
  - bound and free variables, close
  - How $(\lambda x : \sigma . \lambda y : \tau . \lambda z : \rho . M) N P Q$ is interpreted
- equivalence
  - alpha equivalence
  - beta equivalence
  - other axioms(3 in total)
- operational semantics
  - confluence 
  - termination
- Set-theoretic Background
  - cartesian product
  - ordered pair
  - defining the cartesian product using only set-theoretic operations
  - power set
- set definition of relations and functions
  - relations
    - reflexive
    - symmetric
    - Transitive
    - Antisymmetric
    - total order
    - partial order
  - function
    - partial function
    - set interpretation of function composition
- inductions
  - natural number induction
  - structural induction
  - induction on proofs
  - well founded induction
    - well founded relation
    - proposition (well founded induction)

In this book, we will study programming language concepts using the framework of typed lambda calculus.

**PCF**:  programming computable functions
>It can be considered to be an extended version of the typed lambda calculus or a simplified version of modern typed functional languages such as ML or Haskell. --WIKI

# Lambda Notation
primary features: lambda abstraction

### typed lambda calculus
$\lambda x:\gamma$
mapping any x in $\gamma$ to the value given by M

example
$\lambda x : nat.x$
nat is type of natural numbers

## alpha equivalent and binding operator
in the lambda function
$\lambda x: nat. x+1$
x is only a placeholder.

terms that differ only in the names of bound variables are called alpha-equivalent.
$M=_{\alpha} N$

When a varibale x occurs in an expression M, we say an occurence of x is *bound* if it is inside a subexpression of the form $\lambda x :\gamma.N$ and *free* otherwise [](\\?这个意思是如果x在别的地方被作为函数的参数用到了，是函数对外界的接口，所以叫bound)

$FV(M)$ the set of free variables of M

*close* if the expression has no free variables.[](//?M 是 1算不算close?)

**when apply the function**
function application just by putting a function expression next to one or more arguments.
$(\lambda x: nat x)3.$ 
就是把3带入进去

### notational conventions


- associates to the left 
  - $M\; N \;P$ is $(MN)P$ M is a function that returns a functions
- the scope of lambda is as large as possible
  - $\lambda x: \gamma MN$ is regarded as $\lambda x: \gamma (MN)$

thus, example:
$$ (\lambda x : \sigma . \lambda y : \tau . \lambda z : \rho . M) N P Q $$

is regarded as :

$$ (((\lambda x : \sigma .(\lambda y : \tau .(\lambda z : \rho . M)))) N) Q $$

# equations reduction and semantics
in addition to syntax, there are three main parts of the formal system
- axiomatic semantics
- operational semantics
- denotational semantics
  - similar to model throries of other logical systems
  - such as equational logic or first order logic
  - a model consists of a family of sets, one for each type, with the property that each well-typed expression may be interpreted as a specific elementof the approopriate set.


the first two: "proof systmes", third "model theory"

## axiomatic semantics
**axiom** for renaming bound variables
$[N/x]M$ substituting expression N for variable $x$ in M

$$ \lambda x : \sigma . M=\lambda y : \sigma .[y / x] M, \quad y \text { not free in } M $$
[](//??我觉得应该是y is free in M 啊//II 是这样的, free variable是不能替换的符号一般在外面别的地方定义,比如常数,或者其他的函数$f$. 所以只有bound variable是一个函数和外界的接口)

**beta-equivalence**
$$ (\lambda x : \sigma . M) N=[N / x] M $$
evaluate a function application

**other axioms**
- symmetry [c](书上并没说这是啥意思)
- transitivity
- congruence rule

**congruence rule**
$$ \frac{M_{1}=M_{2}, \quad N_{1}=N_{2}}{M_{1} N_{1}=M_{2} N_{2}} $$

## Operational semantics
**reduction rules**: equational reasoning

the central erduction rule is a directed version of beta-reduction
$$ (\lambda x : \sigma . M) N \stackrel{\beta}{\rightarrow}[N / x] M $$

the entire reduction system:
- beta reduction
- other basic one-stem refuctions
  - evaluate parts of a term
  - repeat reduction steps

### two notable properties of reduction
#### **church-rosser** property
also called *confluence*

if $M \Rightarrow N$ (书上的right arrow是一个横线上两个向右的箭头, 代表多次reduction之后的可以得到的结果) and $M \Rightarrow N'$

then there exists P such that $N \Rightarrow P$ and $N' \Rightarrow P$

this can establishing the sonsistency of the equational proof system
#### strong normalization property
also called *termination*

we cannot go on applying single-step reductions indefinitely[](//??我觉的是infinitely)

But in PCF, we add **recursion** -> can nonterminating 

## denotational semantics
each type expreession is associated with a set, called the set of values of this type

>pure typed lambda calculus is relatively simple
but when it comres to recursive functions,  recursive of types, and polymorphic functions .....

### exercis 1.3.1
$$ (\lambda f : n a t \rightarrow \text { nat. } f 5) (\lambda x : n a t, x+x) $$ 
function can be used in substitution in beta equivalence

[c](//??exercise 1.3.2我不会做..如果M里面有f,我觉得我可以延长,但是否则我只能简单地代换一下) 

# Types and type systems
In any type system, types provide a division or classification of some universe of possible values: 

distinguish *types* and *values*(members of types) 
>in some systems, there may be types with types as members, ... usually called something else, to avoid the impression of circularity

>None of the systems we consider in depth will have a type of all types

some advantages of compile-time type checking are:
- early detection of errors
- Documentation
- Guarantee validity of optimizations

>**Predicting run-time type errors is an undecidable property of programs**

a type of languages called statically-typed

we could use a type *untyped* for all the untyped expressions of a language


# Notation and Methematical convensions
P19

X Cartesian product

# Set-theoretic Background
> In some way, set theory is the "machine language" of mathematics.
cartesian product

$$ \langle a, b\rangle \in A \times B \quad \text { iff } \quad a \in A \text { and } b \in B $$

define ordered pair
$$ \langle a, b\rangle \stackrel{\text { def }}{=}\{\{a\},\{a, b\}\} $$

we can define the first element:
$\text { fst } p=a \text { iff }\{a\} \in p$

defining the cartesian product using only set-theoretic operations
$$ A \times B \stackrel{\text { def }}{=}\{\langle a, b\rangle \in \mathcal{P}(\mathcal{P}(A \cup B)) | a \in A \text { and } b \in B\} $$
where P is the power set

## Relations and Functions
Formally, a relation R between sets A and B is a subset $R \subset A*b$

A relation $R \subset A * A$is 
- **reflexive** if R(a,a) for a in A
- **symmetric** if R(a,b) implies R(b,a)
- **Transitive** if...
- **Antisymmetric**  if R(a,b) and R(b,a) then a==b
- **total order** For all a,b either R(a,b) or R(b,a)
- **partial order** reflexive, antisymmetric and transitive
  
### function
A function is identified with its *graph* 

function A->B is relation $f\Subset A *B$ such that:
- $\forall a \in A . \exists b \in B .\langle a, b\rangle \in f$
- $\forall a \in A . \forall b, b^{\prime} \in B . \text { if }\langle a, b\rangle \in f \text { and }\left\langle a, b^{\prime}\right\rangle \in f \text { then } b=b^{\prime}$

**parital function** $f : A \rightarrow B$ satisfying the property ii but not the property i

**function composition**

$$ S \circ R \stackrel{\text { def }}{=}\{\langle a, c\rangle \in A \times C | \exists b \in B .\langle a, b\rangle \in R \text { and }\langle b, c\rangle \in S\} $$


# Sytax and Semantics
## Object language and meta-language

*object* language, the language we study, the object of our attention

*meta language*, the language to describe object language

## grammar
example grammar for numeric expressions
$$
\begin{array}{l}{e : :=n|e+e| e-e} \\ {n : :=d | n d} \\ {d \quad :=0|1| 2|\ldots| 9}\end{array}
$$
**start symbol**: the symbol we begin if we want to derive a well-formed expression from the rules of grammar

**terminal**:

A grammar is ambiguous if there is some expression with more than one parse tree.

## Lexical analysis and Parsing
The first two phases of compilers are lexical analysis and parsing.

The traditional terminology of the field is that programs are written according to a *concrete syntax*, 是包括括号的规则的

parse tree for an expression is called an abstract syntax tree.

For example, no matter what grammar: prefix or postfix or infix, the parse tree can be the same

**example:**
$e : :=0|1| e+e|e-e| e * e$ this is a abstrct syntax for an expression language but by itself is not a good concrete syntax

because this can have ambiguourity

we can parsing unambiguous by adopting parsing convensions

### eample Mathematical interpretation
a historical convention is to write $\llbracket e \rrbracket$ for any parse tree of the expression $e$

Then we can define the **meaning** of an expression $e$: $\mathcal{E}\llbracket e \rrbracket$

For exmaple:
$$
\begin{aligned} \mathcal{E} \llbracket 0 \rrbracket &=\underline{0} \\ \mathcal{E} \llbracket 1\rrbracket &=\underline{1} \\ & \vdots \\ \mathcal{E} \llbracket 9 \rrbracket &=\underline{9} \\ \mathcal{E} \mathbb{I}(n d \mathbb{1}&=\mathcal{E} \mathbb{I} n \mathbb{1} * \underline{10}+\mathcal{E} \mathbb{I} d \mathbb{I} \\ \mathcal{E} \mathbb{I} e_{1}+e_{2} \mathbb{l} &=\mathcal{E}\left\|e_{1} \mathbb{l}+\mathcal{E}\right\| e_{2} \mathbb{I} \\ \mathcal{E} \mathbb{I} e_{1}-e_{2} \mathbb{l} &=\mathcal{E}\left\|e_{1}\right\|-\mathcal{E} \| e_{2} \mathbb{I} \end{aligned}
$$

where the underline number means the actual number. In contrast, the sysmbols on the left are symbols

# Induction
**base case**

**induction step**

**induction hypothesis**

### two forms of natrual number induction
**first form**

prove P(0) and prove that for any natural number m, if P(m) is true then  P(m+1) must also be true.

**second form**
prove that for any natural number m, if P(i) is true for all $i<m$, then P(m) must also be true.

**Note that there is no base case**

**The first form implies the second form:**
$$
Q(m) \stackrel{\text { def }}{=} \text { for all } i<m, P(i)
$$

## structural induction

Structural Induction, Form 1 To prove that  $P(e)$  is true for every expression  $e$  generated by some grammar, it is sufficient to prove $P(e)$ for every atomic expression and, for any compound expression $e$ with immediate subexpressions $e_{1}, \ldots, e_{k},$ prove that if $P\left(e_{i}\right)$  for $i=1, \ldots, k$  then  $P(e)$



Structural Induction, Form 2: To prove that $P(e)$ is true for every expression $e$ generated by some grammar, it is sufficient to prove that for any expression $e,$ if $P\left(e^{\prime}\right)$ for every subexpression $e^{\prime}$ of $e,$ then $P(e)$


## induction on Proofs

**Hilbert-style proof system:**

axioms

proof rules

**soundness** of proof systems: for every provable formular is ture.

### well-founded induction
A well founded relation on a set A is a binary relation $\prec$ on A with the property tht there is no infinite descending sequence $a_0 \succ a_1 \succ ....$

Lemma: Let $\prec$ be a binary relation on set A. Then $\prec$ is well-founded iff every nonempty subset of A has a minimal element

### proposition well-founded induction
let $\prec$.... If $P(a)$  holds whenever we have $P(b)$ for all $b\succ a$ then P(a) is true for all $a\in A$

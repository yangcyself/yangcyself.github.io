# CUE
- what is the syntax tree of lambda calculus?
- what is the notion of bind, free, and bound?
  - What is the recursive defn of the free?
- $\alpha,\beta$ equivalent?
  - what are the two steps of the $\beta$ reduction
  - what might happen if the first step is skipped
- give an example where $\beta$ reduction is not going to terminate
- what is the diamond property and does $\rightarrow _{\beta}$ have this property?
- what is the equivality $=_{\beta}$ defined?
- what is the Church-Rosser Theorem?
# lambda calculus

people use lambda calculus as a vehical, represent what is computable and what is not computable

**the testbed for procedural and functional languages**

> Whatever the next 700 languages turn out to be, they will surely be variants of lambda calculus. **landin '66**


>Fortran is developed toward math expression, lisp is developed toward computability, turing machine, lambda calculus in mind

this is invented before the notion of *Ojbect*

## syntax
$$
\begin{aligned}
    \text { e }::=&x & {\text { Variables }} \\ 
    | & \lambda x \text { .e } & {\text { Functions (abstraction) }} \\ 
    |& e_{1} e_{2} & {\text { function Application }}
\end{aligned}
$$

conventions 
- left association:
  - $xyz$ means $(xy)z$
- abstraction extends to right as far as possible
  - $\lambda x.x\lambda y.xyz$ means $\lambda x .(x(\lambda y .((x y) z)))$

## binds, free and bound

$\lambda x.e$ **binds** variable $x$ in $e$

$x$ is **bound** in the expression $\lambda x.e$

**free**: in $e$ iff it has occurrences that not bound in $e$. It can defined recursively:
- $\text{Free}(x) = \left\{x \right\}$
- $\text{Free}(e_{1} e_{2} ) = \text{Free}(e_{1} )\cup \text{Free}(e_{2} )$
- $\text{Free}(\lambda x.e) = \text{Free}(e)-\left\{x \right\}$


## $\alpha$ equivalent
$$
\lambda x.x = \lambda y.y
$$


## $\beta$ equivalent
the **two step substitution** of $e'$ for $x$ in $e$: ($[e'/x]e$)

1. Rename the bound variables in $e$ and $e'$ so that they are unique
2. Perform the textual substitution of $e'$ for $x$ in $e$

> **NOTE** in the first step, you cannot rename the free variable , it is not bound

### example
$$
[y(\lambda x. x) / x] \quad \lambda y .(\lambda x. x) y x
$$

the result should be 
$$
\lambda z.(\lambda u.u)z(y(\lambda v.v))
$$

if not careful, the result is 
$$
\lambda y .(\lambda x. x) y(y(\lambda x. x))
$$
this is called **inadvertent variable capture**

## operational semantics

all the operational semantics for $\lambda$-calculus are based on the equation 
$$
(\lambda x.e)e' =_\beta [e'/x]e
$$

called $\beta$-rule, $\beta$-reduction

$(\lambda x.e)e'$ called $\beta$-redex

- $e \rightarrow _{\beta } e'$ e reduce to e' **one step**
- $e \rightarrow _{\beta }^{*}  e'$ e reduce to e' **zero or more steps**

### Note that he reduction may not terminate

$$
(\lambda x, x x)(\lambda y \cdot y y) \rightarrow (\lambda y, y y)(\lambda y \cdot y y)
$$

> this is called *while-companied?*[没听清] (read this in book)
> >Y Combinator


> thus the while issue is the same as other semantic parts, **you can never know the result of $\lambda$-calculus** without actually running it

## Normal forms
**term without redexes**

**A reduction sequence stops at a normal form**

if $e$ is normal form and $e \rightarrow _{\beta }^{*}  e'$, then $e$ is identical (in sense of $\alpha$ equivalence) to $e'$

## Nondeterministic Evaluation

$$
\over
(\lambda x . e) e^{\prime} \rightarrow\left[e^{\prime} / x\right] e
$$

$$
\frac{e_{1} \rightarrow e_{1}^{\prime}}{e_{1} e_{2} \rightarrow e_{1}^{\prime} e_{2}}
$$

$$
\frac{e_{2} \rightarrow e_{2}^{\prime}}{e_{1} e_{2} \rightarrow e_{1} e_{2}^{\prime}}
$$

$$
\frac{e \rightarrow e^{\prime}}{\lambda x . e \rightarrow \lambda x . e^{\prime}}
$$

> **Note** this is non-determinitic. here the non-deterministic is the same as that non-deterministic in IMP

$$
{e_1 \rightarrow e_1' \over
e_1 + e_{2} \rightarrow e_{1}' + e_{2} }
\qquad
{e_2 \rightarrow e_2' \over
e_1 + e_{2} \rightarrow e_{1} + e_{2}'}
$$

## the order of evaluation and diamond property

A relation R has the diamond property (or is **confluent**) if whenever $e R e_{1}$ and $e R e_{2}$ then $\exist e' s.t. e_{1} Re', e_{2} Re'$

- $e \rightarrow _{\beta } e'$ do not have diamond property
- $e \rightarrow _{\beta }^{*}  e'$ have diamond property

> here the $R$ is the binary relationship (回想数学的机器语言--集合论)

### **equality**

$=_\beta$ : the **reflexive**, **transitive**, **symmetric** closure of $\rightarrow _{\beta}$

$$
=_{\beta} \text { is }\left(\rightarrow_{\beta} \cup \leftarrow_{\beta}\right)^{\star}
$$

### **Church-Rosser Theorem**

if $e_{1}  = _{\beta}e_{2}$ then there exist e' such that $e_{1} \rightarrow _{\beta}^* e$, and $e_{2} \rightarrow _{\beta}^* e$

### **corollaries**

if $e_{1}  = _{\beta}e_{2}$ and $e_{1}$ and $e_{2}$ are normal forms then $e_{1}$ is identital to $e_{2}$

proof use C-R theorem and normal forms beta reduction

if $e \rightarrow _{\beta}^* e_{1}$ and $e \rightarrow _{\beta}^* e_{2}$ and $e_{1},e_{2}$ are normal forms then, $e_{1},e_{2}$ identital 

## Evaluation strategies
- normal order
- call-by-name
- call-by-value
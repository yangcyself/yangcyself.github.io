# CUE
- what is abstract interpretation
- why do we introduce abstract interpretation
- What is the soundness of ai and the soundness of an operator defined?
  - To define this, we have to define $\beta,\gamma$ function
- Introduce the top and bottom
- Do lub and glb always exist?
- when does the lattice be a proper one?
- what is $\alpha$ $\beta$ $\gamma$ function?
- the three condition for Galois Connections
# The abstract interpretation

## recap:
the semantics we studied so far give us the **precise semantics**

However, we can get an abstract interpretation

> paper:

## abstract interpretation with exmaple 

for example: only the sign

$$
A: E x p \rightarrow\{-, 0,+\}
$$

$$
\begin{array}{|c|ccc|}\hline \underline{*} & {-} & {0} & {+} \\ \hline-& {+} & {0} & {-} \\ {0} & {0} & {0} & {0} \\ {+} & {-} & {0} & {+} \\ \hline\end{array}
$$

**note** $*$ is the operation in language, $\underline{*}$ is the operation in abstract interpretation

$$
\begin{array}{l}{A(n)=\operatorname{sign}(n)} \\ {A\left(e_{1}^{*} e_{2}\right)=A\left(e_{1}\right) \pm A\left(e_{2}\right)}\end{array}
$$

$A$ means abstract 

## Soundness
the correctness can be proved via induction
### two associated functions
**abstraction functions**: do the abstraction
$$
\beta: z \rightarrow\{-, 0,+\}
$$

**concretization functions**: map from the ai to the real word set
$$\begin{array}{l}{\gamma:\{-, 0,+\} \rightarrow \mathcal{P}(z)} \\ {\gamma(+)=\{n \in Z | n>0\}} \\ {\gamma(0)=\{0\}} \\ {\gamma(-)=\{n \in Z | n<0\}}\end{array}$$

**Soundness can be stated succinctly**
$$
\forall e \; E x p .[\mathbb{e}] \in \gamma(A(e))
$$

so the expression is saying:
```txt
Exp ->  A(or beta) -> Abs
 |                     |
 [](precise semantics) gamma
 |                     |
 C  ->      \in   ->  P(C)
```

Consider the generic abstraction of an operator

$$
A\left(e_{1} \text { op } e_{2}\right)=A\left(e_{1}\right) \underline{o p} A\left(e_{2}\right)
$$
it is sound iff
$$
\forall a_{1} \forall a_{2} \cdot \gamma\left(a_{1} \underline{o p} a_{2}\right) \supseteq\left\{n_{1} \text { op } n_{2} | n_{1} \in \gamma\left(a_{1}\right), n_{2} \in \gamma\left(a_{2}\right)\right\}
$$
> note comparing with the previous equation, this is for one single operator:
> **This reduces the proof of correctness to one proof for each operator**

## Add Top and Bottom

Top: includes everything
Bottom: empty(divide 0 or **non termination**)

$$
\begin{array}{|c|ccccc|}\hline \underline{/}& {-} & {0} & {+} & {\top} & {1} \\ \hline-& {+} & {0} & {-} & {\top} & {\perp} \\ {0} & {\perp} & {\perp} & {\perp} & {\perp} & {\perp} \\ {+} & {-} & {0} & {+} & {\top} & {\perp} \\ {\top} & {\top} & {\top} & {\top} & {\top} & {\perp} \\ {1} & {1} & {1} & {\perp} & {1} & {\perp} \\ \hline\end{array}
$$

### abstraction forms a lattice

$$
\begin{array}
    c && \top && \\ & \nearrow & \uparrow & \nwarrow & \\
    - && 0 && +\\
  & \searrow & \downarrow & \swarrow & \\
  &&\bot
\end{array}
$$


**lub**: least upper bound

**glb**: greatest lower bound

A lattice is **complete** when all subsets have lub and gub

> note that if a and b have lub be c or d, then this is not a proper lattice
## standard recipe for defining Abstract Interpretation

**have one abstraction function**
$$
\beta: C \rightarrow A b s
$$

then **concretization function**
$$
\begin{array}{l}{\gamma: A b s \rightarrow \mathcal{P}(C)} \\ {\gamma(a)=\{x \in C | \beta(x) \leq a\}}\end{array}
$$

**define a concrete map mapping $\alpha$**
1. Pick S’the smallest that includes S and is in the image of $\gamma$
2. Define a(S)= $\gamma$^{-1}(S’)
3. Then we define: $a_1\underline{op} \;a_2$= $a(\gamma(a1) op\;  \gamma(a2))$
4. This ensures soundness by construction

**or another definition**
$$
\begin{array}{l}{\alpha: \mathcal{P}(C) \rightarrow A b s} \\ {\alpha(S)=lu b\{\beta(x) | x \in S\}}\end{array}
$$

## Galois Connections

A Galois connectionbetween complete lattices Abs and P(C) is a pair of functions a and $\gamma$ such that:
- $\gamma$ and $\alpha$ are monotonic
- $\alpha (\gamma (a)) = a$ for all $a\in Abs$
- $\gamma (\alpha (S)) \supseteq S$ for all $S\in \mathcal{P}(C)$

three conditions define a correct abstract interpretation
- $\gamma$ and $\alpha$ are monotonic
- $\gamma$ and $\alpha$ form a Galois connection
- Abstraction of operations is correct
  - $a_{1} \underline{\mathrm{op}} \mathrm{a}_{2}=\alpha\left(\gamma\left(\mathrm{a}_{1}\right) \text { op } \gamma\left(\mathrm{a}_{2}\right)\right)$

> Note here is the equal sign


# CUE
- axiomatic semantics
- how to write Hoare tuple
- how to formally write paritial correctness and total correctness assertions?
- what are the rules?
  - consequence rule
  -  assign rule
  - sequence rule
  - if then else rule
  - while loop
    - How to find a loop invariant
  - backward assign axiom

# axiomatic semantics
consists of:
- a language for stating assertions about programs
- Rules for establishing the truth of assertions

## some typical languages of asssertions
- First-order logic
- Other logics (temporal, linear)
- Special-purpose specification languages (Z, Larch, JML)

# Assertions for IMP

the assertion form
$$
\left\{A \right\} c \left\{B \right\}
$$

-  If A holds in state $\sigma$ and $<c, \sigma>\forall \sigma^{\prime}$
-  then B holds in $\sigma'$

## partial&total correctness assetion

**partial correctness assertion:** $\vDash\left\{A \right\}c\left\{B \right\}$: does not imply termination

**total correctness assertion:** $\vDash [A]c[B]$ meaning that 

$\sigma \vDash A$: an assertion holds in a given state

### semantics of assertions
$$
\begin{array}{ll}{\sigma \vDash \text { true }} & {\text { always }} \\ {\sigma \vDash e_{1}=e_{2}} & {\text { iff }\left[e_{1}\right] \| \sigma=\left[\mathbf{e}_{2}\right][\sigma} \\ {\sigma \vDash e_{1} \geq e_{2}} & {\left.\text { iff }\left[e_{1}\right]\right] \sigma \geq\left[\mathbf{e}_{2}\right][\sigma} \\ {\sigma \vDash A_{1} \wedge A_{2}} & {\text { iff } \sigma=A_{1} \text { and } \sigma \vDash A_{2}} \\ {\sigma \vDash A_{1} \vee A_{2}} & {\text { iff } \sigma=A_{1} \text { or } \sigma \vDash A_{2}} \\ {\sigma \vDash A_{1} \Rightarrow A_{2}} & {\text { iff } \sigma \vDash A_{1} \text { implies } \sigma A_{2}} \\ {\sigma \vDash \forall x . A} & {\text { iff } \sigma=2 \cdot \sigma[x :=n] \vDash A} \\ {\sigma=\exists x . A} & {\text { iff } \exists n \in Z \cdot \sigma[x :=n] \vDash A}\end{array}
$$

**Partial correctness assertion**

$$
{\vDash\{A\} c\{B\} :} {\quad \forall \sigma \in \Sigma . \forall \sigma^{\prime} \in \Sigma .\left(\sigma \vDash A \wedge\langle c, \sigma\rangle\Downarrow \sigma^{\prime}\right) \Rightarrow \sigma^{\prime} \vDash B}
$$

**total correctness assertion**
$$
{\vDash [A] c[B]:}\quad {\forall \sigma \in \Sigma . \sigma \in A \Rightarrow \exists \sigma^{\prime} \in \Sigma .\langle c, \sigma \rangle \forall \sigma^{\prime} \wedge \sigma^{\prime} \vDash B}
$$

## Deriving Assertion
lets decide when $\{A\} \;c\; \{B\}$ 

## derivation rules
-
$$
\vdash A \quad \vdash B \over \vdash A \wedge B
$$
-
$$
\frac{\vdash[a / x] A \quad(a \text { is fresh })}{\vdash \forall x, A}
$$
-
$$
\vdash \forall x.A
\over
\vdash [e/x]A
$$
-
$$
\begin{array}c 
\vdash A \\
... \\
\vdash B \\ \end{array}   
\over
\vdash  A \Rightarrow B
$$
-
$$
\vdash A \Rightarrow B \quad  \vdash A
\over
\vdash B
$$
- 
$$
\frac{\vDash[\mathrm{e} / \mathrm{x}] A}{\vdash \exist x A}
$$
- 
$$
\vdash \exist x.A \quad
\begin{array}c 
\vdash [a/x]A \\
... \\
\vdash B \\ \end{array} 
\over
\vdash B
$$



## Derivation Rules for Hoare Logic

$$
\over
\vdash \{A\} \text { skip }\{A\}
$$

**Consequence rule**

$$
\vdash A^{\prime} \Rightarrow A\quad \vdash \{A\} c\{B\}\quad \vdash B \Rightarrow B^{\prime}
\over
\vdash  \{A'\} \quad c \quad \{B\}
$$

**assign rule**
$$
\over
\vdash 
\{[e/x]A\} \; x:= e \; \{A\}
$$

example

$$
\{?\}\; x:=x+1 \; \{x<0\}
$$
就是把x+1换进去然后解不等式

**sequence rule**
$$
\vdash \left\{A \right\}c_1\left\{B \right\} \quad \vdash \left\{B \right\}c_2\left\{C \right\}
\over
\vdash \left\{A \right\} c_1;c_2 \left\{B \right\}
$$

**if then else rule**
$$
\frac{\vdash\{A \wedge b\} c_{1}\{B\}\quad \vdash\{A \wedge-b\} c_{2}\{B\}}{\vdash\{A\} \text { if } b \text { then } c_{1} \text { else } c_{2}\{B\}}
$$

**While loop**
$$
\frac{\vdash\{A \wedge b\} c\{A\}}{\vdash\{A\} \text { while } b \text { do } c\{A \land \lnot  b\}}
$$
where $A$ is a loop invariant, but until now finding it is still a problem

**backward assign axiom**

$$
\vdash\{A\} \times :=e\left\{\exists x_{0} \cdot\left[x_{0} / x\right] A \wedge x=\left[x_{0} / x\right] e\right\}
$$


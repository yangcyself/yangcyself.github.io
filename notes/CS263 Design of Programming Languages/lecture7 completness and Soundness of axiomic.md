# CUE
- what is soundness and compleness respectively?
- Prove soundness of consequence law (这个说法不严谨，但是就是这个意思)
  - what is the used assumption? Did this decrease?
- Prove the soundness of while loop
  - what is the used assumption? Did this decrease?

# road map
we have seen four set of languages, each have rules in it.
1. IMP language
2. The entilement language(我起的非正式名字)) $\sigma \vDash A$ and $\vDash \left\{A \right\}c\left\{B \right\}$ 
   - this defines how to judge True or False, 
   - this can be regarded as evaluation rule based on denotation semantics 
3. assertion language borrowed from first order logic $\vdash A$ (the derivation axioms)
4. Hoare triple assertion language $\vdash \left\{A \right\}c\left\{B \right\}$
   1. we can reason about things in this language

We use the IMP language to describe the (2) entile ment language, and we designed a logical system (4) to make assertions. But we do not know whether the assertion system is true when comparing with the entilement language. The two properties:
- Soundness 
  - all the assertion that we can derive from our logical system are true in the entilement language
  - (4) -> (2)
  - $\text{if} \vdash \left\{A \right\} c \left\{B \right\} \text{then} \vDash \left\{A \right\} c \left\{B \right\}$
  - or to say: $\forall \sigma \text{ if } \sigma \vDash A \text{ and } D::M\langle c,\sigma \rangle \Downarrow\sigma' \text{ and }H::\left\{A \right\} c \left\{B \right\} \text{ then } \sigma' \vDash B$
- Completeness
  - all things that are true in the entilement language can be showed (by a derivation tree) from our logical system


## Proof of soundness
by **simutaneous induction**

define the ordering:
$$
(d,h) < (d',h') \text{ iff } d<d' \text{ or } d = d' \text{ and } h<h'
$$

### Soundness of consequence rule
$$
H : \frac{\vdash A \Rightarrow A^{\prime} \quad H_{1} ::\vdash \left\{A^{\prime}\right\} c\left\{B^{\prime}\right\} \quad\vdash B^{\prime} \Rightarrow B}{\vdash \{A\} c\{B\}}
$$

Here the hypothesis:
- first-order-logic derivations are sound
- there exists a induction tree $D$ that $\llbracket c \rrbracket\sigma=\sigma'$
- there exists a $H_1$
- the soundness is true for $(D,H_1)$ thus, $\sigma'\vDash B'$

### Soundness of Assignment
Case: the last rule used in H :: ⊢{ A } c { B} is the assignment rule

The last rule used in $D::M\langle \text{x:=e},\sigma \rangle \Downarrow \sigma$ must be 
$$
D : \frac{D_{1} :\langle e, \sigma \rangle \Downarrow n}{\langle x :=e, \sigma\rangle \Downarrow \sigma[x :=n]}
$$

this can be proved by substitution lemma
$$
\text{If } s⊨[e/x]B \text{ and } <s, e> ßn \text{ then } s[x := n]⊨B
$$

### Soundness of the while rule
suppose that the last rule used in $H: \vdash \left\{A \right\}c\left\{B \right\}$
is 
$$
H:: {
H_1:: \vdash \left\{A \land b \right\}c\left\{A \right\}
\over
\vdash \left\{A \right\}\text{while b do c}\left\{A\land\lnot b \right\}
}
$$
and suppose the corresponding $D$ is while-true
$$
\mathrm{D} :: \frac{\mathrm{D}_{1} : :\langle \mathrm{b}, \sigma \rangle \Downarrow \text { true } \mathrm{D}_{2} :\langle \mathrm{c}, \sigma \rangle \Downarrow  \sigma^{\prime} \quad \mathrm{D}_{3} ::\langle \text { while } b \text{ do c}, \sigma^{\prime} \rangle \Downarrow \sigma''}{\langle \text { while } b \text{ do c}, \sigma^{\prime} \rangle \Downarrow \sigma''}
$$

we assume that 
$\sigma\vDash A$

show that 
$\sigma''\vDash A\land\lnot b$

use the hypothesis:
1. from $D_1$ we get $\sigma\vDash b$ thus $\sigma\vDash A\land b$
2. from $D_2$ we get $\sigma'$ and from (1) we get $\sigma' \vDash A$
3. from the hypothesis $\langle D_3,H \rangle$ we get $\sigma'' \vDash A\land \lnot b$
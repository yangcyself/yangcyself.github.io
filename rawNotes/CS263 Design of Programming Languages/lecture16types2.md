# CUE
- recap the contextual semantics
  - what is the difference of this against big and small step semantics?
- Give the grammar of Context and redex of F1
  - Note the grammar implies the evaluation order
- add bool short-cuts to the grammars
- Express the following properties of F1 with formal languages(with notions like $\empty \vdash e:\tau$ and $e = H[e']$)
  - unique decomposition
  - redex closed and well typed
  - local reduction is type preserving
  - substitution lemma
- write the context and redex rules for:
  - product type
  - records
  - sum types (operation names are `injl`, `injr`, and `case`)
- use sum types to express boolean.


# contextual semantics(with types)

recap the contextual semantics in the first chapter
$$
H[r]
$$

> H is called the context and $r$ is called the redex, also called hole and marked by $\bullet$

redex is the smallest grunality of things that you can reduce in one atomic step

> This is neither big nor small step semantics\
> I don't want to reintroduce the whole rule, I just want to add some Macro rules. I'm just patching(打补丁) on the existing way of semantics without reimplementing

The global reduction step:
$$
\text{If } r\rightarrow e \text{ then } H[r] \rightarrow H[e]
$$

For exmaple in F1, the redex's can be defined as
$$
\begin{aligned} r::=& n_{1}+n_{2} \\ & | \text { if true then } e_{1} \text { else } e_{2} \\ & | \text { if false then } e_{1} \text { else } e_{2} \\ & |\left(\lambda x: \tau \cdot e_{1}\right) v_{2} \end{aligned}
$$

and have the rule
$$
\begin{array}{l}{n_{1}+n_{2} \rightarrow n} \\ {\text { if true then } e_{1} \text { else } e_{2} \rightarrow e_{1}} \\ {\text { if false then } e_{1} \text { else } e_{2} \rightarrow e_{2}} \\ {\left(\lambda x: \tau \cdot e_{1}\right) v_{2} \rightarrow\left[v_{2} / x\right] e_{1}}\end{array}
$$

Context are also defined by a grammar, for example

$\begin{aligned} H::=& \bullet|H+e| n+H | \text { if } H \text { then } e_{1} \text { else } e_{2} \\ &|H e|(\lambda x: \text { t.e }) H \end{aligned}$

> Note that the grammar implies the order of evaluation.\
>For example $H+e|n+H$ implies evaluate from left to right\
>$(\lambda x:t.e)H$ implies call by name

## example: experss short-circuit

the contexts and redexes have the following rules:

$$
\begin{array}{l}{\mathrm{H}: :=\ldots | \mathrm{H} \wedge \mathrm{b}_{2}} \\ {\mathrm{r}::=\ldots|\mathrm{true} \wedge \mathrm{b}| \text { false } \wedge \mathrm{b}} \\ {\text { true } \wedge \mathrm{b} \rightarrow \mathrm{b}} \\ {\text { false } \wedge \mathrm{b} \rightarrow \mathrm{false}}\end{array}
$$

> the $\dots$ is the old rules for the semantics.
>  So we are just patching new rules

## Contextual semantics for F1
### **decomposition lemmas**
**unique decomposition**
If $\emptyset \vdash e:\tau$ and $e$ is not a value then there exist unique $H$ and $r$ such that $e = H[r]$
- Any well typed expression can be decomposed
- Any well-typed non-value can make (deterministic) progress

And:
- **redex closed and well typed**$\exist \tau '$ such that $\empty\vdash r: \tau '$

- **local reduction is type preserving** $\exist e'$ such that $r \rightarrow e'$ and $\empty \vdash e':\tau '$

- **substitution lemma** if $\empty \vdash e : \tau$ and $e  =  H[e']$ for any $e'$, $\empty\vdash e':\tau '$ imples $\empty\vdash H[e']:\tau$

>Furthermore, due to type preservation we know that the execution of a well typed expression never gets stuck
>> [II][??] Confused

# extend other types

## Product types $F_{1}^{\times}$

$$
\begin{array}{l}{e::=\ldots\left|\left(e_{1}, e_{2}\right)\right| \text { fste } | \text { snd } e} \\ {\tau::=\ldots | \tau_{1} \times \tau_{2}}\end{array}
$$

**typing judgement rules**
$$
\frac{\Gamma \vdash e_{1}: \tau_{1} \quad \Gamma \vdash e_{2}: \tau_{2}}{\Gamma \vdash\left(e_{1}, e_{2}\right): \tau_{1} \times \tau_{2}}
$$

$$
\frac{\Gamma \vdash e: \tau_{1} \times \tau_{2}}{\Gamma \vdash \text { fst } e: \tau_{1}} \frac{\Gamma \vdash e: \tau_{1} \times \tau_{2}}{\Gamma \vdash \text { snd } e: \tau_{2}}
$$

**big step evaluation rules**
$$
\frac{e_{1} \Downarrow v_{1} \quad e_{2} \Downarrow v_{2}}{\left(e_{1}, e_{2}\right) \Downarrow\left(v_{1}, v_{2}\right)}
$$

$$
\frac{e \Downarrow\left(v_{1}, v_{2}\right)}{\text { fst } e \Downarrow  v_{1}} \quad \frac{e \Downarrow\left(v_{1}, v_{2}\right)}{\text { snd } e \Downarrow  v_{2}}
$$

**new contexts and redexes rules**

$$
H::=\ldots\left|\left(H, e_{2}\right)\right|\left(v_{1}, H\right) | \text { fst } H | \text { snd } H
$$
$$
\begin{array}{l}{\text { fst }\left(v_{1}, v_{2}\right) \rightarrow v_{1}} \\ {\text { snd }\left(v_{1}, v_{2}\right) \rightarrow v_{2}}\end{array}
$$

the soundness can be proved

> still note the order implied in $\left(H, e_{2}\right)|\left(v_{1}, H\right)$

## records
$$
e:=\ldots\left|\left\{L_{1}=e_{1}, \ldots, L_{n}=e_{n}\right\}\right| e . L
$$
tuples with labels


## sum types
$$
\begin{array}{l}{\left.e:=\ldots | \text { injl }e | \text { injr } e| \text { (case e of injl } x \rightarrow e_{1} | \text { injr } y \rightarrow e_{2}\right)} \\ {\tau::=\ldots | \tau_{1}+\tau_{2}}\end{array}
$$

> Like **Union** in C or pascal

> the `Case e` statement is just like the `match` statement in Ocaml

The `injr` and `injl` means injection left and injection right. Input a type $\tau$ and output a type $\tau+\tau '$

### **example: express other thing**

this can express Boolean

- **`true`** $\text{injl }()$
- **`false`** $\text{injr }()$
- **`if e then e1 else e2`** $\text { (case e of injl } x \rightarrow e_{1} | \text { injr } y \rightarrow e_{2})$


> $()$ is unit element (or null element)

**Note Now types are not unique anymore**

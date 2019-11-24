# CUE
- given the defn of reference types, write down the rules
- Whrite down the rules for typing and evaluation of exceptions

# the imperative features with contextual semantics
 imperative means that the effect is non-local
## reference types

$$
\begin{array}{l}{e::=\ldots | \text { ref }e : \tau\left|e_{1}:=e_{2}\right| ! e} \\ {\tau::=\ldots | \tau \text { ref }}\end{array}
$$

- $\text{ref }e:\tau$ is malloc, null-check, and initialization together($e$ is the init value) 
- $e_{1} :=e_{2}$ assignement
- $!e$ get from the memory cell

**To model the non-local effect**, we need to have someting global

### heap state

$$
h::=\emptyset | h, a<v: \tau
$$

> Note the **erasure property:** types on heap cells are not needed for the evaluation. JVM has this kind of property to make the binary smaller. "every good language should have this"

### Program and program state
$$
p:=\text { heap } h \text { in } e
$$

this line just like `let xx in xx`

### it has typing rules ...

### Contextual semantics **global rules**

$$
\mathrm{H}::=\text { ref } \mathrm{H}: \tau\left|\mathrm{H}:=\mathrm{e}_{2}\right| \mathrm{a}_{1}:=\mathrm{H} | ! \mathrm{H}
$$

> still note that $\mathrm{H}:=e_{2} | a_{1}:=\mathrm{H}$ implies order

$$
\text { heap } h \text{ in H[ref }v: \tau] \rightarrow \text { heap } h, a \leftarrow v: \tau \text { in } H[a]
$$

$$
\text { heap } h \text { in } \mathrm{H}[\mathrm{a}] \rightarrow \text { heap } h \text { in } \mathrm{H}[\mathrm{v}]
$$

$$
\text { heap } h \text { in } H[a:=v] \quad \rightarrow \quad \text { heap } h[a \leftarrow v] \text { in } H[()]
$$

> Note that modeled like this, we can then test the garbage collection's correctness.\
> The expression after reduction and garbage collection should be equal to the original one.

> for example
> $$
>\text { heap } \emptyset \text { in }(\lambda f \text { int } \rightarrow \text { int ref. } !(f 5)) \quad(\lambda x \text { int. } \text {ref} x: \text { int })
>$$
>evaluates to $\text { heap } a=5: \text { int in } 5$\
> after garbage collection 
> $\text { heap } \varnothing \text { in } 5$ should be equal

> This `heap xx in xx` statement maybe can express **scope**

## exceptions

exception never return to $H$(context)
>here the 'return' means in the sense of evaluation of the redex

### Exception Syntax
$$
\begin{array}{l}{e:=\ldots | \text { raise } e | \text { try } e_{1} \text { handle } x=>e_{2}} \\ {\tau::=\ldots | e x n}\end{array}
$$

### **Typing rules**
$$
\frac{\Gamma \vdash e: \text { exn }}{\Gamma \vdash \text { raise } e: \tau}
$$

$$
\frac{\Gamma \vdash e_{1}: \tau \quad \Gamma, x: \operatorname{exn} \vdash e_{2}: \tau}{\Gamma \vdash \operatorname{try} e_{1} \text { handle} x \Longrightarrow e_{2}: \tau}
$$

Note the $\Gamma \vdash \text { raise } e: \tau$ 

This means that the `raise` statement itself can be whatever type to pass the type checking. So a statement crazy as `if(raise 2) then 1 else 2` is okay.

But a requirement is $\Gamma, x: \operatorname{exn} \vdash e_{2}: \tau$ the raised value should match the type of the value if not raise.

> [II] in ppt `(raise 2)5` is also leagle, but how, when is the `(raise 2)` evaluated?

### Model the semantics for exceptions

**Introduce another context that propagate exceptions**

$$
\mathrm{H}::=\cdot|\text{H e}| \text { v H } | \text { raise } \mathrm{H} | \text { try } \mathrm{H} \text { handle } x \Rightarrow \mathrm{e}
$$
$$
P::=\cdot | \text { Pe}|{vP } | \text { raise } P
$$

with the rules
$$
(\lambda x ; \tau . e) v \quad \rightarrow[v / x] e
$$
$$
\text { try v handle } x\Rightarrow e \quad \rightarrow v
$$
$$
\text { try P[raise v] handle } x=>e \quad \rightarrow[v / x] e
$$
$$
\text { P[raise v] } \quad \rightarrow \text { uncaught v }
$$
> 没有看懂p[raisev] 是如何传上来的
A typical example for imperative programs is the assign statement x:=y

**aliasing**: the location variabels x, y are given the same location by the environment

### separate environments from stores
environments -> symbol table

store -> the contents in compiled program

$$
\langle M, s\rangle_{\eta} \stackrel{\text { eval }}{\sim} v
$$
to suggest that we "evaluate" expression M in store s with respect to environment $\eta$ and obtain value v. 

## evaluation of expressions
quite similar to lecture1 operational semantics

p395
QUESTION:\??? what is algebra A? The function of memory management?

## [\\!!] exercise 6.3.4
**Nondeterministic program**

added two nondeterministic commands

$$
\begin{aligned} P :=& x :=M|P ; P| \text { if } B \text { then } P \text { else } P | \text { while } B \text { do } P \text { od } | \\ & P \cup P | P \| P \end{aligned}
$$

arbitrarily choosing to execute P1 or P2 and, execute P1 and P2 in parallel, no matter what the order.

$$
(x :=1 ; x :=(\operatorname{con} t x)+1) \|(x :=2 ; x :=(\operatorname{con} t x)+2)
$$
this may return 2,4,5


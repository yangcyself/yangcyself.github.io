# notions
$\lambda$ is the set of the $\alpha!x$ and $\alpha?x$ and $\tau$ some times
## Process:
  - input, output channels
  - process can composition to be another process

### operations
**parallel composition**


**restriction:**

hides a specified set of ports

$p \backslash\{\alpha, \gamma\}$ results in a process

**relabelling:**

generate several copies of the same process but for a renaming of channels.

$p[f]$ returns a process that interface is relabeled by $f$

$f: port -> port$

**communications**

$a?n$ and $a!n$

$\tau$: earlier Skip

> Note to say the $P$ are equal:

P ranges over **identifiers** for processes

### **rules**

$$
\frac{p_{0} \stackrel{\lambda}{\longrightarrow} p_{0}^{\prime}}{p_{0}\|p_{1} \stackrel{\lambda}{\longrightarrow} p_{0}^{\prime} \| p_{1}}
$$


$$
\frac{p_{0} \stackrel{\alpha?n}{\longrightarrow} p_{0}^{\prime}
\;p_{0} \stackrel{\alpha!n}{\longrightarrow} p_{0}^{\prime}
}{p_{0}\|p_{1} \stackrel{\tau }{\longrightarrow} p_{0}^{\prime} \| p_{1}}
$$

>Note that the second one gets $\tau$ unber the line.

也就是说一个收的一个发的然后二者抵消了嘛？

## Pure CCS

get rid of the variables

expand a term 
$\alpha ? x \rightarrow p$ to the sum of enumerating all possible values
$$
\left(\alpha ? n_{1} \rightarrow p\left[v_{1} / x\right]\right)+\ldots+\left(\alpha ? n_{k} \rightarrow p\left[v_{k} / x\right]\right)
$$

or when the value set is infinite we can write

$$
\sum_{m \in \mathbf{N}}(\alpha ? m \rightarrow p[m / x])
$$

> Note the difference between $\alpha ?x$ and $\alpha ?n$. The first one is wait for $\alpha$ channel to assign value $x$ and the second one is wait a number to be excatly $n$ from $\alpha$.



**three kinds of names**
- actions $l$ 
  - $\alpha ? n$ or $\alpha ! n$
- complementary action $\bar{l}$
  - $\alpha ?n$ completmentary to $\alpha !n$ 
  - and the opposite
  - it is symmetry
- internal actions $\tau$


The syntax of pure CCS
$$
p:=\operatorname{nil}|\lambda, p| \sum_{i \in I} p_{i}\left|\left(p_{0} \| p_{1}\right)\right| p \backslash L|p[f]| P
$$

Note that here $\lambda .p$ is convenient way of writing the guard process $\lambda \rightarrow p$


> Now we only know about the rules, but we do not know about the meaning yet. Maybe has to do with the sound and compelete


### **use the recursive definition**

$$
\frac{p[\mathrm{rec}(P=p) / P] \stackrel{\lambda}{\rightarrow} q}{\operatorname{rec}(P=p) \stackrel{\lambda}{\longrightarrow} q}
$$

## A specification language 
> the soundness and the completeness

### **Notions**

- Bisimulation
  - they satisfy precisely the same assertions in a little modal logic
- HennessyMilner logic

### **the HennessyMilner logic**

$$
A:=T|F| A_{0} \wedge A_{1}\left|A_{0} \vee A_{1}\right| \neg A |\langle\lambda\rangle A
$$

$\langle \lambda  \rangle A$ modal assertion. 

Satisfied by **any** process which **can do** a $\lambda$. action to become a process **satisfying $A$**

dual modality in logic $[\lambda]A$ this is $\neg\langle\lambda\rangle \neg A$

by any process which **cannot do a $\lambda$**. action to become one **failing** to satisfy A. 

> to understand this, consider
> $\neg(\langle\lambda\rangle \neg A)$

and this assertion is satisfied by any process which cannot do any>. action at all.

**Note that this is finite**

a single assertion can only specify the behaviour of a process to a finite depth

### **an example: deadlock**

**State of dead**

$$
\text { Dead } \equiv  _\text{def}([.] F \wedge \neg \text { terminal })
$$

The $[.]F$ means the cannot do any step further 
> F means false, and not the $[]$ rather than $\langle \rangle$

terminal is defined as some state that is properterminated

**The dead lock process**

$$
\text { Dead } \vee\langle\cdot\rangle \text { Dead } \vee\langle\cdot\rangle\langle\cdot\rangle \text { Dead } \vee\langle\cdot\rangle\langle\cdot\rangle\langle\cdot\rangle \text { Dead } \vee \cdots \vee(\langle.\rangle \cdots\langle\cdot\rangle D e a d) \vee \cdots
$$
> reaches deadlock state after arbitrary steps

But, of course, this is not really an assertion because of infinity

### introduce infinite disjunction
$$
\mu X .(D e a d \vee\langle.\rangle X)
$$

this is related to *least upper bound* of chains and *least fixed point*

### generalize it

$$
\text {possibly}(B) \equiv _\text{def} \mu X .(B \vee\langle.\rangle X)
$$

$$
\text {eventually}(B) \equiv_{\text {def}} \mu X .(B \vee(\langle.\rangle T \wedge[.] X))
$$

$$
\nu X .(B \wedge[.] X)
$$

satisfied by those processes which, no matter what actions they perform, always satisfy B.


> I don't quite get this

express that an assertion B is satisfied all the way along an infinite sequence of computation from a process
$$
\nu X .(B \wedge\langle.\rangle X)
$$

## the modal $\upsilon$-calculus

introduce **Assertions**


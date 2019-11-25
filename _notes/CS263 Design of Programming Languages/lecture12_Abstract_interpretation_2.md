# CUE
- what is lables? collecting semantics, and bounded $C_i^k$?
  - write formally as mapping
- What are the rules for collecing semantics on the flow-chart
  - assign
  - condition
  - join
- write the rules in abstract domain
- why do we have guarantee of termination in abstract domain?
  - what is the "at most" bound?
- what is the difference between mapping abs states as $A=\{x, y\} \rightarrow\{1,-, 0,+, T\}$(independently) and as $A=\mathcal{P}(\{\perp,-, 0,+, T\} \times\{\perp,-, 0,+, T\})$(as a whole)
- what is the lattice of **Linear relationships between variables**

# summarise
- This lectures follows the previous lecture about lattice, and moves the notions to the states
- with the finite height abstraction we can analysis through the flow-chart with guarentee of termination.


# The Collecting Semantics

## defn of new notions
- labels
- collecting semantics
- Bounded $C_i^k$
  - the set of states reached at program point iafter at most k execution steps
  
### **labels**

points in a flowchart program

### **collecting semantics**

$$
C \in \text { Labels } \rightarrow \mathcal{P}(\Sigma)
$$

mapping a program label to a set of program states


### **Bounded $C_i^k$**

the set of states reached at program point iafter at most k execution steps

initial state：
-  entry points $C_{i}=\Sigma$
-  $\emptyset$ for all other labels

$$
C_{i}=U_{k \in N} C_{i}^{k}
$$


> II 我觉得这个应该是和loop的展开一样为了后面的迭代分析方便而设置的，
> II 我觉得这个的定义有一些问题，比如两个分支的长度不一样，这样就会导致合并的时候同一个语句的不同k的合并。



## rules 
### Assignment
$$
C_{\mathrm{j}}=\left\{\sigma[x:=n] | \sigma \in C_{\mathrm{i}} \wedge \llbracket e \rrbracket \sigma=n\right\}
$$


### conditions
$$
\begin{array}{l}{C_{\mathrm{j}}=\left\{\sigma | \sigma \in C_{\mathrm{i}} \land \llbracket b \rrbracket\sigma =\text { false }\right\}} \\ {C_{\mathrm{k}}=\left\{\sigma | \sigma \in C_{\mathrm{i}} \land\llbracket b \rrbracket\sigma =\text { true }\right\}}\end{array}
$$

### join (after branch)

$$ C_{\mathrm{k}}=C_{\mathrm{i}} \cup C_{\mathrm{j}} $$

> **Note** there should be a new version of these rules with Bounded$C_i^k$

**Now with these rules, we can calculate and update $C_i^k$ round and round** 

## Abstract interpretation
$$
\mathrm{a} \in \text { Labels } \rightarrow \mathrm{A}
$$
> here 'a' stands for abstraction?

> 到了abstract interpretation 的地方先想 $\alpha \beta \gamma$ functions

 - pick $\alpha : \mathcal{P}(\Sigma) \rightarrow A$
 - pick $\beta: \Sigma \rightarrow A$
 - the above defines its Galois connection $\gamma$

### **rules**
**assign**
$$
a_{j}=\alpha\left\{\sigma[x:=n]\;|\;\sigma \in \gamma\left(a_{i}\right) \land  \llbracket e \rrbracket\sigma=n\right\}
$$
**conditional**
$$
a_{j}=\alpha\left\{\sigma | \sigma \in \gamma\left(a_{i}\right) \wedge \llbracket e \rrbracket \sigma=false \right\}\\
a_{k}=\alpha\left\{\sigma | \sigma \in \gamma\left(a_{i}\right) \wedge \llbracket e \rrbracket \sigma=true \right\}
$$
**join**
$$
a_{k}=\alpha\left(\gamma\left(a_{i}\right) \cup \gamma\left(a_{j}\right)\right)=l u b\left\{a_{i}, a_{j}\right\}
$$

## least fixed point

We can update $C_i^k$ round and round. **But Now we have guarantee of termination** 

In this case the computation takes at most $O(h*|\text{labels}^2|)$ steps

$h$ is the finite height of $A$(lattice of the abs domain)


## Notes:

previously in example We abstracted the state of each variable independently
$$
A=\{x, y\} \rightarrow\{1,-, 0,+, T\}
$$


**We can also abstract the state as a whole**

$$
A=\mathcal{P}(\{\perp,-, 0,+, T\} \times\{\perp,-, 0,+, T\})
$$

> 这二者的区别是 第一个只能表示 x y 都是top, 但是第二个可以表示x y虽然单个看都是top， 但是x 和 y的符号永远相同


## Other Abstract Domains
- **Linear relationships between variables**
  - A convex polyhedron is a subset of $Z^k$ whose elements satisfy a number of inequalities $a_{1} \times_{1}+a_{2} \times_{2}+\ldots+a_{k} x_{k} \geq c$
  - **complete lattice**, use linear programming methods for computing lub
- Linear relationships with at most two variables
  - Octagons: $x \pm y>=c$ have efficient algorithms

> II 可能对我搞控制很有用？
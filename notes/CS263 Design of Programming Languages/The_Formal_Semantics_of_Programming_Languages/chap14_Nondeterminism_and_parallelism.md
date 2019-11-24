# CUE

# introduction

**small step operational semantics**
$$
\frac{\left\langle c_{0}, \sigma\right\rangle \rightarrow_{1} \sigma^{\prime}}{\left\langle c_{0} \| c_{1}, \sigma\right\rangle \rightarrow_{1}\left\langle c_{1}, \sigma^{\prime}\right\rangle} \quad \frac{\left\langle c_{0}, \sigma\right\rangle \rightarrow_{1}\left\langle c_{0}^{\prime}, \sigma^{\prime}\right\rangle}{\left\langle c_{0} \| c_{1}, \sigma\right\rangle \rightarrow_{1}\left\langle c_{0}^{\prime} \| c_{1}, \sigma^{\prime}\right\rangle}
$$

$$
\frac{\left\langle c_{1}, \sigma\right\rangle \rightarrow_{1} \sigma^{\prime}}{\left\langle c_{0} \| c_{1}, \sigma\right\rangle \rightarrow_{1}\left\langle c_{0}, \sigma^{\prime}\right\rangle} \quad \frac{\left\langle c_{1}, \sigma\right\rangle \rightarrow_{1}\left\langle c_{1}^{\prime}, \sigma^{\prime}\right\rangle}{\left\langle c_{0} \| c_{1}, \sigma\right\rangle \rightarrow_{1}\left\langle c_{0} \| c_{1}^{\prime}, \sigma^{\prime}\right\rangle}
$$

this leads to ***nondeterminism***

# Guarded commands
Dijkstra's language of guarded commands uses a nondeterministic construction to help free the programmer from overspecifying a method of solution

$$
\begin{array}{l}{c::=\operatorname{skip} | \text { abort }|X:=a| c_{0} ; c_{1} | \text { if } g c \text { fi } | \text { do } g c \text { od }} \\ {g c::=b \rightarrow c\left|g c_{0}\right| \lg c_{1}}\end{array}
$$

$gc$ is called **alternative** 

$b_i$ is called **guards** 

If no guard evaluates to true at a state the guarded command is said to **fail**,

Otherwise the guarded command executes **nondeterministically** as one of the commands $C_i$ whose associated guard $b_i$ evaluates to true. 

$\mathbf{if }\; gc\; \mathbf{fi}$  executes as the guarded command gc, if gc does not fail, and otherwise acts like abort.

$\mathbf{do }\; gc\; \mathbf{od}$  executes repeatedly until $gc$ fails



## rules for guarded commands
$$
\frac{\langle b, \sigma\rangle \rightarrow \text { true }}{\langle b \rightarrow c, \sigma\rangle \rightarrow\langle c, \sigma\rangle}
$$

$$
\frac{\left\langle g c_{0}, \sigma\right\rangle \rightarrow\left\langle c, \sigma^{\prime}\right\rangle}{\left\langle g c_{0} \| g c_{1}, \sigma\right\rangle \rightarrow\left\langle c, \sigma^{\prime}\right\rangle} \quad \frac{\left\langle g c_{1}, \sigma\right\rangle \rightarrow\left\langle c, \sigma^{\prime}\right\rangle}{\left\langle g c_{0} \| g c_{1}, \sigma\right\rangle \rightarrow\left\langle c, \sigma^{\prime}\right\rangle}
$$


$$
\frac{\langle b, \sigma\rangle \rightarrow \text { false }}{\langle b \rightarrow c, \sigma\rangle \rightarrow \text { fail }} \quad \frac{\left\langle g c_{0}, \sigma\right\rangle \rightarrow \text { fail }\left\langle g c_{1}, \sigma\right\rangle \rightarrow \text { fail }}{\left\langle g c_{0} | g c_{1}, \sigma\right\rangle \rightarrow \text { fail }}
$$

> **IIQUESTION** How to understand the rules for alternatives? One Command can come to different results

> From the rules for guarded commands it can be seen that in transitions (ge, tJ) --+ (e, d) which can be derived the state is unchanged, but the extra generality will be needed when later we extend the set of guards to allow them to have side effects (从这里的定义来看gc到c的过程只是选择了一个c，所以$\sigma' = \sigma$, 但是由于后面可能计算b的时候有副作用？所以这里写得宽松一点)

## exercises

the exercises are about big-step semantics and axiomatic semantics very cool.


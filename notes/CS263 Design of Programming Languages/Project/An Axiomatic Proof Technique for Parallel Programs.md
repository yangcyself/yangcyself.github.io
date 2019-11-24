# An Axiomatic Proof Technique for Parallel Programs
## CUE


## summary
**PL 的 axiomatic semantics 基础**


> 文中假设所有的单个statement都是不可分割的, 这可以很简单的实现, 比如把`a = a + a^2`(计算`a^2`与`+a`之间可能`a`被改变了，但是我们为了方便分析不允许这样的发生) 写成  `t = a^2; a = a + t`. 
## Add two operations

### cobegin
$$
\text { cobegin } S_{1} / / S_{2} / / \ldots / / S n \text { coend }
$$
$S_i$ executes in parallel

**axiomatic rule**
$$
\text { await } \quad \frac{\{P \wedge B\} S\{Q\}}{\{P\} \text { await } B \text { then } S\{Q\}}
$$


### awaits
$$
\text { await } B \text { then } S
$$

- wait for condition $B$
- $S$ is indivisible statement
- if two or more wait for $B$, then one of them proeceed

**axiomatic rule**
$$
\text { cobegin }\left\{\frac{\left.P_{1}\right\} S_{1}\left\{Q_{1}\right\}, \ldots,\{P n\} S n\{Q n\} \text { are interference-free }}{\left\{P_{1} \wedge \ldots \wedge P n\right\} \text { cobegin } S_{1} / / \ldots / / S n \text { coend }\{Q 1 \wedge \ldots \wedge Q n\}}\right.
$$

## defn of interference-free

Proof $\{P\} S\{Q\}$ and statement $T$ with $pre(T)$, T does not interfere with ... iff
- $\{Q \wedge \operatorname{pre}(T)\} T\{Q\}$
- Let $S'$ be any statement within S but not within an await. then $\left\{p r e\left(S^{\prime}\right) \wedge p r e(T)\right\} T\left\{p r e\left(S^{\prime}\right)\right\}$


**interference-free**

$\{P 1\} S 1\{Q 1\}, \ldots,\{P n\} S n\{Q n\}$ are interference-free iff

let $T$ be an **await** or **assignment statement** (which does not appear in an await) of process $S_i$. and T does not interfere with $\{P_i\} S_j \{Q_j\}$. $\forall i,j$

>**Note**: At the end there is the version which determines the **termination**

## AV auxilary variable
只有赋值过程没有使用的变量

### Auxiliary variable trans/ormation
有 AV和没有AV的程序的hoare triple应该一样
$$
\frac{\{P\} S^{\prime}\{Q\}}{\{P\} S\{Q\}}
$$

## applications
### **Semaphores:**
replace `P(empty)` with `await empty > 0 then begin empty:= empty-1; P_empty : = P_empty + 1 end;`

Note `P_empty` is the AV for counting the lock

and replace `v (full);` as `await true then begin full := full+ 1 ;V_full := V_full + 1 end;`

### **block and deadlock**
***free from deadlock*** if no execution of S which begins with P true ends in deadlock.


**Theorem**
we are going to give sufficient condition for free of dead-lock

S: a statement

$A_j$: (direct **awaits**) the awaits of S which do not occur within cobegins of $S$

 $A_{j}: \text { await } B_{j} \text { then } \ldots$

> direct **awaits** 这个说法是我起的， 意思就是想象一个大程序是一个由各种 cobegin 构成的hierarchy，一个树。直接属于这个节点的 **awaits** 就是direct awaits

$T_k$: cobegins of S which do not occur within other cobegins of S 

$$
T_{k}: \text { cobegin } S_{1}^{k} / / S_{2}^{k} / / \ldots / / S_{n_{k}}^{k} \text { coend }
$$

define
$$
D(S)=\left[\bigvee_{j}\left(p r e(A_j) \land \neg B_{j}\right)\right] \lor \left[\bigvee_k D_{1}\left(T_{k}\right)\right]
$$

这里面$D(S) = false$ 就代表S不可能被block掉，前面关于$A_j$的或，意思是所有的direct awaits都不会被block。 后面也是说所有的direct cobegin不会被block

define
$$
D_1(T_k)=\left[\bigwedge_{i}\left(post(S_i^k) \land \lnot  D(S_i^k)\right)\right] \land \left[\bigvee_i D(S_i^k)\right]
$$

同样研究什么时候$D_1(T_k) = false$. 前面的意思是一个cobegin子线程停着等待有两种可能，一个是结束了但是在等别人（$post(S_i^k)$），一个是被block了。 还有后面那一项$\left[\bigvee_i D(S_i^k)\right]$意思是所有的线程都不可能发生等待（对应所有线程都执行完了的情况），这些情况取and，也就是只要有子线程能走得通，A就不会被卡住

原文：then each of its processes $S_i^k$ has terminated or is blocked, and moreover, at least one of its processes $S_i^k$ is blocked. 


> 上面只是直觉的理解，但是还不能解释为什么pre 和 post在这里可以代表执行完了或者还未执行？为什么他们可以和D取交或者并？



> **EXAMPLE OF PROOF FOR DEADLOCK-FREE OF 4.7** didnot understood

## another exmaple about the number of blocked process
For the program
```txt
s:=m; ...
cobegin S1 // ... // Sn // Sp coend
```
where each Si, i<=n has the form given below, none of the processes Si, i>n, reference s.
Si:
```txt
while true do
    begin noncirtical section;
    P(s);
    critical section;
    V(s);
    noncritical section
```

**we can prove**
1. at most $n-m$ of the processes can be blocked
2. if a process is blocked at P(s), then m processes are in the critical section

**method**, find the an invariable
$$
I \equiv s=m-\sum_{i=1}^{n} I N C i \wedge(\forall i, 1 \leqq i \leqq n, 0 \leqq I N C i \leqq 1)
$$


Then we prove:
0. the $INC_i$ and assertion $I$ always holds because interference-free
1. $n-m+k$ processes blocked $\Rightarrow$ $s>0$, which is contradictory to the block $\Rightarrow$ $s = 0$
2. only $m-k$ process are in critical section $\Rightarrow$ $s>0$, a process is blocked $\Rightarrow$ $s\leq 0$

## Consider termination
We have to add another condition to the defn of *not interfere*
- Let W be a loop within S, but not within an await of S. Let t be the integer function used in the proof of correctness of the loop. Then $\{t=c \wedge p r e(T)\} T\{t \leqq c\}$
  - Note here the $t$ is like $\{P \wedge B\} S\{P\}, t \geqq 0, \text { wdec }(P \wedge B, S, t)$ or $\{P \wedge B\} S\{P\}, \text { wdec }(P \wedge B, S, t),(P \wedge t \leqq 0) \Rightarrow \neg B$

> where $w d e c(Q, S, t) \equiv\{Q \wedge t=c\} S\{t<c\}$
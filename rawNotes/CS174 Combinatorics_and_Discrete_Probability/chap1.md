# CUE
- The counter intuitive of independence
- the algorithm and probability of checking funcitons
- the algorithm and probability of verifying matrix multiplication
- the algorithm and probability of A Randomized Min-Cut Algorithm 
  - prove after repeat it for how many times, the probability can be reduced to $\frac{1}{n^2}$

# summary

# review of probability.
## independent
**By the definition of independence, events do not have to be intuitively independent to be independent**
比如产生两个随机数，每个的范围是 1-3， 如下两个事件

```txt
0 ! 0
- f -
0 ! 0
```

（这是老师说他很喜欢的思考方式），其中横着的表示第一个变量的取值， 竖着的是第二个变量的取值。这里面`-` 和`!` 代表个事件 `f`代表它们的交集。很显然上面的两个事件是independent的

但是下面的这个也是两个独立的事件（虽然不好理解），根据定义
```txt
0 ! ！
0 f -
0 ! -
```

definition:
$$
\operatorname{Pr}(E \cap F)=\operatorname{Pr}(E) \cdot \operatorname{Pr}(F)
$$

mutually independent: for any subset $I$, that 
$$
\operatorname{Pr}\left(\bigcap_{i \in I} E_{i}\right)=\prod_{i \in I} \operatorname{Pr}\left(E_{i}\right)
$$

## sampling with and without replacement

> sampling with replacement is significantly easier to analysis (book,p8)


# Some simple probabilistic algorithms

## why do we need probabilistic algorithms?
In old times, calculation is expensive. Probabilistic algorithms is simpler

Nowadays, programming is expensive. Probabilistic algorithms is simpler to write

## Checking the equivalence of two functions.

algorithm: find a random number from [1,100d] and calculate the result of both side

the probability of failure, less than 1/100

how to improve: increase 100, or more times.

## verifying matrix multiplication
test that AB=C
 
for convenience, assume that we are working over **the integers modulo 2**

we can randomly choose a vector $r$ to test it.

theorem: if $AB \neq C$ and if r is chosen uniformly at random from $\{0,1\}^n$ then 
$$
\operatorname{Pr}(\mathbf{A B} \overline{r}=\mathbf{C} \overline{r}) \leq \frac{1}{2}
$$

proof: first prove choosing from $\{0,1\}^n$ is equivalent to choosing those independtly

is this way, we can use **deferred decisions**


## A Randomized Min-Cut Algorithm 
algorithm:  The main operation in the algorithm is edge contraction. In contracting an edge {u, v} we merge the two vertices u and v into one vertex, eliminate all edges connecting u and v, and retain all other edges in the graph. 

probability:  The algorithm outputs a mill-cut set with prohability at least 2/n(n - 1). 

Proof: (P26) hint: bound the degree of each vertex given the cardinality of mincut set

### analysis:

if we do $n(n-1)\log n$ times, the probability is $\frac{1}{n^2}$  

proof:
$$
(1-\frac{2}{n(n-1)})^{n(n-1)\log n} \leq e^{-2\log n} = \frac{1}{n^2}
$$

**trick**:

$e^{-x} = 1 - x + \frac{x^2}{2!} - ...$
thus
$x < 1 \; 1-x \leq e^{-x}$






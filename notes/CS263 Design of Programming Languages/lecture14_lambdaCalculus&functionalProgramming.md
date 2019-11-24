# CUE
- what is the church turing thesis?
  - So use this thesis to informaly prove that you cannot always find normal form for every expression
- what is difference between syntatically equivalent and semantically equivalent?
  - give examples 
- what is the difference of defn between normal form and *canonical form*
- what are the three typical evaluation strategies that can be expressed by $\lambda$ calculus
- What is the normal order?
- what is a good theorem about it?
- why does no popular programming language uses normal order?
- How to express 'don't evaluate under $\lambda$' with rules?
- what are the rules for call-by-name?
- what is the name of the strategie of call-by-name with memorization
- What is the termination behavior CBN? is it easier or harder to terminate than normal order?
  - give example to show it
- compare to other strategies and show why CBN can support infinite data structures such as stream?
- why it is harder to predict the order of the evaluation?
- what are the rules for Call by Value?
- this is easier to terminate or harder than normal order?
- express boolean with lambda functions
- express pair with lambda functions
- express natural number with lambda functions
- express succ with lambda functions
- express add with lambda functions
- express mult with lambda functions
- express iszero with lambda functions
- express pred with lambda functions
- express the **Fixed-point** combinator
- express the function that calculates the factorial?
# some recap from last lecture

**You cannot find normal form for every expression**

> turing was a student of church(see last note who is church)\
> The **church turing thesis**: lambda expression and turing machine have equal experssiveness\
> This means: for a lambda express have normal form -> cannot reduction further <=> cannot evaluation further <- program terminate

## the significance of the corollary

> if $e \rightarrow _{\beta}^* e_{1}$ and $e \rightarrow _{\beta}^* e_{2}$ and $e_{1},e_{2}$ are normal forms then, $e_{1},e_{2}$ identital 

Note that here the identital is **syntatically identital** 

>Thus, the **canonical form** is: something uniquely(syntatically) normal

Note this equivalent is not always hold, exmaple `2*x` and `x+x`, they semantically equivalent but syntatically not.

## strategies for evaluation

the process deciding which rule to use and when

> and they are corresponding to real life PLs

- normal order
- call by name
- call by value

# strategies for evaluation

## normal order
**Normal order always reduces the leftmost outer most redex first**

Theorem: If e has a normal form e' then normal order reduction will reduce e to e'

### **No popular programming languages uses normal order**

we do not evaluate a function body until we apply the function

$$
\lambda x .(\lambda x . x x)(\lambda x . x x)
$$

in normal order, this function body will get evaluated.

## call-by-name

Don't reduce under $\lambda$
$$
\overline{\lambda x . e \rightarrow_{n}^{*} \lambda x . e}
$$
> see this rule, the function itself is always reduced to itself (it is never reduced)


Don't evaluate the argument of a function call
$$
\frac{e_{1} \rightarrow_{n}^{*} \lambda x . e_{1}^{\prime}\left[e_{2} / x\right] e_{1}^{\prime} \rightarrow_{n}^{*} e}{e_{1} e_{2} \rightarrow_{n}^{*} e}
$$
> in this rule, if there is a function calling redex, directly put all argument(without evaluate it) into the function.


Call-by-Name is demand-driven: expressions not evaluated unless needed

Lazy evaluation('***Call-by-Need***') is **Call-by-Name** with memoization.
– Same termination behavior
– Just an optimization

> the example of this is Haskel


### The termination

For any expression, if normal order evaluation converges, CBN terminates.

However CBN may not find normal forms, It terminates more often than normal order

For example:
$$
\lambda y .(\lambda z . zz)(\lambda x . x x)
$$
CBN will terminate here(because there is no outer function calls), but normal order will not terminate(because there is still redex)

For example:
$$
\lambda y .(\lambda z . z)(\lambda x . x x)
$$
CBN will terminate at here, but normal order will terminate at 
$$
\lambda y .(\lambda x . x x)
$$
### considerations
- More difficult to implement
- **Allows infinite data structures (e.g., streams)**
- The order of evaluation is harder (impossible?) to predict
- Extremely difficult to reason about space complexity
  - [II]??

## call-by-value
The calling method of most programming languages C, Java, python

> when you have a stack, you know what you are pushing onto the stack, they are values.

Similar to CBN, call by value don't reduce under lambda

$$
\overline{\lambda x . e \rightarrow_{v}^{*} \lambda x . e}
$$

Do evaluate the arguments to a function call

$$
\frac{e_{1} \rightarrow_{v}^{*} \lambda x . e_{1}^{\prime} \;e_{2} \rightarrow_{v}^{*} e_{2}^{\prime}\;\left[e^{\prime}_{2} / x\right] e_{1}^{\prime} \rightarrow_{v}^{*} e}{e_{1} e_{2} \rightarrow_{v}^{*} e}
$$

>Note the difference between this rule and the corresponding to CBN
>$$
>\frac{e_{1} \rightarrow_{n}^{*} \lambda x . e_{1}^{\prime}\;\left[e_{2} / x\right] e_{1}^{\prime} \rightarrow_{n}^{*} e}{e_{1} e_{2} \rightarrow_{n}^{*} e}
>$$

> the difference is just $e_{2} \rightarrow_{v}^{*} e_{2}^{\prime}$

this represents to evaluate the expression $e_2$ before calling $e_1$



### normalizing:
for example:
$$
(\lambda x. \lambda y . y)((\lambda x . x x)(\lambda x . x x))
$$

CBV will not normalizing this, it will stuck at evaluating the argument of the function$(\lambda x . x x)(\lambda x . x x)$

However the normal order and CBV can terminate and get the normal form $\lambda y.y$

CBV diverges more often than normal order or CBN, but it acts the way most programmers expect

### considerations

- easy to implement
- well-behaved (predictable) with respect to side-effects

## Other parameter passing mechanisms
they cannot be naturally expressed in the lambda calculus
- by reference
  - lambda calculus has no notion of reference
- value-result
  - the function return not only the value but also the result of the side effects?


# $\lambda$ calculus and functional programming

it is a prototypical functional language:
- no side effects
- several evaluation strategies
- lots of functions
- **nothing but functions (pure lambda-calculus does not have any other data type)**

In a functional language, variables are never updated, **they are just names for expressions or values**. 

thus if ML `let x = e1 in e2` is like $(\lambda x.e_2)e_1$

## the expressiveness
- data types (integers, booleans, lists, trees, etc.
- branching
- recursion

## encodes turing machines
*church encoding* of a datatype

**The general idea**: encodes the constructs using only functions


### **Boolean**

boolean means selection
so 
$$
\text{true: } \lambda x . \lambda y . x \qquad \text{False: } \lambda x . \lambda y . y
$$

example: the `if true then u else v` is 
$$
(\lambda x. \lambda y. x) u v
$$



### **Pairs**
pair is a function that given boolean gives its content

thus,
$$
(x,y) =_{\text{def}} \lambda b.b xy
$$

$$
\begin{array}{ll}{\text { fst } p} & {=_\text { def } p \text { true }} \\ {\text { snd } p} & {=_\text { def } p \text { false }}\end{array}
$$

where $b$ is a boolean.

### **Natural Numbers**
The natural number can mean the times of a repeatition

thus 
$$
\begin{array}{l}{0=\operatorname{def} \lambda f . \lambda s . \mathrm{s}} \\ {1=\operatorname{def} \lambda f . \lambda s . f s} \\ {2=\operatorname{def} \lambda f . \lambda s . f(f s)}\end{array}
$$

> called Church numerals
> also called Peano representation

>so a natural number `n` is given a function and argument, you apply the function `n` times

### **successor of number**
succ means you apply this one more time
$$
\operatorname{succ}n=_{def} \lambda n . \lambda f . \lambda s . f(n f s)
$$
or 
$$
\operatorname{succ}n=_{def} \lambda n . \lambda f . \lambda s . nf(f s)
$$

### **addition of number**
to add $n_1$ and $n_2$ means succ on $n_2$ for $n_1$ times
$$
\text { add } n_{1} n_{2}=_{def} n_{1} \operatorname{succ} n_{2}
$$

here 

### **multiplication**

$$
\text { mult } n_{1} n_{2}=_{\text {def }} n_{1}\left(\text { add } n_{2}\right) 0
$$

> here note `add n2` that a beauty of $\lambda$ function is that when you pass one argument in a two argument function, it becomes a one argument function

> recall that `succ` takes three arguments (the $\lambda n.\lambda f.\lambda s$ part). However, the last two argument is the argument to form a number, so when it is applied the first argument, it is the succ

> here `add n2` becomes a one argument function operate on a natural number(actually, it is $\lambda n.n_2 \operatorname{succ} n$, and if we enroll thee $n_2$ and $n$ with $s,t$ there will be more arugments). 


### **testing 0**

$$
\text { iszero } n=_{\text {def }} n(\lambda b\text { . false) true }
$$

## partial evaluation exmaple
consider `add 0`

$$
\left(\lambda n_{1} . \lambda n_{2} . n_{1} \operatorname{succ} n_{2}\right) 0
$$
so this get 
$$
\lambda n_{2} .0 \text { succ } n_{2} 
$$

which is (unroll 0)
$$
\lambda n_{2}.(\lambda f.\lambda s.s) \text { succ } n_{2} 
$$

get (evaluation in the body)

$$
\lambda n_2.n_2
$$

So with this we can **express some optimizations**
- but we need to reduce under the lambda
- > contract this with the evaluation order we just saw



## Pred of number
> 2019-11-16 18:52:47 finally, I finally worked this out by myself! After a whole week!

The idea is to call something like `succ` n times. I have to design a state to act as a "buffer", so that it only add1 on the number n-1 times.

So, A tuple with a boolean and a number is the ideal object.

$$
\text{pred } n = \Big[ n\Big( \lambda p. (pF)(\lambda b.b(\text{succ }(pT))T)(\lambda b.b0T) \Big)\Big(\lambda b.b0F \Big) \Big] (T) 
$$

> $T$ is true and $F$ is false

To understand this, we are calling a function $n$ times, the input and output of this function are tuples, and have the following transformation.

$$
(0,F) \rightarrow (0,T)\rightarrow (1,T)\rightarrow (2,T)\rightarrow \dots \rightarrow (n-1,T)
$$

## Encoding recursion

example: factorial function

`fact n = (iszero n)1(mult n (fact (pred n)))`

we have this recursive form but now we cannot put it into $\lambda$ expression
> we have not explicitly written out `fact`\
> all other things `iszero`, `mult`... are $\lambda$ functions, but here `fact` is just a function name (there is no function name in $\lambda$ calculus)

let $Y = \lambda f .(\lambda y . f(y y))(\lambda x . f(x x))$

then 
$$
Y f n = f(Yf)n
$$

to prove, check 
$$
Y f n \rightarrow 

(\lambda y . f(y y))(\lambda x . f(x x)) n\\
\rightarrow f((\lambda x . f(x x))(\lambda x . f(x x)) n \\\text{ (this is by substituting the second part into the first part)}\\
\rightarrow f(Yf) n
$$

So Y is called **Fixed-point** combinator

Given any function in $\lambda$-calculus we can compute its fixed-point

Then $\text{fact } n = Y F n$
where 
$$
\mathrm{F}=\lambda \mathrm{f} . \lambda \mathrm{n} \text { . (iszero } \mathrm{n}) 1(\mathrm{mult}\; n(\mathrm{f}(\mathrm{pred} n)))
$$

>Note that the $F$ takes as first argument a function to recall, it is itself.


> Note that for the $Yfn$, if we always evaluate the function body first $(Yf)\rightarrow f(Yf)$, then we might get untermination evaluation. However, luckily, normal-order, call-by-name, call-by-value, don't have this kind of problems. Because they don't evaluate inside the function body with argument given before putting the argument in.

> A [company](https://en.wikipedia.org/wiki/Y_Combinator) is called **Y Combinator,** just named after this Y combinator


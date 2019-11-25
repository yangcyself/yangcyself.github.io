# CUE

# Verification Conditions for Program Transformations
## program transformation:
比如我有一个JAVA写的函数，我如何给他转成spark的形式(函数编程语言，十分方便做并行等分析), 传统方法基于写规则，然后做模式匹配，匹配上了之后改写代码

但是这样过于麻烦

## USE verification conditions to prove 
思路:

在JAVA和spark中间找一个语言，选取的是一个由map reduce构成的语言， 从map reduce到spark 很方便，

所以整个的流程是，从java代码里面得到它后面的输出条件，也就是$\left\{A \right\}c\left\{B \right\}$里面的B, 然后使用Program synthesizer来生成map reduce的语言

program synthesizer的基本功能是，给定
1. Expression grammar（搜索空间）
2. Verification conditions（需要满足的约束）
给你输出一个语言

这里面verification conditions就是
- Invariant is true initially
- Invariant is preserved
- Invariant implies post condition


# A denotational semantics for SQL
内容是需要找到一个SQL的denotational semantics， 而不是根据自然语言的描述。

however:

Deciding the equality of two queries are undicidable in general.

Many decidable fragments exits


## denotation 的思路
K-relation on Homotopy type

### K relation
$$
\llbracket R \rrbracket: \text{tuple} \rightarrow K
$$
这里面的意思也就是一个query，的结果是一个函数，这个函数是输入一个relation（表中一行），输出一个数字，表中一共有多少个这样的行 multiplicity of tuple

所以，这个是不同domain中的转化，从SQL的操作转化到数学domain中

We can prove equivalences using algebraic rewrites
# CUE
Let $X$ and $Y$ be sets, show that there is one-to-one correspondence
$$
X \rightarrow \mathcal{P}(Y) \text { and } \mathcal{P}(X \times Y)
$$
## problem
Let $X$ and $Y$ be sets, show that there is one-to-one correspondence

$$
X \rightarrow \mathcal{P}(Y) \text { and } \mathcal{P}(X \times Y)
$$

## answer
**idea:**

**excibits mappings between the two sets**

$$
\theta_{1}(f)=\{(x, y) | x \in X \text { and } y \in f(x)\}
$$

$$
\theta_{2}(A)(x)=\{y |(x, y) \in A\}
$$

and then show that $\theta_1\circ\theta_2$ and $\theta_2\circ\theta_1$ are identity funcitons
$$
\theta_{1}\left(\theta_{2}(A)\right)=\{(x, y)|y \in\{y |(x, y) \in A\}\}=\{(x, y) |(x, y) \in A\}=A
$$

$$
\theta_{2}\left(\theta_{1}(f)\right)(x)=\{y|(x, y) \in\{(x, y) | y \in f(x)\}\}=\{y | y \in f(x)\}=f(x)
$$

我当时的做法是: 没有后面的证明identity对应的步骤，但是是证明的两边都是单一映射。 但是构造的过程十分的繁琐，写了好久，还不如这样简介明了。
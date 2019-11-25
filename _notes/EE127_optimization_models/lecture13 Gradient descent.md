# CUE
- How to find a descent direction
- what is the step $v_N$ of the newton method?
- algebric understanding of the second-order method
# review
when ask you to show a program is convex, you show that the problem can be written as 
$$
\min_x  f_0(x)\\
s.t. f_i(x)<0
$$

you maybe need to get rid of inacitive unconvex constraints

## gradient descent


```md
start a guess: x0
    advance x:
    xk+1 := xk + ()
    check good enough?
stop
```

### How to find a descent direction

$$
f(x_k + v) = f(x_k+\alpha d)\\
    = f(x_k)+   \alpha \nabla f^T(x_k) d + \dots
$$
(Tayler expansion)

How to choose direction

$$
d^* \; s.t. \; d^{T*}  \nabla f(x_k) = \nabla f(x_k)^T d^* <0
$$


if you pick $\alpha >0$

$$
d^* = - \frac{\nabla f(x_k)}{\left\|\nabla f(x_k) \right\|_2 }
$$

this is the steepest descent

#### decent method does not solve two problems
- gradient problem
- step-size problem



## second-order method
solve the above problem

Do second order approximation instead of the first order approximation



$f()$ is in general non linear, non ..

$\hat{f}$  the scecond order approximation


$$
\hat{f} = f(x_k+v)\\
= f(x_k)+ \nabla f(x_k)^Tv + \frac{1}{2}v^TH(x_k)v + ...
$$



How to find the min of $\hat{f}(v)$

take the derive, let the gradient be zero

$$
 f(x_k)+ \nabla f(x_k)^Tv + \frac{1}{2}v^TH(x_k)v + ...\\
0 = 0 + \nabla f(x_k)^T + H(x_k)v + ...
$$
solution
$$
v_N = -H(x_k)^{-1} \nabla f(x_k)
$$
> why is the hessian always invertable
**this $v_n$ tells exactly how much to move**

Newton's algorithm

```markdown
start at x0
    repeat
    $x_{k+1}$ = $x_k$ - H^{-1}(x_k)\nabla f(x_k)
    if good enough stop
    other
```

**question**    
why not directy compute the derivative of the whole function and find the root?



second order is just an improvement of the approximation

**it is the first order method of the gradient**

>II we can think about this using the first order method of gradient

画一下图像表示！\
上面是f(x) 下面是f'(x)\
然后f(x)的最小值点是f'(x)和零的交点，牛顿法是每一次在f'(x)取切线然后移动到下一个root

>Professor: you can introduce an alpha and do the line search, but it is epxensive

## Example
 
$$
f(x) = \frac{1}{2}\left[ x_1^2+\gamma x_2^2 \right]
$$

gradient method 无数步逼近

newton method 一步！

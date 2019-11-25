# CUE

# prove convex
Good hygine


the more standard form
$$
\min_x   f_0(x)\\
\text{s.t.}\quad f_i(x)
$$

prove that this is convex
- $f_0(x)$ is convex
  - the domain is convex
  - > there will be a problem in MT that the domain is not convex
  - the function is convex
- then the same to $f_i(x)$

> **YOU have to explitly show it in convex form**

>is the original question convex?
>> NO\
> but we can transform it into convex problem

# Srewing up an SOCP
No NOT DO IT

for a SOCP constraint
$$
\left\|x \right\|_2 \leq x_{1} + 2x_{2} 
$$

then, if you
$$
\left\|x \right\|_2^2 \leq( x_{1} + 2x_{2} )^2
$$

Trouble
$$
x_{1}^{2} + x_{2}^{2} \leq x _{1}^{2} + 4 x_{1} x_{2} + 4x_{2}^{2}  \\
0 \leq x_{2} [4x_{1}+3x_{2}  ]
$$
then you get the cone where $x_{2}$ can be negtive, this is not convex

> what happend here is, in the square operation, you lost the implicit constraint that $x_{1} + 2x_{2} \leq 0$

if you have to square something, DO THAT INEQUALITY

# NOTE

is a cone convex? ingeneral?

**NO**

that 
$$
f(x) = \max _{\alpha \in A}f_\alpha (x)
$$

we do not need $A$ to be a convex set

Not say "**The** minimizer" unless it is unique

Do say "the optimum" when it is convex

You can draw something to say sth like "bounded", that's fine

**when prove that equ con -> inequ cons**

show that **no relexation gap**

**Write the defn of a rotated cone in the cheat sheet**

**Write a little column of the reductions of LP, QP to SOCP** 

if we ask inventory control is convex?

you can compute hessian(about 3 lines), but you can say its SOCP (simple one line)

Put the chance constraint into you cheatshett


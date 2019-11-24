# CUE
- what is the difference between spreading loss and attenuation loss?
- if f and h are separable, then how to compute f**h?
- what is the result of the delta blade?
  - f(x,y) ** \delta(x-x_0)
# LSI 2D

the two kinds of losses in our class:
- spreading loss
  - 这个应该只是在真空中传播导致的loss
- attenation loss
  - 这个是被人体吸收导致的loss，一般需要交流电磁场

# separability and its applicaiton

**Important:** 
if $h(x,y),f(x,y)$ is separable, $h(x,y) = h_1(x)h_2(y) ... $
and 

then 
$$
f(x,y) ** h(x,y) = h_1(x)*f_1(x) \times h_2(y)*f_2(y)
$$

note that the multiply in the middle

## the delta blade
consider 
$$
f(x,y) ** \delta(x-x_0)
$$
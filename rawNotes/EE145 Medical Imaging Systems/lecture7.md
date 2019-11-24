# CUE
- when we are sampling in K space, what should be the limit of the frequency
- compute the matrix of convolution in discrete space
# some recap about sampling theorem
when we are sampling in K space, what should be the limit of the frequency
$$
\Delta K\leq \frac{1}{x_0} \equiv\frac{1}{\text{FOV}}
$$
where FOV is the field of view

**如何理解:**  如果K不够细的话，在整个FOV里面就会有周期信号

ideal interpolation
$$
f(x) = \sum f(n\Delta x)\operatorname{sinc}\left( \frac{x-n\Delta x}{\Delta x} \right)
$$

# convolution in discrete space
$$
f(x)*h(x) = \int_{0}^{\infty}f(x)h(x-u)du
$$

## Toeplitz matrix
$$
\left[\begin{array}c 
h_0 & h_1 & h_2 & h_3 & ... \\
h_{-1} & h_{0} & h_1 & h_2 & ...\\
h_{-2} & h_{-1} & h_0 & h_1 & ...\\
...
 \end{array}\right] 
$$

Note:

recasting the convolution problem into matrix problem does no help to improve the tractability

### conditional number
suppose condition number is 1

then, $\hat{x}$ has no noie gain

**P-inverse**: I only want three singular value

## FFT
$$
F(\Delta k) = \sum(fn\Delta x)e^{-i2\pi \frac{mn}{x}}(\frac{2L}{N})
$$

then the matrix form will be 

F0 is whole One, 

F1 is one sin wave

F2 is two sin wave..
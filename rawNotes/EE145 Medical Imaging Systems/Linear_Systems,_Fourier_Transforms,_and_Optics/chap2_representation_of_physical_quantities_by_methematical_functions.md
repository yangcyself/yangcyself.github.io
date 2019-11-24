# CUE
- separable of two dimensional function
- modulus, argument phase of complex number
- hermetian of a phasor
- representation and simplification of Phase Modulation(PM)
- representation of Monochromatic light
- derivation of wave equation
# Summarise

# contents
....

### almost periodic
the sum of two periodic signal whose ratio is not all rational number

## two dimensional function
### separable
A two-dimensional function is said to be separable in a particular coordinate system if it can be written as the product of two one-dimensional functions, each of which depends only on one of the coordinates
$f(x,y) = g(x)h(y)$

we shall make extensive use of their properties later when we discuss two-dimensional convolution and two-dimensional Fourier transforms

## complex numbers and phasors
complex number, real number, imaginary number
real and imaginary parts: Re{u}, Im{u}

absolute value (modulus)

$\phi$: *argument*, *phase*

*complex conjugate* of complex number

### phasors
denote a complex exponential function of constant modulus and linear phase, a function with purely harmonic behavior. 

***hermetian***: a phasor, whose real part iis an even function and whose imaginary part is odd 
..... odd .... even is called *antihermetian*

a Hermitian function is a complex function with the property that its complex conjugate is equal to the original function with the variable changed in sign

# representation of physical quantities
**signal**

### phase modulation(PM)

$$ \phi(t)=2 \pi \nu_{c} t+\Delta \phi m(t) $$

instantaneous frequency
$$ \begin{aligned} \nu_{\mathrm{in}} &=\frac{1}{2 \pi} \frac{d \phi(t)}{d t} \\ &=\nu_{c}+\frac{\Delta \phi}{2 \pi} \frac{d m(t)}{d t} \end{aligned} $$

when taken nano band
$$ e^{j \Delta \phi m(t)} \cong 1+j \Delta \phi m(t) $$

$$ v(t) \cong \operatorname{Re}\left\{A[1+j \Delta \phi m(t)] e^{j 2 \pi \nu_{c} t}\right\} $$

which is nearly the same expression for an AM wave

## representation of Monochromatic light
**monochromatic light**: waves consisting of a single temporal-frequency component
$$ u(\mathbf{r}, t)=a(\mathbf{r}) \cos \left[2 \pi \nu_{0} t-\phi(\mathbf{r})\right] $$
**co-phasal surfaces**, **wavefronts**


The function is a solution of the scalar wave equation
$$ \nabla^{2} u(\mathbf{r}, t)-\frac{n^{2}}{c^{2}} \frac{\partial^{2} u(\mathbf{r}, t)}{\partial t^{2}}=0 $$




## the derivation of wave equation
The wave equation in the one-dimensional case can be derived from Hooke's Law in the following way: Imagine an array of little weights of mass m interconnected with massless springs of length h. The springs have a spring constant of k:

Here the dependent variable u(x) measures the distance from the equilibrium of the mass situated at x, so that u(x) essentially measures the magnitude of a disturbance (i.e. strain) that is traveling in an elastic material. The forces exerted on the mass m at the location x + h are:

$$
\begin{aligned} F_{\text {Newton }} &=m \cdot a(t)=m \cdot \frac{\partial^{2}}{\partial t^{2}} u(x+h, t) \\ F_{\text {Hooke }} &=F_{x+2 h}-F_{x}=k[u(x+2 h, t)-u(x+h, t)]-k[u(x+h, t)-u(x, t)] \end{aligned}
$$

If the array of weights consists of N weights spaced evenly over the length L = Nh of total mass M = Nm, and the total spring constant of the array K = k/N we can write the above equation as:

$$
\frac{\partial^{2}}{\partial t^{2}} u(x+h, t)=\frac{K L^{2}}{M} \frac{u(x+2 h, t)-2 u(x+h, t)+u(x, t)}{h^{2}}
$$

Taking the limit N → ∞, h → 0 and assuming smoothness one gets :
$$
\frac{\partial^{2} u(x, t)}{\partial t^{2}}=\frac{K L^{2}}{M} \frac{\partial^{2} u(x, t)}{\partial x^{2}}
$$

which is from the definition of a second derivative. KL2/M is the square of the propagation speed in this particular case.

For a problem $Ax = b$ we can do QR to get 
$$
A=Q R=\left[\begin{array}{ll}{Q_{1}} & {Q_{2}}\end{array}\right]\left[\begin{array}{l}{R_{1}} \\ {0}\end{array}\right]
$$

where Q is orthogornal and R is uppertriangle,

show that the residual r = b - Ax can be represented as 
$$
\|r\|_{2}^{2}=\left\|c_{1}-R_{1} x\right\|_{2}^{2}+\left\|c_{2}\right\|_{2}^{2}
$$

solution

$$
\begin{aligned} r &=b-A x \\ r &=b-Q R x \\\|r\|_{2}^{2} &=\left\|b-Q\left[\begin{array}{c}{R_{1}} \\ {0}\end{array}\right] x\right\|_{2}^{2} \end{aligned}
$$

$$
\begin{array}{l}{=\left\|Q^{\top}\left(b-Q\left[\begin{array}{c}{R_{1}} \\ {0}\end{array}\right] x\right)\right\|_{2}^{2}} \\ {=\left\|\left[Q_{2}^{\top} b\right]-\left[\begin{array}{c}{R_{1} x} \\ {0}\end{array}\right]\right\|_{2}^{2}} \\ {=\left\|\left[\begin{array}{c}{Q_{1}^{\top} b-R_{1} x} \\ {Q_{2}^{\top} b}\end{array}\right]\right\|_{2}^{2}} \\ {=\left\|\left(Q_{1}^{\top} b-R_{1} x\right)\right\|_{2}^{2}+\left\|Q_{2}^{\top} b\right\|_{2}^{2}}\end{array}
$$
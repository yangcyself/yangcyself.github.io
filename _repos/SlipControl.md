---
title: "Slip Control on planar RABBIT"
collection: repos
permalink: /publication/SlipControl
excerpt: 'This is the course project for Legged Robotics, we designed a controller to prevent slipping on a slippery surface of a double legged robot'
repodate: 2019-06-16

---
This is the course project for ME193 Berkeley Feedback control of legged robot. We implemented an anti-slipping controller on RABBIT.

The gif comparing robot with our controller and without.
![](https://github.com/yangcyself/TA_GaitDesign/blob/master/pics/compare_mu0.25.gif)

## Implementation

### Controller

#### Normal PD controller

Track the reference joint angle

$$
u_{PD}=-K_{P}\left(q-\hat{q}_{des}\right)-K_{D}\left(\dot{q}-\dot{\hat{q}}_{des}\right)
$$

#### ETH's method

Add impedance

$$
u_{E T H}=u_{W B C, r e f}-K_{P}\left(q-\hat{q}_{d e s}\right)-K_{D}\left(\dot{q}-\dot{\hat{q}}_{d e s}\right)
$$

Where WBC: Whole Body Controller and the $\hat{q}_{d e s} \dot{\hat{q}}_{d e s}$ comes from gait library or WBC

#### our method

When the stance leg slips, we want to “drag” it to the original desired place. 

The “drag force” is proportional to the toe slip velocity. 

We modify the reference trajectory for stance leg to cause “drag force”. 

$$
q_{\text {des}, s t}=\hat{q}_{\text {des}, s t}+K_{P}^{f f d} v_{\text {toe}, x}
$$
$$
\dot{q}_{d e s, s t}=\dot{\hat{q}}_{d e s, s t}+K_{D}^{f f d} v_{t o e, x}
$$
$$
u=-K_{P}\left(q-q_{d e s}\right)-K_{D}\left(\dot{q}-\dot{q}_{d e s}\right)
$$

### Reaction Force simulation

We assume the [Coulomb model of friction](https://mech.subwiki.org/wiki/Coulomb_model_of_friction). There are two cases for simulation:
- The reaction force is in the friction cone
- The reaction force is on the friction cone

Both are simulated by solving the dynamic model and rigid contact model together.

The dynamic model is:
$$
M(q)\ddot{q} = F(q,\dot{q}) + G(q) + Bu + J^{T} \Gamma 
$$

#### The reaction force is in the friction cone

This is the case of static friction, the constraint should be the fix of the ground contact point. As the reaction force $\Gamma$ is relatively second degree to this constraint, so the constraint we use is 

$$
\dot{(J\dot{q})} = \dot{J}\dot{q}+J\ddot{q} =0 
$$

Thus, we can simulate the dynamics and the reaction force together with the following equation

$$
\left[\begin{array}c 
M & -J^{T} \\
J & 0
 \end{array}\right] 
\left[\begin{array}c 
\ddot{q}\\
\Gamma 
 \end{array}\right]
 = 
 \left[\begin{array}c 
 G(q)+Bu\\
 -\dot{J}\dot{q}
  \end{array}\right] 
$$

#### The reaction force is on the friction cone

When the ground contact point is sliding or the reaction force under the static friction assumption is outside of the friction cone, then the friction is saturated. 

Then we assume that the $y$ direction of ground contact is fixed and the $sf_{x} = \mu f_{y}$. Where $s$ is the direction of the friction and $\mu$ is the friction coefficient.

We can solve the equation below

$$
\left[\begin{array}c 
M & -J^{T} \\
(J)_{y}  & 0\\
0 & 
\begin{array}c s & -\mu  \end{array}
 \end{array}\right] 
\left[\begin{array}c 
\ddot{q}\\
\Gamma 
 \end{array}\right]
 = 
 \left[\begin{array}c 
 G(q)+Bu\\
 (-\dot{J}\dot{q})_{y} \\
 0
  \end{array}\right] 
$$


#### The unilateral constraint

After computed one of the above cases, we have to check the unilateral constraint. If the $f_{y}<0$, we directly set $f=0$ and recomputed the $\ddot{q}$


## experiments

|  $\mu$  | their controller|their result | our controller | our result
| ---- | ---- | ---- | ---- | ---- |
| 0.55 |  105, 0.6|   |   0.05,0.02  |yes 5/5|
| 0.30 |  105, 0.6|   |   0.05,0.02  |yes 5/5|
| 0.25 |  105, 0.6|   |   0.05,0.02  |yes 5/5|
| 0.15 |  105, 0.6|   |   0.05,0.02  |yes 5/5|
| 0.10 |  105, 0.6|   |   0.05,0.02  |walk long double stand  5/5|
| 0.05 |  105, 0.6|   |   0.05,0.02  |double stand 1/5|
|      |      |      |
> Their controller is the Kp and Kd, our controller is their Kp and Kd adding feedforward with $q$ and $dq$\
> The value in result is the amount of steps in experiment\
> The above result is get under the condition that zero react force above 1e-2\
> Deprecated

**changed the no-force height to 1e-5**

|  $\mu$  | their controller|their result | our controller | our result
| ---- | ---- | ---- | ---- | ---- |
| 0.55 |  105, 0.6|   |   0.05,0.02  |yes 5/5|
| 0.25 |  105, 0.6|   |   0.05,0.02  |yes 15/15|
| 0.15 |  105, 0.6|   |   0.05,0.02  |walk long double stand 3/5|


[The Link To the Github Repository](https://github.com/yangcyself/TA_GaitDesign)
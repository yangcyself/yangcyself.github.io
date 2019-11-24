# CUE
# basis
## machanical types configuration
two kinds of joints
-  prismatic joints -> linear motion
-  revolvte joints -> rotational

machanical types configuration
- Cartesian: PPP -> Gantry type
- Cylindrical: RPP  
- spherical: RRP -> SCARA
- anthropomorphic(拟人): RRR

**work space:** reachalbe space of robots
- dextrous workspace: volume of space where the end effector can be arbitralily oriented
- reachable workspace: volume of space where robot reaches
## manipulator kinematics
- forward kinematics
- inverse kinematics

**rotation & homogeneous transformation matrix**

$$
^AT_b = \left[\begin{array}c ^AR_B & p \\ 0&1 \end{array}\right] 
$$

## D-H representation
先设定一堆link之间的坐标轴

对于joint $i-1$ 到 joint $i$之间的link， 设定两个坐标系

$z_{i-1}$, $z_i$ 轴是各自运动轴， 无论怎么运动，这个轴保持不变

$x_{i-1}$同时垂直 $z_{i-1}$和$z_i$

$y$是另外一个维度的轴

设定四个参数:
- $\alpha_{i-1}$ 是$z_{i-1}$与$z_i$之间的夹角
- $a_{i-1}$ is the distance between $z_{i-1}$ and $z_i$ (along $x_{i-1}$)
- $d_i$ is the distance between $x_{i-1}$ and $x_i$ (along $z_i$)
- $\theta_i$ is the angle between $x_i$ and $x_{i-1}$

注意还要有一个$0$坐标系，一般是地面坐标系

### 坐标系转换的性质
**一个joint，前面的*四个参数*里面只有一个是变量**
- 如果是prismatic的话这个变量就是$d_i$
- 如果是 revolve的话就是$\theta_i$

## transformation matrix
$^{i-1}T_i$：坐标系转换的矩阵

这个矩阵$T_i$输入的是$(x,y,z,1)^T$, 输出的是另外一个坐标系下的~

$$
^{i-1}T_i = \left[\begin{array}c
1 & 0 & 0 & 0 \\
0 & \cos\alpha_{i-1} & -\sin\alpha_{i-1} & 0\\
0 & \sin\alpha_{i-1} & \cos\alpha_{i-1} & 0\\
0 & 0 & 0 & 1
  \end{array}\right] 
\left[\begin{array}c 
1 & 0 & 0 & a_{i-1} \\
0 & 1 & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
 \end{array}\right] 
 \left[\begin{array}c 
\cos\theta_i & -\sin\theta_i & 0 & 0\\
\sin\theta_i & \cos\theta_i & 0 & 0\\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
  \end{array}\right] 
  \left[\begin{array}c 
1 & 0 & 0 & 0\\
0 & 1 & 0 & 0 \\
0 & 0 & 1 & d_i \\
0 & 0 & 0 & 1
 \end{array}\right] 
$$

$$
^{i-1}T_i = \left[\begin{array}c 
\cos\theta_i & -\sin\theta_i & 0 & a_{i-1}\\
\sin\theta_i\cos\alpha_{i-1} &
\cos\theta_i\cos\alpha_{i-1} &
-\sin\alpha_{i-1} & -\sin\alpha_{i-1}d_i\\
\sin\theta_i\sin\alpha_{i-1} &
\cos\theta_i\sin\alpha_{i-1} &
-\cos\alpha_{i-1} & -\cos\alpha_{i-1}d_i\\
 \end{array}\right] 
$$

## inverse kinematics
given desired position & orientation

get $q = (\theta_1,\theta_2 ..., \theta_n)$

**思路**: 有了desired Y之后，可以得到一个目标的从地面到最后的转移矩阵

$$
^0T_n = \left[\begin{array}c 
R_{11}&R_{12}&R_{13}&P_{1}\\
R_{21}&R_{22}&R_{23}&P_{2}\\
R_{31}&R_{32}&R_{33}&P_{3}\\
0&0&0&1
 \end{array}\right] 
$$

里面十二个数相当于是12个等式

**这是一个highly NON-LINEAR 的系统，如何解呢**

一个解决办法是左乘$^{0}T_{1}^{-1}$
得到
$$
^{0}T_{1}^{-1} . ^0T_N = ^1T_2.^2T_3 ... ^{n-1}T_{n}
$$

这样如果12个等式里面右边有常数项的话，就可以直接解出来了
>这是工程师正式求解之前都会看一下这个试试运气

inverse kinematic -> differential kinematic


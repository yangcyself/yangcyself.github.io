**The Concepts in control theory**

**Fixed points.** Stable fixed points represent the static postures in which the robot can safely stand still.

**Limit cycles.** Limit cycles provide a natural extension of fixed-point analysis to periodic walking or running motions

**Viability.** Viability is a concept of controlled invariance, which analyzes the set of states from which the robot is able to avoid to fall. Unfortunately, this property can be intractable to compute

**Controllability.** Controllability provides a slightly restricted notion of viability, analyzing the set of states from which the robot is capable of returning to a particular fixed point (or limit cycle). This can be more tractable to compute than viability, especially for simple models.

**Robust stability**. Robust stability (or viability) examines the properties of the system considering worst-case (bounded) disturbances. For instance, a robust controller may be able to guarantee that a fixed point is stable even if the estimate of the mass of the trunk is wrong by ±10%.

**Stochastic stability**. Stochastic analysis provides tools to investigate the probability of falling down. For many robot disturbance models, the system will always fall eventually (with probability one), but analysis can reveal long-living “metastable” distributions.

**Input-output stability**. This analysis treats a particular disturbance as an input, a performance criteria as output, and attempts to compute a relative gain or sensitivity of the robot performance due to this input.

**Stability margins**. Robustness analysis can be difficult. In practice control designers often settle for the system staying comfortably away from the boundaries of deterministic stability


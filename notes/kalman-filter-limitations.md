# Kalman Filter Limitations in Real-World Systems

## Overview

The Kalman Filter is widely used for state estimation in robotics due to its optimality under linear Gaussian assumptions. However, real-world systems rarely satisfy these assumptions perfectly. Understanding its limitations is essential for designing reliable autonomous systems.

---

## Assumptions and Practical Violations

The standard Kalman Filter relies on several key assumptions:

- Linear system dynamics  
- Gaussian noise distributions  
- Accurate system and noise models  

In practice, these assumptions are often violated:

- **Non-linear dynamics:** Real robotic systems frequently exhibit non-linear behavior, especially in motion and sensing.  
- **Non-Gaussian noise:** Sensor noise may include outliers, bias, or heavy-tailed distributions.  
- **Model mismatch:** Inaccurate system models can lead to divergence over time.  

---

## Failure Modes Observed in Practice

Through experimental implementations with noisy sensor data, several failure patterns emerge:

- **Filter divergence:** When the model is incorrect or noise is underestimated, the estimate drifts away from reality.  
- **Overconfidence:** Poor covariance tuning leads to estimates that appear certain but are incorrect.  
- **Latency sensitivity:** Delayed measurements can destabilize estimation when not handled properly.  
- **Sensor inconsistency:** Conflicting sensor inputs can degrade estimation quality if not properly weighted.  

---

## Engineering Implications

These limitations highlight an important principle:

> State estimation is not only a mathematical problem, but a systems engineering challenge.

Robust estimation requires:

- Careful modelling of system and noise characteristics  
- Continuous validation of assumptions  
- Integration with system-level constraints such as timing, communication, and computation  

---

## Extensions and Alternatives

To address these limitations, several approaches are commonly used:

- **Extended Kalman Filter (EKF):** Handles mild non-linearities through linearization  
- **Unscented Kalman Filter (UKF):** Improves estimation under non-linear transformations  
- **Particle Filters:** Suitable for highly non-linear, non-Gaussian systems  

---

## Conclusion

In real-world robotics, the Kalman Filter is not a universal solution but a component within a broader estimation architecture. Reliable autonomy depends on understanding when the filter works, when it fails, and how it interacts with physical and computational constraints.

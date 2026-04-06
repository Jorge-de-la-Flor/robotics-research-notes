# Estimation Failure Under Model Mismatch: A Practical Observation

## Overview

State estimation techniques such as the Kalman Filter assume accurate system models and well-characterized noise. In real-world embedded systems, these assumptions are rarely satisfied.

This note documents a practical observation: how small mismatches between the assumed model and the real system can lead to degraded estimation quality and unstable system behavior.

---

## Experimental Context

The observation is based on a distributed sensing system composed of:

- An Arduino-based sensing node  
- Ultrasonic distance measurements (HC-SR04)  
- A 1D Kalman filter implemented on-device  
- Transmission over UART → MQTT → edge node  

The system operates under real-world conditions, including sensor noise, timing variability, and communication delays.

---

## Model Assumptions

The Kalman filter was implemented under standard assumptions:

- Linear state transition  
- Gaussian measurement noise  
- Fixed process noise (Q) and measurement noise (R)  

These assumptions simplify the estimation problem but introduce risk when they do not match reality.

---

## Observed Mismatch

In practice, several deviations were observed:

- Ultrasonic sensor noise exhibited non-Gaussian behavior (spikes and outliers)  
- Measurement latency varied depending on system load  
- Environmental factors affected signal consistency  

These effects violate core Kalman assumptions.

---

## Failure Behavior

Under these conditions, the following behaviors emerged:

- **Over-smoothing:** The filter lagged behind rapid changes in distance  
- **Delayed response:** State updates were not aligned with real-time dynamics  
- **Transient divergence:** Sudden measurement spikes caused temporary estimation drift  

These effects were not constant but appeared under specific operating conditions.

---

## System-Level Impact

The estimation errors propagated into system behavior:

- Incorrect proximity classification in the finite-state machine  
- Delayed transitions between system states  
- Inconsistent actuation (servo and alert responses)  

This demonstrates that estimation errors directly influence control logic and system outcomes.

---

## Engineering Insight

> Estimation quality cannot be evaluated in isolation from system behavior.

A filter that appears stable in isolation may produce undesirable outcomes when integrated into a real system with timing constraints and decision logic.

---

## Practical Adjustments

To mitigate these effects, several adjustments were considered:

- Increasing measurement noise (R) to reduce overconfidence  
- Introducing threshold-based validation for outlier rejection  
- Designing FSM transitions to tolerate estimation lag  

These adjustments improved system robustness without requiring a complete change in estimation method.

---

## Conclusion

This observation highlights a key principle in robotics:

Estimation is not a standalone solution, but a component whose behavior must be evaluated within the full system.

Reliable systems emerge not from perfect models, but from architectures that remain stable when models are imperfect.

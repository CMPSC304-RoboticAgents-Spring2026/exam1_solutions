# CMPSC 304 – Robotic Agents
## Exam 1 Solutions
**Date:** February 13, 2026  
**Duration:** 50 minutes

---

## SECTION 1: MULTIPLE CHOICE
*(5 questions × 1 point = 5 points)*

### 1. Which of the following statements about stability is CORRECT?

- A. A car and a motorcycle are both statically stable when stationary.
- B. A car is statically stable when stationary, while a motorcycle requires dynamic stability when moving.
- C. A motorcycle is statically stable at rest, but a car requires dynamic stabilization when turning.
- D. Both a car and a motorcycle are dynamically stable systems at all times.

**ANSWER: B**

*Explanation:* A car has 4 wheels and is statically stable; a motorcycle needs to be moving to stay upright through dynamic stability.

---

### 2. Which type of sensor provides information about a robot's internal state?

- A. Proprioceptive sensors
- B. Exteroceptive sensors
- C. Environmental sensors only
- D. Distance sensors only

**ANSWER: A**

*Explanation:* Proprioceptive sensors like encoders and IMUs measure internal state; exteroceptive sensors measure the environment.

---

### 3. In Arduino, what value should X be in analogWrite(pin, X) to achieve a 25% duty cycle?

- A. 25
- B. 64
- C. 128
- D. 255

**ANSWER: B**

*Explanation:* 64 = 25% of 255; analogWrite uses 0-255 range, so 255 × 0.25 = 63.75 ≈ 64.

---

### 4. A sensor has measurements that cluster tightly together but are far from the true value. This sensor has:

- A. High accuracy, high precision
- B. Low accuracy, low precision
- C. High accuracy, low precision
- D. Low accuracy, high precision

**ANSWER: D**

*Explanation:* Precision = repeatability/clustering; accuracy = closeness to true value. Tight cluster = high precision, far from true = low accuracy.

---

### 5. A drone can adjust pitch, yaw, and roll independently. How many mechanical degrees of freedom does it have for rotation?

- A. 1
- B. 2
- C. 3
- D. 6

**ANSWER: C**

*Explanation:* 3 rotational DoF: pitch, yaw, and roll are independent rotations about different axes.

---

## SECTION 2: SHORT ANSWER
*(3 questions × 1 point = 3 points)*

### 6. Your robot uses 4 AA batteries in series to power DC motors.

**a) What is the total voltage supplied to the motors? Show your calculation.**

**ANSWER:** 4 AA batteries in series = 4 × 1.5V = **6V total** (voltages add in series)

**b) Why can't you power the motors directly from Arduino's 5V pin? Explain the role of a motor driver.**

**ANSWER:** Motors draw 150-300 mA (up to 2A when stalled), but Arduino pins can only supply 20-40 mA. Direct connection would damage the Arduino. Motor driver acts as a power bridge: Arduino provides low-current control signals (<20 mA) to the driver, which switches high-current power from the battery to the motors.

---

### 7. Compare two distance sensors: Sensor A uses sound waves at 40 kHz, while Sensor B uses infrared light. Which performs better outdoors in sunlight? Which has a longer maximum range? Explain your reasoning.

**ANSWER:** Sensor A (ultrasonic) performs better outdoors because sunlight contains IR light that interferes with Sensor B (IR sensor). Sensor A also has longer maximum range (several meters vs ~1m for IR) because sound waves travel farther before dissipating. IR sensors are affected by ambient light and surface properties.

---

### 8. A differential-drive robot has two powered rear wheels and one front caster wheel.

**a) What are its Cartesian degrees of freedom (DoF) on the plane?**

**ANSWER:** **3 Cartesian DoF:** x, y, and θ

**b) What happens to the Cartesian DoF if you add a second caster wheel? Explain.**

**ANSWER:** The Cartesian DoF remains 3. Adding a second caster wheel doesn't change the controllable DoF because caster wheels are passive and follow the motion determined by the two powered wheels. The robot still moves in the same ways (forward/backward and rotation).

---

## SECTION 3: SCENARIO-BASED PROBLEMS
*(2 questions × 1 point = 2 points)*

### 9. You're programming a differential-drive robot using wheel encoders. You command both wheels to rotate forward at the same speed, but the robot curves to the right instead of moving straight.

**a) Using your knowledge of kinematics, explain what is happening. What does this tell you about the two wheels?**

**ANSWER:** The robot curves right because the left wheel travels less distance than the right wheel. In differential-drive kinematics, unequal wheel distances cause rotation. This indicates the left wheel is slipping, has a smaller effective diameter, or the motors have different speeds despite the same command.

*Note: The fact that the robot curves (rather than spins in place) tells us both wheels are moving forward but at different rates. If motors were reversed or pins incorrectly connected, we'd see spinning rather than curving. An off-center center of mass could contribute to unequal wheel performance through weight distribution, but the direct observation is that the wheels have unequal speeds/distances.*

**b) Describe one way you could fix this problem to make the robot move straight:**

**Sample Solution 1:** Calibrate the motors - measure actual wheel speeds with encoders and adjust PWM values to compensate for differences (e.g., if left wheel is slower, increase its PWM).

**Sample Solution 2:** Use encoder feedback in a control loop - continuously read encoder values and adjust motor speeds in real-time to keep wheel velocities equal.

**Sample Solution 3:** Check for mechanical issues - ensure wheels have equal diameters, check for debris or friction differences, and verify both motors are functioning properly.

---

### 10. You need to design a robot that can climb a 15-degree slope while carrying a 10 kg payload. The robot will move slowly and must not tip over.

**a) Explain how the position of the center of mass affects the robot's stability on the slope. Where should you place the payload?**

**ANSWER:** The center of mass must remain within the support polygon (area between the wheels/contact points). On a slope, gravity pulls the center of mass backward, potentially causing backward tipping. Place the payload LOW and FORWARD to keep the center of mass as low and forward as possible, increasing stability.

**b) How does static stability apply to this scenario? What determines whether the robot will tip backward while climbing?**

**ANSWER:** Static stability requires the vertical projection of the center of mass to fall within the support polygon. The robot will tip backward if the center of mass shifts too far back such that its projection moves behind the rear wheels. A lower center of mass and longer wheelbase help prevent tipping.

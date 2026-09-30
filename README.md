**Distance-Based Speed Controller with Automatic Braking:**
This Arduino Uno project implements an automated collision avoidance system. It measures the distance to an obstacle using an HC-SR04 ultrasonic sensor, displays the warning level via a 4-LED bar graph, and dynamically controls a DC motor's speed using an L293D motor driver.

**How It Works:**

The system continuously runs a loop through three main stages:

**1. Distance Calculation**
• The Arduino triggers the HC-SR04 sensor to emit ultrasonic sound waves.
• The waves bounce off an obstacle and return to the sensor.
• The Arduino measures the travel time (pulseIn) and uses the speed of sound to calculate the precise distance in centimeters.

**2. Speed Control & PWM Actuation**
• The L293D driver handles direction by keeping one input pin HIGH and the other LOW (forward motion).
• The Arduino adjusts the motor's actual speed using Pulse Width Modulation (PWM) via the L293D's enable pin. Varying the duty cycle (0 to 255) changes the voltage sent to the motor, safely lowering or increasing its speed.

**3. Logic & Response Matrix**
The microcontroller constantly updates the system state based on the calculated distance:
• Green: Safe (> 50 cm): Green LED turns ON. Motor runs at Full Speed (PWM: 255).
• Yellow: Approach (31 - 50 cm): Yellow LED turns ON. Motor slows to Medium-High Speed (PWM: 180).
• Orange: Warning (15 - 30 cm): Orange LED turns ON. Motor drops to Slow Speed (PWM: 100).
• Red: Hazard (< 15 cm): Red LED turns ON. Motor receives a command of 0 for an Immediate Stop.

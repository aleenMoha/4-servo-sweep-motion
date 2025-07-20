# 🦾 4-Servo Sweep Motion (Arduino Tinkercad Project)

This project simulates **4 servo motors** using an Arduino Uno board in **Tinkercad Circuits**. The motors:
- Perform a sweeping motion for **2 seconds** (based on the Arduino Sweep example).
- Then **all servos hold at 90°** indefinitely.

## 🔗 Live Simulation
Run the project in your browser:  
👉 [Tinkercad Link](https://www.tinkercad.com/things/1G5uHiXdlmG-4-servo-sweep-motion?sharecode=atNll8OwS89YeunBeoKZ5KRF0xbZoa25Jt3r0iUoAgE)

## 🧠 Project Objectives

- Understand how to control multiple servo motors using the `Servo` library.
- Simulate basic robotic motion in a virtual environment.
- Practice controlling timing and motion flow using Arduino code.

## ⚙️ Hardware Components

- 1 × Arduino Uno R3
- 4 × Standard Servo Motors (micro servo)
- Jumper wires

## 🔌 Wiring Overview

Each servo has three connections:
- **Red** → `5V`
- **Black/Brown** → `GND`
- **Yellow/Orange (Signal)** → Connected to:
  - `Servo1`: Pin 3
  - `Servo2`: Pin 5
  - `Servo3`: Pin 6
  - `Servo4`: Pin 9

## 🧾 Arduino Code

```cpp
#include <Servo.h>

Servo servo1;
Servo servo2;
Servo servo3;
Servo servo4;

void setup() {
  servo1.attach(3);
  servo2.attach(5);
  servo3.attach(6);
  servo4.attach(9);
}

void loop() {
  // Sweep for 2 seconds
  unsigned long startTime = millis();
  while (millis() - startTime < 2000) {
    for (int pos = 0; pos <= 180; pos += 1) {
      servo1.write(pos);
      servo2.write(pos);
      servo3.write(pos);
      servo4.write(pos);
      delay(5);
    }
    for (int pos = 180; pos >= 0; pos -= 1) {
      servo1.write(pos);
      servo2.write(pos);
      servo3.write(pos);
      servo4.write(pos);
      delay(5);
    }
  }

  // Hold at 90°
  servo1.write(90);
  servo2.write(90);
  servo3.write(90);
  servo4.write(90);
  while (true); // stop loop
}
```
## 🤖 Humanoid Robot Walking Motion Algorithm

This section describes the step-by-step process used to make the humanoid robot walk using servo motors.

### Initialization
- Set all leg and body servos to neutral (standing) position.
- Ensure the robot is stable and balanced.

### Walking Cycle (Repeat for each step)

1. **Shift Weight to Supporting Leg**  
   - Adjust torso and hip servos to transfer weight onto the supporting leg.
   - Stabilize the supporting leg firmly on the ground.

2. **Lift Swinging Leg**  
   - Bend the knee servo of the swinging leg to lift the foot by the desired step height.
   - Move the hip servo forward by the step length.
   - Adjust the ankle servo to keep the foot parallel to the ground.

3. **Move Swinging Leg Forward and Place Down**  
   - Extend the knee servo to straighten the leg forward.
   - Gradually lower the foot until it touches the ground.

4. **Shift Weight to Newly Placed Leg**  
   - Transfer weight onto the leg that just landed by adjusting torso and hip servos.

5. **Repeat for Opposite Leg**  
   - Perform the same lift, move, and place sequence for the opposite leg.

6. **Optional Arm Movement**  
   - Swing arms opposite to the legs to help with balance and natural motion.

7. **Continuous Walking**  
   - Repeat steps 1 to 6 continuously for sustained walking.

### Stopping
- Return all servos to the neutral standing position.
- Ensure the robot is balanced and stable.

### Notes
- Smooth and gradual servo movements are essential for realistic walking.
- Sensor feedback (e.g., gyroscope) can be integrated for dynamic posture adjustments.
- Step length, height, and speed can be tuned according to terrain and desired walking pace.


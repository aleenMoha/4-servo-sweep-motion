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
🤖 Humanoid Robot Walking Motion Algorithm
This section explains the step-by-step logic used to execute walking motions in the humanoid robot using servo motors.

Algorithm Overview
The humanoid robot performs walking by coordinating leg servos to simulate natural steps. Each walking cycle consists of shifting weight, lifting and moving the swinging leg, placing it down, and repeating with the opposite leg, while maintaining balance.

Step-by-Step Algorithm
Initialization

Set all leg and body servos to the neutral standing position.

Ensure the robot is stable and balanced before starting.

Walking Cycle (Repeat for each step):

Shift Weight to Supporting Leg
Slightly tilt the torso or shift hip servos to transfer the robot’s weight onto the supporting leg, ensuring stability.

Lift Swinging Leg
Bend the knee servo of the leg to be lifted to raise the foot by the desired step height.
Adjust the hip servo to move the leg forward by the step length.
Position the ankle servo to keep the foot parallel to the ground.

Move Leg Forward and Place Down
Straighten the knee servo as the leg extends forward.
Lower the foot gradually until it touches the ground.

Shift Weight to Newly Placed Leg
Transfer the weight onto the leg that just landed by adjusting torso and hip servos.

Repeat with Opposite Leg
Perform the lifting and moving sequence on the other leg to complete a full walking step.

Arm Movement for Balance (Optional)
Swing the arms in opposition to the legs to help maintain balance and provide natural movement.

Continuous Walking
Repeat the walking cycle steps until the robot needs to stop.

Stopping
Return all servos to the neutral standing position and ensure the robot is stable.

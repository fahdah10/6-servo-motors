# Arduino + 6 Servo Motors Control

## 🧠 Project Idea

This project demonstrates how to control **6 servo motors** using an **Arduino Uno** board. The code runs a synchronized "sweep" movement across all servos for 2 seconds, then locks all servos at the center position (90°). This setup is ideal for simulating the basic motion of a **humanoid robot** or mechanical system.

---

## 📘 Explanation

This project is perfect for beginners who want to learn how to:
- Use the `Servo.h` library to control multiple motors.
- Synchronize servo movements for robotic motion.
- Apply timing logic using `millis()` instead of delay functions.
- Simulate basic robotic movement such as walking or joint calibration.

To build this project, you will need:
- An **Arduino Uno** board to run the code.
- **6 servo motors** (e.g., SG90) to simulate legs or joints.
- A **breadboard** and **jumper wires** to make connections.
- A **USB cable** to upload the sketch to the Arduino.
- Optionally, an **external 5V power supply** if the servos need more current than the Arduino can provide.

> This project gives a solid base for learning how to develop humanoid or robotic leg motion, and can be expanded to include balance sensors and movement algorithms.

---

## 🔌 Wiring Instructions

Each servo has three wires:
- **Signal (Orange/Yellow)** → Connect to Arduino digital pins (3, 5, 6, 9, 10, 11)
- **VCC (Red)** → Connect to 5V (Arduino or external power)
- **GND (Brown/Black)** → Connect to Arduino GND

---

## 📜 Arduino Code

```cpp
#include <Servo.h>

Servo servo1, servo2, servo3, servo4, servo5, servo6;
unsigned long startTime;
int angle = 0;
int step = 1;

void setup() {
  servo1.attach(3);
  servo2.attach(5);
  servo3.attach(6);
  servo4.attach(9);
  servo5.attach(10);
  servo6.attach(11);
  
  startTime = millis();
}

void loop() {
  unsigned long currentTime = millis();

  if (currentTime - startTime <= 2000) {
    // Sweep motion
    servo1.write(angle);
    servo2.write(angle);
    servo3.write(angle);
    servo4.write(angle);
    servo5.write(angle);
    servo6.write(angle);

    angle += step;
    if (angle >= 180 || angle <= 0) {
      step = -step;
    }
    delay(15);
  } else {
    // Hold at 90 degrees
    servo1.write(90);
    servo2.write(90);
    servo3.write(90);
    servo4.write(90);
    servo5.write(90);
    servo6.write(90);

    while (true); // Stop the loop
  }
}

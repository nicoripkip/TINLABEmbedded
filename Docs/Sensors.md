# Sensor document

This guide provides a detailed overview of the sensors, actuators, and control modules used in the automated telescope system. It is intended to help anyone looking to replicate or expand upon the project.

---

## Stepper Motor

### Description
```
Bipolar stepper motors are essential for accurate rotational control of the telescope. With precise step increments, they allow the telescope to follow celestial objects smoothly.
```

### Key Features
```
- High torque
- 1.8° step angle (200 steps per revolution)
- Works with microstepping drivers like A4988
```

---

## Raspberry Pi 4B (2GB)

### Description
```
The Raspberry Pi serves as the main control unit, running the software that processes sensor input and controls motor output.
```

### Key Features
```
- Quad-core ARM Cortex-A72 CPU
- GPIO for hardware interfacing
- Supports Linux-based OS for flexibility
```

---

## A4988 Stepper Motor Driver

### Description
```
This driver module allows microstepping, enabling smoother motion and better accuracy when controlling the stepper motors.
```

### Key Features
```
- Up to 1/16 microstepping
- Adjustable current control
- Compatible with 8V–35V power supply
```

---

## BMI160 6DOF Gyroscope & Accelerometer

### Description
```
A compact IMU sensor used to measure angular motion and orientation. It provides feedback to ensure the telescope is pointing in the correct direction.
```

### Key Features
```
- 3-axis gyroscope and 3-axis accelerometer
- I2C or SPI interface
- Low power consumption
```

---

## Bresser Full HD Deep-Sky Camera

### Description
```
A specialized astronomy camera used for capturing high-resolution images of celestial bodies and guiding the telescope.
```

### Key Features
```
- Full HD resolution
- High sensitivity sensor
- USB interface for image streaming
```

---

## Adafruit Ultimate GPS Module

### Description
```
Provides accurate geographical coordinates to align the telescope for celestial tracking based on the user's location.
```

### Key Features
```
- 1.8m positional accuracy
- Fast fix times
- Built-in antenna and battery backup
```

---

## ASAIR AHT25 Temperature & Humidity Sensor

### Description
```
Monitors environmental conditions that may affect the telescope’s electronics or image quality.
```

### Key Features
```
- Digital I2C interface
- High precision readings
- Compact and reliable
```

---

## TCA9548A I2C Multiplexer

### Description
```
An 8-channel I2C switch that allows multiple sensors with the same address to coexist on a single bus.
```

### Key Features
```
- Selectable I2C channels
- Ideal for connecting multiple BMI160s
- Easy GPIO control
```

---

## HC-SR04 Ultrasonic Sensor

### Description
```
Used to detect obstacles around the telescope, preventing collisions during movement.
```

### Key Features
```
- Measures distances from 2 cm to 4 m
- Digital trigger and echo pins
- Accurate within a few millimeters
```

---

## Planetary Gearbox

### Description
```
Reduces the RPM of the stepper motors while increasing torque, allowing for precise and powerful movements.
```

### Key Features
```
- Compatible with NEMA 17 motors
- Multiple gear ratios available
- Ensures fine control of telescope positioning
```

---

## Tactile Buttons (12x12mm)

### Description
```
Simple mechanical push-buttons used for basic control functions such as resets, manual override, or menu navigation.
```

### Key Features
```
- Durable and responsive
- Suitable for quick inputs
- Comes in various colors for distinction
```

---

## 4x4 Matrix Membrane Keypad

### Description
```
Flexible keypad used to input commands or coordinates directly into the control system.
```

### Key Features
```
- 16 keys (0–9, A–D, *, #)
- Easy to interface using GPIO or I2C adapters
- Flat, adhesive-backed for easy mounting
```

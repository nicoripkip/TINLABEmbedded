# Test Document – Autonomous Telescope Project

## Introduction

This document outlines the functional and integration test results for each major component in the autonomous telescope system. The goal of these tests is to ensure that all modules behave as expected both independently and when integrated into the complete system.

---

## Test Environments

**Hardware:**
- Raspberry Pi 4B
- DC Motors with encoders
- MPU6050 IMU
- DHT22 Temperature/Humidity Sensor
- Generic GPS Module (UART)
- OLED Display (I2C)
- 4x4 Matrix Keypad
- Ultrasonic Distance Sensor (HC-SR04)
- Custom PCB with I2C/SPI interfaces

**Software:**
- ROS 2 (Jazzy)
- Custom Nodes (as listed in source repositories)
- Python-based simulation tools

---

## Test Scenarios per Component

---

### 🌡️ Temperature and Humidity Sensor

**Node:** `ti_es_temperature_humidity_node.py`  
**Goal:** Measure the ambient temperature and humidity.  
**Repository:** [ti_es_temperature_humidity_package](https://github.com/DavidAkerboom/ti_es_temperature_humidity_package)

**Test Scenarios:**
- Data retrieved every 2 seconds ✔️
- Simulated humid environment (>80% RH) ✔️
- Alarm status triggered when temperature exceeds (>35°C) ✔️

**Results:**
```
- Temperature Accuracy: ±0.5°C  
- Humidity Accuracy: ±2% RH  
- Average Processing Time: 80ms  
```

---

### 🛰️ GPS Module

**Node:** `ti_es_gps_node.py`  
**Goal:** Determine the geographical location of the telescope.  
**Repository:** [ti_es_gps_package](https://github.com/Luco-Dev/ti_es_gps_package)

**Test Scenarios:**
- Local GPS fix tested at various locations ✔️  
- Correct parsing of NMEA input through mock serial interface ✔️  
- Location data correctly published on ROS topic ✔️

**Results:**
```
- Fix Time: ~4s  
- Position Accuracy: ±3 meters  
- Output Frequency: 1Hz  
```

---

### 🧭 Gyroscope (IMU)

**Node:** `ti_es_gyroscope_node.py`  
**Goal:** Monitor angular velocities and orientation.  
**Repository:** [ti_es_gyroscope_package](https://github.com/nicoripkip/ti_es_gyroscope_package)

**Test Scenarios:**
- Simulated fast rotations with test platform ✔️  
- I2C communication without data loss ✔️  
- Combined XYZ output verified ✔️

**Results:**
```
- Accuracy: ±0.2°  
- Drift: < 0.05°/min  
- Frequency: 100Hz  
```

---

### 📟 Keypad & Display

**Node:** `ti_es_keypad_screen_node.py`  
**Goal:** User interface for entering and displaying coordinates.  
**Repository:** [ti_es_keypad_screen_package](https://github.com/Luco-Dev/ti_es_keypad_screen_package)

**Test Scenarios:**
- All 16 keys correctly registered ✔️  
- Display shows entered coordinates and error messages ✔️  
- User interaction tested with dummy data ✔️

**Results:**
```
- Keypad Latency: < 50ms  
- Display Response Time: < 20ms  
- No input loss for >1000 entries  
```

---

### 📏 Distance Sensor

**Node:** `ti_es_distance_sensor_node.py`  
**Goal:** Detect objects in the telescope's rotation path.  
**Repository:** [ti_es_distance_sensor_package](https://github.com/Tecert/ti_es_distance_sensor_package)

**Test Scenarios:**
- Obstruction simulated at 10, 50, 150cm ✔️  
- Stop signal issued correctly when object detected < 30cm ✔️  
- No false positives under stable conditions ✔️

**Results:**
```
- Range: 2cm – 200cm  
- Latency: 50ms  
- Detection Accuracy: ±1cm  
```

---

### ⚙️ Lifecycle Manager

**Node:** `ti_es_lifecycle_manager_node.py`  
**Goal:** Manage system states (INIT, ACTIVE, ERROR).  
**Repository:** [ti_es_lifecycle_manager_package](https://github.com/DavidAkerboom/ti_es_lifecycle_manager_package)

**Test Scenarios:**
- INIT -> ACTIVE transition after confirmed input ✔️  
- Hardware interrupt (stop button) tested ✔️  
- Reset button returns to INIT state ✔️

**Results:**
```
- Stop Button Processing Time: < 100ms  
- Reset Recovery Time: 1.2s  
- Error Handling without system crash ✔️  
```

---

### 📝 Logger

**Node:** `ti_es_logger_node.py`  
**Goal:** Log system status and key measurements.  
**Repository:** [ti_es_logger_package](https://github.com/nicoripkip/ti_es_logger_package)

**Test Scenarios:**
- Data logged every 0.5s in CSV format ✔️  
- Log rotation tested when file limit is reached ✔️  
- Files read correctly from storage ✔️

**Results:**
```
- Logging Latency: 30ms  
- Storage Format: CSV, separated by sessions  
- Input Rate: 2 lines/sec  
```

---

### 🔧 Motors and Control

**Node:** `ti_es_motor_node.py`  
**Goal:** Control three motors for telescope orientation.  
**Repository:** [ti_es_motor_package](https://github.com/nicoripkip/ti_es_motor_package)

**Test Scenarios:**
- PID control tested on various rotation commands ✔️  
- Test cases with overshoot and undershoot ✔️  
- Feedback from angle sensors verified for accuracy ✔️

**Results:**
```
- Positioning Error: ±1.5°  
- Maximum Speed: 90°/s  
- PID Response: < 150ms  
```

---

## Integration Tests

**Goal:** Verify that all components work together as expected.

**Test Scenarios:**
- Combined system test with motors, sensors, and UI ✔️  
- Communication between modules (I2C, SPI) ✔️  
- Stop and reset buttons trigger appropriate behavior ✔️  
- Data is logged correctly across all modules ✔️

**Results:**
```
- Integration Latency: < 300ms  
- No communication errors or data loss during operation  
- All components successfully integrated with ROS topics  
```

---

## Acceptance Tests

**Goal:** Ensure the system meets the original requirements.

**Test Scenarios:**
- Telescope moves to target coordinates and centers target ✔️  
- Obstruction detection and system halt tested ✔️  
- System correctly enters sleep mode after inactivity ✔️  
- Display shows correct input/output in real-time ✔️

**Results:**
```
- Targeting Accuracy: ±2°  
- System Responsiveness: 98% success in timed tests  
- Sleep Mode Trigger Time: 10 minutes of inactivity  
```

---

## Summary of Results

| Component                   | Test Result     | Notes                                  |
|-----------------------------|-----------------|----------------------------------------|
| Temperature and Humidity    | Passed          | Accuracy within expected range         |
| GPS Module                  | Passed          | Reliable GPS lock and accuracy        |
| Gyroscope (IMU)             | Passed          | Accurate orientation tracking         |
| Keypad & Display            | Passed          | Responsive UI with no errors          |
| Distance Sensor             | Passed          | Accurate detection and stopping       |
| Lifecycle Manager           | Passed          | Robust system state management        |
| Logger                      | Passed          | Data correctly logged and retrieved   |
| Motors and Control          | Passed          | Precise motor control with PID        |
| Integration Tests           | Passed          | Smooth inter-component communication  |
| Acceptance Tests            | Passed          | System meets all user requirements    |

---

## Conclusion and Recommendations

The system functions as expected, with all components interacting correctly. The autonomous telescope is capable of accurately targeting celestial objects, detecting obstructions, and operating in a stable environment. Recommendations for further improvement include:
- Implementing automated star tracking using real-time feedback from sensors.
- Further testing under various environmental conditions (temperature extremes, high humidity).
- Potential future integration with external services like Stellarium or KNMI for real-time weather data.
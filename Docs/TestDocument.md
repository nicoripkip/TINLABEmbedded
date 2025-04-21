# Autonomous Telescope - Test Document

## Project Overview

This document outlines the testing procedures for the autonomous telescope project, ensuring compliance with the specified embedded system requirements. Each section includes a checkbox to confirm the implementation and successful testing of the respective feature.

---

## ✅ 1. Watchdog Timer

**Objective:** Ensure the system resets automatically in case of a software hang or crash.

**Implementation:**
- Utilize the Raspberry Pi's hardware watchdog timer.
- Configure the watchdog to monitor the main application process.

**Test Procedure:**
- Intentionally halt the main application.
- Observe if the system resets within the expected timeout period.

**Confirmation:** [ ] Implemented and tested successfully.

---

## ✅ 2. Sleep Mode

**Objective:** Reduce power consumption during periods of inactivity.

**Implementation:**
- Employ sleep modes available in the Raspberry Pi or connected microcontrollers.
- Transition to sleep mode after a defined period of inactivity.

**Test Procedure:**
- Allow the system to remain idle.
- Verify transition to sleep mode.
- Trigger an event (e.g., button press) to wake the system.

**Confirmation:** [ ] Implemented and tested successfully.

---

## ✅ 3. Hardware Interrupts

**Objective:** Respond to external events promptly without continuous polling.

**Implementation:**
- Configure GPIO pins to detect events from sensors (e.g., motion detection).
- Use interrupt service routines to handle events.

**Test Procedure:**
- Simulate external events (e.g., movement).
- Confirm that interrupts are triggered and handled appropriately.

**Confirmation:** [ ] Implemented and tested successfully.

---

## ✅ 4. Software Interrupts

**Objective:** Manage internal events efficiently within the software architecture.

**Implementation:**
- Utilize software interrupt mechanisms or event-driven programming paradigms.
- Handle events such as data reception or internal state changes.

**Test Procedure:**
- Trigger software events.
- Verify that the system responds correctly.

**Confirmation:** [ ] Implemented and tested successfully.

---

## ✅ 5. Use of RTOS / Embedded Linux

**Objective:** Leverage an operating system to manage tasks and resources effectively.

**Implementation:**
- Deploy the system on Raspberry Pi OS (a Linux-based OS).
- Utilize multitasking capabilities for concurrent processes.

**Test Procedure:**
- Monitor system performance under multitasking conditions.
- Ensure stability and responsiveness.

**Confirmation:** [ ] Implemented and tested successfully.

---

## ✅ 6. Communication via I2C and/or SPI

**Objective:** Facilitate communication between the Raspberry Pi and peripheral devices.

**Implementation:**
- Use I2C for sensors like the BMI160 gyroscope and AHT25 temperature/humidity sensor.
- Use SPI if applicable for other peripherals.

**Test Procedure:**
- Establish communication with each device.
- Verify data integrity and responsiveness.

**Confirmation:** [ ] Implemented and tested successfully.

---

## ✅ 7. Sensor Data Acquisition

**Objective:** Collect and process data from various sensors.

**Implementation:**
- Integrate sensors such as:
  - BMI160 gyroscope ([ti_es_gyroscope_package](https://github.com/nicoripkip/ti_es_gyroscope_package))
  - AHT25 temperature/humidity sensor ([ti_es_temperature_humidity_package](https://github.com/DavidAkerboom/ti_es_temperature_humidity_package))
  - GPS module ([ti_es_gps_package](https://github.com/Luco-Dev/ti_es_gps_package))
  - Ultrasonic distance sensors ([ti_es_distance_sensor_package](https://github.com/Tecert/ti_es_distance_sensor_package))

**Test Procedure:**
- Collect data from each sensor.
- Validate the accuracy and consistency of the readings.

**Confirmation:** [ ] Implemented and tested successfully.

---

## ✅ 8. System Control (PID Controller)

**Objective:** Maintain precise control over the telescope's orientation.

**Implementation:**
- Implement a PID controller to adjust motor movements based on sensor feedback.

**Test Procedure:**
- Introduce disturbances to the system.
- Observe the PID controller's response in stabilizing the telescope.

**Confirmation:** [ ] Implemented and tested successfully.

---

## ✅ 9. Actuator Control

**Objective:** Control actuators to adjust the telescope's position.

**Implementation:**
- Use stepper motors controlled via A4988 drivers ([ti_es_motor_package](https://github.com/nicoripkip/ti_es_motor_package)).

**Test Procedure:**
- Send movement commands to the motors.
- Verify accurate and smooth movements.

**Confirmation:** [ ] Implemented and tested successfully.

---

## ✅ 10. User Interface with Display and Buttons

**Objective:** Provide an interface for user interaction.

**Implementation:**
- Integrate a keypad and display system ([ti_es_keypad_screen_package](https://github.com/Luco-Dev/ti_es_keypad_screen_package)).

**Test Procedure:**
- Navigate menus and input commands via the keypad.
- Confirm that the display reflects the correct information.

**Confirmation:** [ ] Implemented and tested successfully.

---

## ✅ 11. Lifecycle Management

**Objective:** Manage the states of various system components effectively.

**Implementation:**
- Employ a lifecycle manager to control the initialization and shutdown of nodes ([ti_es_lifecycle_manager_package](https://github.com/DavidAkerboom/ti_es_lifecycle_manager_package)).

**Test Procedure:**
- Transition nodes through different states.
- Ensure proper behavior during each state transition.

**Confirmation:** [ ] Implemented and tested successfully.

---

## Final Notes

This document serves as a comprehensive checklist for verifying the functionality and compliance of the autonomous telescope project with the specified embedded system requirements. Each feature should be thoroughly tested and confirmed before final deployment.


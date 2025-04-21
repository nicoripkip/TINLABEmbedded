# Sensor document

This document provides an overview of which sensors are used in the telescope and why they are used in the telescope


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

## ZWO ASI120mm mini Camera

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
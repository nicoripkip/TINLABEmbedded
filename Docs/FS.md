# Functional Specification


## 1 Introduction

This document provides an overview of the telescope control system. The telescope control system operates the telescope and
- Camera sensor


## 2 Firmware

### 2.1 Operating System

To give the firmware basic functionality for operation and easy task handling an operating system is used. The Operating System used is the 

### 2.2 ROS

For handling processes on the embedded Linux Environment an abstraction layer and framework is used to automate that process. The system used is the Robotic Operating System (<a href="https://docs.ros.org/en/jazzy/index.html">ROS</a>). Different nodes are used for separating tasks into their own processes. Because different timers are used to process different processes, this is the ideal solution. 

The overview of how the different packages are linked can be shown in the <a href="#">architecture diagram</a>.

## 3 Rotation system

### 3.1 Overview

The rotation system is the system that handles the rotation of telescope. The motors used are steppermotors for it's precision and gearboxes to increase the precision of the stepper motor and counter the vibrations caused by the stepper motors. Stars are located following the Equatorial Coordinate System. These coordinates are mapped on the inside of a sphere. These coordinates exists of two axis, a RA axis and a DEC axis.

To move arround these axis the telescope uses two stepper motors. Each stepper motor has it's own gyroscope in a feedback loop to validate if the stepper is on the right angle or not. 

When the telescope is in it's neutral state, The position of the motors are set to 0. When the coordinates are inserted into the system, the telescope will calculate the position it needs to turn to and the motors are started. When the setpoint of the celestial object is reached with checks from the gyroscope sensors, the reached state is toggled and the motors are turned off.

A detailed description of the locatisation system can be found in the <a href="#">research</a> here.

### 3.2 Hardware

The following hardware is used for the rotation system:

- Nema 17 steppermotors
- Nema 17 gearboxes
- Bosch BMI160 gyroscopes
- A4988 Motordrivers 

Detailed information is specified in the <a href="https://github.com/nicoripkip/TINLABEmbedded/blob/master/Docs/Hardware.md">Hardware Specification</a>.


### 3.3 System states

To make the 


### 3.4 Error messages

<table>
    <tr>
        <td>#: </td>
        <td>Error message: </td>
        <td>Warning: </td>
        <td>Critical: </td>
    </tr>
    <tr>
        <td>1 </td>
        <td>RA gyroscope sensor not responding. </td>
        <td> </td>
        <td>X </td>
    </tr>
    <tr>
        <td>2 </td>
        <td>DEC gyroscope sensor not responding. </td>
        <td> </td>
        <td>X </td>
    </tr>
    <tr>
        <td>3 </td>
        <td>RA Motor not moving. </td>
        <td> </td>
        <td>X </td>
    </tr>
    <tr>
        <td>4 </td>
        <td>DEC motor not moving. </td>
        <td> </td>
        <td>X </td>
    </tr>
</table>


### 3.5 ROS Topics

<table>
    <tr>
        <td>#: </td>
        <td>Topic: </td>
        <td>Datatype: </td>
        <td>Format: </td>
    </tr>
    <tr>
        <td>1 </td>
        <td>/ti/es/gyro_data </td>
        <td>String </td>
        <td>JSON </td>
    </tr>
    <tr>
        <td>2 </td>
        <td>/ti/es/motor_data </td>
        <td>String </td>
        <td>JSON </td>
    </tr>
    <tr>
        <td>3 </td>
        <td>/ti/es/logger_data </td>
        <td>String </td>
        <td>JSON </td>
    </tr>
</table>


## 4 Location System

### 4.1 Overview

To make sure to find the correct degree on the RA axis relative to it's zero point, the position of the telescope has to be found in Longitude and Latitude coordinates. Because the earth rotates arround it's own axis and the shape of the earth is a sphere it's position on the surface of the earth is mandatory to position the telescope for the correct star.

First this is important for calibrating the telescope into it's neutral position, which makes the telescope always facing north. 

Second this is import because the sky looks different on different places of the earth. When the longitude and latitude position are known of the location of the telescope a calculation be done where the telescope exists on the RA as on the DEC axises.

To make the System redundant, an option is added to the User Interface Module to insert manually the GPS location in longitude and latitude of the position of the telescope. This to make sure if the sensor failes, the telescope can always be used on it's accurate coordinates.

A detailed description of the locatisation system can be found in the <a href="#">research</a> here.

### 4.2 Hardware

The hardware used for the Localisation System:

- Adafruit GPS

Detailed information is specified in the <a href="https://github.com/nicoripkip/TINLABEmbedded/blob/master/Docs/Hardware.md">Hardware Specification</a>.

### 4.3 Error messages

When the GPS module failes it generates a few error messages. These error messages are:

<table>
    <tr>
        <td>#: </td>
        <td>Error message: </td>
        <td>Warning: </td>
        <td>Critical: </td>
    </tr>
    <tr>
        <td>1 </td>
        <td>GPS Sensor not responding. </td>
        <td> </td>
        <td>X </td>
    </tr>
    <tr>
        <td>2 </td>
        <td>Can't connect to satelites. </td>
        <td> </td>
        <td>X </td>
    </tr>
</table>


### 4.4 ROS Topics

<table>
    <tr>
        <td>#: </td>
        <td>Topic: </td>
        <td>Datatype: </td>
        <td>Format: </td>
    </tr>
    <tr>
        <td>1 </td>
        <td>/ti/es/gps_data </td>
        <td>String </td>
        <td>JSON </td>
    </tr>
    <tr>
        <td>3 </td>
        <td>/ti/es/logger_data </td>
        <td>String </td>
        <td>JSON </td>
    </tr>
</table>



## 5 User Interface System


### 5.1 Overview

To feed coordinates into the system an input module is needed. This input module is constructed of a keypad an a display to insert the coordinates and to validate it's correctness. The display is besides validating the coordinates also used to display any error messages and used for informing the user of the state of the telescope.

The keypad is also used besided feeding coordinates into the system for navigating through the menu of the telescope. In the menu different things can be selected. These are the following menu options: 

- Insert manual location.
- Insert manual celestial object location.
- Select preset location.
- Select preset celestial object.

To navigate the menu different keys are used for different functions.

- The 1...9 keys are used to input numbers into the system.
- The X key is used to select an option.
- The A key is used to go back from an option.


### 5.2 Hardware

The hardware used for the User Interface System:

Detailed information is specified in the <a href="https://github.com/nicoripkip/TINLABEmbedded/blob/master/Docs/Hardware.md">Hardware Specification</a>.

### 5.3 Error messages

When components in the user interface module failes 

<table>
    <tr>
        <td>#: </td>
        <td>Error message: </td>
        <td>Warning: </td>
        <td>Critical: </td>
    </tr>
    <tr>
        <td>1 </td>
        <td>Keypad not responding. </td>
        <td> </td>
        <td>X </td>
    </tr>
    <tr>
        <td>2 </td>
        <td>Display not connected. </td>
        <td> </td>
        <td>X </td>
    </tr>
</table>


### 5.4 ROS Topics

<table>
    <tr>
        <td>#: </td>
        <td>Topic: </td>
        <td>Datatype: </td>
        <td>Format: </td>
    </tr>
    <tr>
        <td>1 </td>
        <td>/ti/es/gps_data </td>
        <td>String </td>
        <td>JSON </td>
    </tr>
    <tr>
        <td>3 </td>
        <td>/ti/es/logger_data </td>
        <td>String </td>
        <td>JSON </td>
    </tr>
</table>



## 6 Environmental Monitoring System

### 6.1 Overview

The telescope is an electronic and optical device that is going to be used outside the house. When people live in the more northren countries, it can be really humid outside. Because the electronics emid heat and when it's cold outside, condens can be forming onto the critical components and this can damage the compoments. To prevent damaging from happening a humidity sensor makes readings of the humidity levels inside the enclosure of the telescope.

When the telescope reaches a certain level, the humidity sensor will send a disabling request to the telescope and the telescope will shutdown. 

The outside temperature is also red with the sensor, this is handy for logging the sessions with the weather patterns.

### 6.2 Hardware

The hardware used for the environmental monitoring system:

- Temperature sensor
- Humidity sensor

Detailed information is specified in the <a href="https://github.com/nicoripkip/TINLABEmbedded/blob/master/Docs/Hardware.md">Hardware Specification</a>.

### 6.3 Error Messages

### 6.4 ROS Topics

<table>
    <tr>
        <td>#: </td>
        <td>Topic: </td>
        <td>Datatype: </td>
        <td>Format: </td>
    </tr>
    <tr>
        <td>1 </td>
        <td>/ti/es/gps_data </td>
        <td>String </td>
        <td>JSON </td>
    </tr>
    <tr>
        <td>3 </td>
        <td>/ti/es/logger_data </td>
        <td>String </td>
        <td>JSON </td>
    </tr>
</table>



## 7 Object avoidance system

### 7.1 Overview

### 7.2 Hardware

### 7.3 Error Messages

### 7.4 ROS Topics


## 8 Star tracking System

### 8.1 Overview

### 8.2 Hardware

### 8.3 Error Messages

### 8.4 ROS Topics


## 9 Logging System

### 9.1 Overview

### 9.2 Hardware

### 9.3 Error Messages

### 9.4 ROS Topics


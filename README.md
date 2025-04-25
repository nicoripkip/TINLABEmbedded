# Project TINLABS Embedded Systems

## About

This repo contains all the files for the project for the course TINLAB Embedded Systems at the Rotterdam University of Applied Sciences. This course teaches students to build their own embedded system and to document it. 

Our project focuses on developing an automated equatorial telescope mount capable of tracking visible celestial objects in the night sky. The system uses motors, sensors, and a PID controller to precisely orient the telescope and follow objects as the Earth rotates. This enables long-duration imaging, where a telescope camera can capture detailed photos of stars, planets, or deep-sky objects—especially when using longer exposure times.

To learn about the functionality of the telescope, go read the <a href="https://github.com/nicoripkip/TINLABEmbedded/blob/master/Docs/FS.md">Functional Specification</a> here.


## Requirements

- The telescope is able to be oriented using motors in the mount.
- The mount uses angle sensors to determine the current position of the mount and the direction the telescope is facing.
- Coordinates of celestial object can be entered on a keypad so the telescope can be oriented to find it.
- The entered coordinates are used to correctly point the telescope towards the celestial object.
- The entered coordinates can be viewed on a display.
- The display can show output of the system.
- When moving, the telescope avoids colliding with surrounding objects using sensors.
- The mount can be stopped with a stop button.
- The mount can be set to its starting position with a reset button.
- The mount goes into sleepmode after being inactive for a period of time to save energy.
- The humidity and temperature is measured so the user knows when not to use the telescope, since it can have negative effect on the lenses and electronics.
- A watchdog timer is used to reset the software when an unexpected error occurs.
- The telescope follows a celestial object to keep it in view using a PID controller.
- The position of the telescope is found using GPS.
- GPS coordinates can be manually entered so the system still works without GPS.
- The system writes logs to a txt file so its history can be viewed.


## Hardware

To see which hardware is used in the project and how it is configured, look at the <a href="https://github.com/nicoripkip/TINLABEmbedded/blob/master/Docs/Hardware.md">Hardware Specification</a> here.

To see which sensors are used in the project and why they are used, look at the <a href="https://github.com/nicoripkip/TINLABEmbedded/blob/master/Docs/Sensors.md">Sensor Document</a> here.

## Dependencies

- ROS2
- Ubuntu 24.04
- SMBUS (python)
- RPi.GPIO (python)
- OpenCV (python)


## Installation

To see how to setup the Raspberry Pi and install the project software, look at the <a href="https://github.com/nicoripkip/TINLABEmbedded/blob/master/Docs/Installation.md">Installation Manual</a> here.


## References

To read more about the project, checkout the this <A href="#">wiki</a> to learn more

## Authors

Nico van Ommen | Luco Berkhouwer | Clarence Lurfs | David Akerboom

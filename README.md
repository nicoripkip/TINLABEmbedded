# Project TINLABS Embedded Systems

## About

This repo contains all the files for the project for the course TINLAB Embedded Systems at the Rotterdam University of Applied Sciences. This course teaches students to build their own embedded system and to document it. 

The Project I and my team has done is to track visible celestial objects in the sky 

To learn about the functionality of the telescope, go read the <a href="#">Functional Specification</a> here.



## Hardware

To see which hardware is used in the project and how it is configured, look at the <a href="https://github.com/nicoripkip/TINLABEmbedded/blob/master/Docs/Hardware.md">Hardware Specification</a> here.


## Dependencies

- ROS2
- Ubuntu 24.04
- SMBUS (python)
- RPi.GPIO (python)
- OpenCV (python)


## Installalation

1. Clone the repo
```bash
git clone https://github.com/nicoripkip/TINLABEmbedded.git
```

2. Move into the working directory
```bash
cd TINLABEmbedded
```

3. Clone the submodules
```bash
git submodule update --init
```

4. Init colcon workspace
```bash
colcon build
```

5. Run the given script
```bash
./scripts/run_nodes
```

6. Enter password (sudo)

## References

To read more about the project, checkout the this <A href="#">wiki</a> to learn more

## Authors

Nico van Ommen | Luco Berkhouwer | Clarence Lurfs | David Akerboom

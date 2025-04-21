# Localisation

**Luco Berkouwer**  
Hogeschool Rotterdam, Wijnhaven (CMI), Netherlands  
Email: 1036570@hr.nl

---

## Abstract

Accurate localisation is a critical prerequisite for astronomical tracking systems, particularly in autonomous telescope applications. This section outlines the design and implementation of a flexible localisation module using ROS 2 and the Skyfield Python library. The system supports multiple origin selection modes and provides consistent input to a coordinate transformation pipeline. Challenges addressed include GPS signal reliability, menu interaction with embedded displays, and synchronizing serial communication within ROS 2 nodes. This localisation method forms the spatial foundation for the system described further in the companion document: [EquatorialCoordinateSystem.md](./EquatorialCoordinateSystem.md).

---

## I. Introduction

In telescope-based tracking systems, knowing the observer's position on Earth is essential for accurately determining celestial object positions. This process, commonly referred to as *localisation*, provides the geographic reference point required to convert Earth-based positions to sky-based directions.

The telescope system implemented for this project is designed for portability and variable deployment environments. As such, it must support multiple localisation strategies while integrating seamlessly with other system components via ROS 2.

---

## II. Problem Definition

A localisation system for a mobile telescope must:

- Accurately determine the observer’s location
- Operate independently of internet access
- Offer fallback modes in case GPS is unavailable
- Integrate with user inputs from a keypad and display
- Output compatible data for astronomical transformation libraries (e.g., Skyfield)

In addition, synchronizing user interaction, GPS data input, and ROS communication within a real-time application introduces technical challenges, particularly when using serial interfaces and limited onboard hardware like microcontrollers.

---

## III. Methodology

### A. System Architecture

Localisation functionality is implemented as part of a ROS 2 node named `serial_publisher`. This node acts as a bridge between user inputs (via keypad/display) and data consumers (e.g., coordinate transformers and motors).

The localisation strategy supports three operational modes:

1. **GPS Mode** – Utilizes live NMEA data from an attached GPS module via `/ti/es/gps_data`.
2. **Wijnhaven Mode** – A fallback that assumes a fixed location at Hogeschool Rotterdam.
3. **Custom Mode** – Placeholder for future enhancements (e.g., user-defined lat/lon or WiFi-based geolocation).

### B. Skyfield Integration

The Skyfield library is used to represent Earth locations through its `Topos` API. It also handles celestial mechanics, allowing conversion from Earth-based locations to celestial coordinates.

However, the localisation module itself does not handle the transformation to equatorial coordinates. For that functionality, please refer to:  
📎 [EquatorialCoordinateSystem.md](./EquatorialCoordinateSystem.md)

---

## IV. Implementation

### A. Menu System

The user selects localisation mode through a keypad interface connected via UART. Visual feedback is provided through both OLED and LCD displays.

#### Menu Options

| Key         | Function                          |
|-------------|-----------------------------------|
| `#`         | Cycle through celestial targets   |
| `*`         | Confirm celestial target          |
| `A`         | Cycle through localisation modes  |
| `C`         | Confirm localisation mode         |

Once confirmed, the system collects the location data (either from GPS or preset), packages it into a JSON object, and publishes it to ROS.

### B. GPS Processing

GPS data is received as a JSON string on the `/ti/es/gps_data` topic. The node verifies that latitude and longitude fields are present before passing the data on.

If GPS data is unavailable (due to environmental interference or signal loss), users can fall back on Wijnhaven or Custom modes.

---

## V. Challenges Encountered

### A. GPS Reliability

Indoor environments or urban canyons often interfere with GPS acquisition. To mitigate this, the Wijnhaven preset was added as a reliable fallback. However, future improvements could include differential GPS (DGPS) or GNSS fusion.

### B. Serial Timing Conflicts

Simultaneously handling keypad input, display output, and GPS processing on a shared serial interface required careful timer tuning. ROS 2 timers and callback priorities were adjusted to ensure responsiveness.

### C. ROS Message Synchronization

Synchronizing user-driven menu selections with incoming GPS data required state management inside the node. Menu confirmation only triggers coordinate publishing if valid GPS data is available, otherwise a structured error message is sent.

---

## VI. Conclusion

The localisation system developed for this project successfully supports real-time and fallback geolocation modes. It offers:

- Robust fallback options
- Seamless integration with ROS 2
- Compatibility with Skyfield for further celestial transformation

Future iterations may improve user flexibility by supporting WiFi-based positioning or offline caching of prior GPS fixes.

For detailed discussion of equatorial coordinate transformation techniques, refer to:  
📎 [EquatorialCoordinateSystem.md](./EquatorialCoordinateSystem.md)


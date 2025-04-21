# Localisation

## Overview

Localisation in this context means figuring out **where the telescope is starting from**, so it knows **how to find the correct direction in the sky**. This system supports three start modes:

1. **GPS-based start** (real-time location)
2. **Fixed location** (Wijnhaven, Rotterdam)
3. **Custom input**

## How It Works

The localisation process gathers the starting position either from a **GPS module**, a **preset location**, or a **manual input**. It then uses that information to determine where the telescope is currently positioned on Earth.

That starting point is passed into the Skyfield library, which is responsible for converting that Earth position into something the telescope can use to aim.

### Modes Explained

#### 1. GPS Start
- Pulls live coordinates from the `/ti/es/gps_data` topic
- Requires a valid GPS fix
- Automatically feeds live latitude and longitude into the system

#### 2. Wijnhaven Start
- Uses the fixed location of Hogeschool Rotterdam (Wijnhaven)
- Coordinates: `51.9163° N, 4.4861° E`
- Works even without GPS

#### 3. Custom Start
- Placeholder for user-defined input
- Can be expanded for manual coordinate entry or a map interface

## Coordinate Generation

Based on the selected mode:
- If **GPS** is chosen, the latest valid GPS data is used
- If **Wijnhaven**, the coordinates are generated using Skyfield
- If **Custom**, a default or user-specified location is used

The output is always a dictionary like this:

```json
{
  "type": "gps",
  "lat": 51.9163,
  "lon": 4.4861
}
```

Or for non-GPS modes:

```json
{
  "type": "coords",
  "ra": "02;31;49",
  "dec": "+89;15;51"
}
```

## Technical Summary

- The `serial_publisher` node manages menu input and GPS handling
- It listens to GPS updates and sends the selected coordinates to other parts of the system
- Skyfield is used under the hood to calculate celestial positions based on this starting point

## Related Topics

- For the actual coordinate transformation logic, see:  
  [equatorialcoordinatesystem.md](./EquatorialCoordinateSystem.md)


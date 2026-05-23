# Auto-Fill Fresh Water System for 48' Novatech Trawler

## Project Goal
Design and build a system to automatically maintain the water level in the boat's fresh water tank. The system must fill the tank when water is missing and automatically shut off when full, eliminating the need for manual monitoring and preventing water waste.

## Boat Facts & Specifications
* **Vessel:** 48' Novatech trawler
* **Fresh Water Capacity:** 100 gallons

## Design & Physical Constraints
1. **Construction:** Prefer off-the-shelf components from hardware stores. 3D printing is acceptable. Custom fabrication or welding should be avoided unless it is a last resort.
2. **Overflow Protection:** Cannot use a supplementary reservoir or a float switch positioned above the fill line due to the tank's built-in overflow protection (it will drain extra water).
3. **Tank Access:** Access is limited to a capped pipe (approximately 1.5" in diameter) located inside a recessed cabinet in the rear of the boat. This cabinet also houses the fresh water washdown access.

## Initial Work Streams
To kick off the project, we need to solve a few core engineering challenges. We can tackle these as parallel or sequential work streams:

### 1. Water Level Sensing
Since we cannot use a traditional float switch above the fill line and are constrained by a 1.5" pipe, we need a reliable way to measure the water level.
* **Potential Approaches:**
  * **Hydrostatic Pressure Sensor:** A submersible pressure transducer dropped down the 1.5" pipe to the bottom of the tank. Extremely reliable for deep tanks.
  * **Ultrasonic / Time-of-Flight Sensor:** Mounted to the inside of a custom 3D-printed cap for the 1.5" pipe, pointing downward to measure the distance to the water's surface.
  * **Capacitive / Non-Contact Sensor:** If the tank material is non-metallic and accessible, sensors could be strapped to the outside.

### 2. Water Control (Valve System)
We need a way to automatically turn the dock water on and off based on the sensor's readings.
* **Potential Approaches:**
  * **Solenoid Valve:** A standard 12V or 110V normally-closed brass or plastic solenoid valve connected inline with the dock water hose before it enters the tank. 
  * **Motorized Ball Valve:** Slower to close but doesn't require holding current and causes less "water hammer" effect on the pipes.

### 3. Controller & Logic
The "brain" of the system that reads the sensor and commands the valve.
* **Potential Approaches:**
  * **Microcontroller (e.g., ESP32 / Arduino):** Cheap, widely available, and can easily interface with pressure/ultrasonic sensors and relays. Can also provide Wi-Fi/Bluetooth monitoring if desired.
  * **Off-the-shelf Level Controller:** There might be ready-made industrial/RV relay controllers that take a standard sensor input and trigger a switch, requiring minimal programming.

### 4. Power & Safety
* **Power Source:** Will the system run on the boat's 12V/24V DC battery bank, or 110V AC shore power? DC is usually preferred for safety around water.
* **Fail-safes:** Implementing redundant shut-offs (e.g., a hard time-limit on how long the valve can remain open) to prevent flooding if a sensor fails.

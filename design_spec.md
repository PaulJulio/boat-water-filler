# System Design Specification

## Project Overview
The primary goal is to design a system to automatically keep a 48' Novatech trawler's fresh water tank full without manual intervention or wasting water, working within the constraints of a 1.5" capped pipe access and existing built-in overflow protection.

## The Pivot: Digital Panel Upgrade
Instead of simply adding a standalone water-fill controller, we are upgrading the boat's entire tank monitoring system. The boat currently has an analog monitoring system that we will remove, repurposing the existing wiring to the tank senders for a new, modernized digital system.

### Current System (To be Replaced)
* A single analog gauge with a physical on/off rotary switch.
* A selector switch with 6 settings: 
  1. Fresh Water
  2. Diesel Aft
  3. Diesel Port
  4. Diesel Starboard
  5. Unused
  6. Unused

### New System Requirements
* **Display:** A single digital screen.
* **Power:** Physical on/off switch.
* **Monitoring:** When turned on, the screen must display the levels of all 4 active tanks simultaneously, showing a `00-99%` readout for each.
* **Control:** Manage the fresh water auto-fill system with 3 selectable modes:
  * `Off` - Auto-fill disabled.
  * `Auto` - Maintains water level automatically (e.g., between 50-75% to prevent overflow).
  * `Fill` - Manual override to begin filling.

## Technical Approach (Draft)
By reusing the existing wiring, the new microcontroller (e.g., ESP32) will act as the "gauge" for all 4 tanks. It will send a reference voltage through the existing resistive senders in each tank and measure the voltage drop via its ADC pins (potentially using voltage dividers or I2C sensors like the INA219) to calculate the fill percentages. It will also control a solenoid or motorized ball valve for the fresh water intake based on the selected fill mode.

---

## Appendix: Prior Sensor Exploration
Before deciding to completely replace the gauge panel and reuse the existing sender wiring, several other options were brainstormed and documented for posterity:

1. **Piggybacking the Analog Gauge:** Using an INA219 voltage sensor to read the 12V signal on the existing analog gauge without removing it. (Superseded by full panel replacement).
2. **Submersible Hydrostatic Pressure Sensor:** Dropping a weighted transducer down the 1.5" pipe to measure the water weight.
3. **Time-of-Flight / Ultrasonic Sensor:** Pointing a laser or sound wave down from a 3D-printed cap. Dismissed due to the likelihood of false reflections in the 1.5" metal pipe and condensation issues.
4. **Dead Reckoning:** Using flow meters on the inlet and outlet hoses to calculate the remaining water via math (`Level = In - Out`). Dismissed due to compounding drift over time.

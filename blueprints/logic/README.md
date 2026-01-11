# Logic Blueprints

This directory contains hardware-agnostic logic blueprints. Unlike manufacturer-specific blueprints, these are designed to work with any device (Zigbee, Z-Wave, WiFi, or Matter) that provides the required sensor data or entity types.

## Humidity-Controlled Fan with Safety Timer (`humidity_fan_control.yaml`)

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fmerichar%2Fha-blueprints%2Fmain%2Fblueprints%2Flogic%2Fhumidity_fan_control.yaml)

This blueprint automates an exhaust fan based on humidity levels. It uses a dual-threshold (hysteresis) approach to ensure the fan doesn't "stutter" near the trigger point and includes a safety timeout to prevent the fan from running indefinitely if the humidity remains high.

### Operation
* **Trigger High:** When the humidity sensor rises above the **Activation Threshold**, the fan turns on.
* **Trigger Low:** When the humidity sensor drops below the **Deactivation Threshold**, the fan turns off.
* **Safety Timeout:** If the fan remains on for a continuous period exceeding the **Safety Timeout**, it will force-stop. This prevents excessive wear on the motor during naturally humid days.

### Prerequisites
* **Humidity Sensor:** A sensor entity with the `humidity` device class (e.g., an Inovelli switch, a dedicated Zigbee environment sensor, or a multi-sensor).
* **Target Entity:** The fan or switch entity that controls the physical exhaust fan.

### Configuration
* **Activation Threshold:** The percentage (default 70%) at which the fan should start.
* **Deactivation Threshold:** The percentage (default 60%) at which the fan should stop.
* **Safety Timeout:** The maximum duration in minutes (default 30) the fan is allowed to run before being forced off.

### Setup Example (Guest Bathroom)
1. **Sensor:** `sensor.guest_bath_switch_humidity`
2. **Fan:** `switch.guest_bath_fan`
3. **Configuration:**
    * **Activation Threshold:** 65%
    * **Deactivation Threshold:** 55%
    * **Safety Timeout:** 15 Minutes

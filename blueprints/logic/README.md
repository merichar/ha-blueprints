# Logic Blueprints

This directory contains hardware-agnostic logic blueprints. Unlike manufacturer-specific blueprints, these are designed to work with any device (Zigbee, Z-Wave, WiFi, or Matter) that provides the required sensor data or entity types.

---

## Automation Blueprints

### Humidity-Controlled Fan with Safety Timer (`humidity_fan_control.yaml`)

[![Open your Home Assistant instance and show the blueprint import dialog.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fmerichar%2Fha-blueprints%2Fmain%2Fblueprints%2Flogic%2Fhumidity_fan_control.yaml)

This blueprint automates an exhaust fan based on humidity levels. It uses a dual-threshold approach to ensure the fan doesn't "stutter" near the trigger point and includes a safety timeout to prevent indefinite run-times.

#### Operation
* **Trigger High:** When the humidity sensor rises above the **Activation Threshold**, the fan turns on.
* **Trigger Low:** When the humidity sensor drops below the **Deactivation Threshold**, the fan turns off.
* **Safety Timeout:** If the fan remains on for a continuous period exceeding the **Safety Timeout**, it will force-stop. This prevents excessive wear on the motor during naturally humid days.

#### Prerequisites
* **Humidity Sensor:** A sensor entity with the `humidity` device class (e.g., an Inovelli switch, a dedicated Zigbee environment sensor, or a multi-sensor).
* **Target Entity:** The fan or switch entity that controls the physical exhaust fan.


#### Configuration
* **Activation Threshold:** The percentage (default 70%) at which the fan should start.
* **Deactivation Threshold:** The percentage (default 60%) at which the fan should stop.
* **Safety Timeout:** The maximum duration in minutes (default 30) the fan is allowed to run before being forced off.


#### Setup Example (Guest Bathroom)
1. **Sensor:** `sensor.guest_bath_switch_humidity`
2. **Fan:** `switch.guest_bath_fan`
3. **Configuration:**
    * **Activation Threshold:** 65%
    * **Deactivation Threshold:** 55%
    * **Safety Timeout:** 15 Minutes


---

## Script Blueprints

### Disco Lighting Mode (`disco_mode.yaml`)

[![Open your Home Assistant instance and show the blueprint import dialog.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fmerichar%2Fha-blueprints%2Fmain%2Fblueprints%2Flogic%2Fdisco_mode.yaml)

Rapidly cycles every light in selected areas to a unique, 100% saturated random color. Includes high-performance hybrid logic for mixed lighting environments.

#### Operation
* **Deep Expansion:** Recursively flattens "Groups of Groups" into individual bulb commands.
* **Bop Logic:** Only updates a randomized subset of lights per cycle for organic, multi-color chaos.
* **Hybrid Support:** Auto-detects `hs`, `rgb`, and `xy` capabilities.
* **Strobe Mode:** White-only lights randomly flash between 0% and target brightness.
* **Optimization:** Performs capability checks once upon execution to minimize network and CPU overhead.

#### Prerequisites
* **Hue Hub (Recommended):** This script sends frequent local API calls.

#### Configuration
* **Brightness:** Global brightness level for the disco (default 100%).
* **Bop Count:** Number of individual bulbs to change per cycle (default 3).
* **Transition Speed:** Fade duration between colors (default 0.3s).
* **Refresh Rate:** Delay before the next color shift (default 0.8s).

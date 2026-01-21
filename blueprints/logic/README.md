# Logic Blueprints

Hardware-agnostic automation blueprints that work with any compatible device.

## Logic Humidity: Control Fan (`humidity_control_fan.yaml`)

[![Open your Home Assistant instance and show the blueprint import dialog.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fmerichar%2Fha-blueprints%2Fmain%2Fblueprints%2Flogic%2Fhumidity_control_fan.yaml)

Automates a fan based on humidity levels using dual thresholds and a safety timeout. Commonly used for bathroom exhaust fans.

### Operation
* **High threshold:** Fan turns on when humidity rises above the activation threshold
* **Low threshold:** Fan turns off when humidity drops below the deactivation threshold
* **Maximum runtime:** Forces fan off after continuous run-time limit to prevent excessive motor wear

### Prerequisites
* **Humidity Sensor:** Sensor entity with `humidity` device class
* **Target Entity:** Fan or switch entity controlling the fan

### Configuration
* **Activation Threshold:** Humidity percentage to start the fan (default 70%)
* **Deactivation Threshold:** Humidity percentage to stop the fan (default 60%)
* **Maximum Runtime:** Maximum continuous run-time in minutes (default 30)

### Setup Example (Pink Bathroom)
1. **Sensor:** `sensor.pink_bathroom_fan_wall_switch_humidity`
2. **Fan:** `fan.pink_bathroom_exhaust_fan`
3. **Configuration:**
    * **Activation Threshold:** 65%
    * **Deactivation Threshold:** 55%
    * **Maximum Runtime:** 15 Minutes
4. **Name your automation:** `Pink Bathroom Humidity: Control Fan`

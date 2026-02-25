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

---

## Logic Presence: Control (`presence_control.yaml`)

[![Open your Home Assistant instance and show the blueprint import dialog.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fmerichar%2Fha-blueprints%2Fmain%2Fblueprints%2Flogic%2Fpresence_control.yaml)

Presence-driven automation with configurable occupied and vacated actions. Any new presence event while the vacated timer is running resets the countdown.

### Operation
* **On Occupied:** Runs the configured actions when the presence sensor turns on.
* **On Vacated:** Starts a countdown when presence clears. Runs the configured actions after the timeout elapses. Any new presence event resets the timer.

### Prerequisites
* **Presence Sensor:** Any `binary_sensor` entity. For complex presence logic (multiple sensors, zone occupancy, etc.), combine them into a single template binary sensor upstream.

### Configuration
* **Presence Sensor:** The `binary_sensor` to monitor.
* **On Occupied:** Actions to run when presence is detected (scene, script, service call, etc.).
* **Vacated Timeout:** Seconds to wait after presence clears before running vacated actions (default 900).
* **On Vacated:** Actions to run after the timeout (turn off lights, TV, etc.).

### Setup Example (Laundry Room)
1. **Sensor:** `binary_sensor.laundry_room_presence`
2. **On Occupied:**
    ```yaml
    - action: light.turn_on
      target:
        entity_id: light.laundry_room
    - action: button.press
      target:
        entity_id: button.laundry_room_tv_control_power_toggle
    ```
3. **Vacated Timeout:** 1800 seconds (30 minutes)
4. **On Vacated:**
    ```yaml
    - action: light.turn_off
      target:
        entity_id: light.laundry_room
    - action: button.press
      target:
        entity_id: button.laundry_room_tv_control_power_toggle
    ```
5. **Name your automation:** `Laundry Room Presence: Control`

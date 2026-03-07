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

Presence-driven automation using a motion sensor and a boolean entity (switch, light, or `input_boolean`) to track occupancy state. The blueprint manages the boolean on/off; optional action lists run on each transition. Any new presence event while the vacated timer is running resets the countdown.

### Operation
* **Occupied:** Turns the boolean on and runs occupied actions when presence is detected, provided the reoccupancy delay has elapsed since the boolean was last turned off.
* **Vacated:** Starts a countdown when presence clears. Turns the boolean off and runs vacated actions after the timeout elapses. Any new presence event resets the timer.
* **Reoccupancy delay:** After the boolean is turned off (automatically or manually), suppresses re-activation for a configurable period. Prevents re-triggering while the occupant is leaving, and handles sensors that briefly clear while the space is still occupied.

### Prerequisites
* **Presence Sensor:** Any `binary_sensor` entity. For complex presence logic (multiple sensors, zone occupancy, etc.), combine them into a single template binary sensor upstream.
* **Presence Boolean:** A `switch`, `light`, or `input_boolean` to track occupancy state. Use a physical switch or light to directly control a device, or an `input_boolean` as a virtual indicator paired with separate action lists.

### Configuration
* **Presence Sensor:** The `binary_sensor` to monitor.
* **Presence Boolean:** The entity that tracks occupancy state.
* **Reoccupancy Delay:** Seconds to suppress re-triggering after the boolean turns off (default 60).
* **Vacated Timeout:** Seconds to wait after presence clears before turning off the boolean and running vacated actions (default 900).
* **Actions When Occupied:** Actions to run when the space becomes occupied. Optional if the boolean turning on is sufficient.
* **Actions When Vacated:** Actions to run when the space is vacated. Optional if the boolean turning off is sufficient.

### Setup Examples

**Physical switch (Inovelli Blue, Laundry Room)**

The switch IS the presence indicator — turning on/off controls the lights directly. No action lists needed.

1. **Sensor:** `binary_sensor.laundry_room_presence`
2. **Presence Boolean:** `light.laundry_room_switch`
3. **Reoccupancy Delay:** 60 seconds (default)
4. **Vacated Timeout:** 1800 seconds (30 minutes)
5. **Name your automation:** `Laundry Room Presence: Control`

**Virtual indicator with action lists (no physical switch)**

Use an `input_boolean` as the presence state and define explicit action lists.

1. **Sensor:** `binary_sensor.laundry_room_presence`
2. **Presence Boolean:** `input_boolean.laundry_room_occupied`
3. **Reoccupancy Delay:** 60 seconds (default)
4. **Vacated Timeout:** 1800 seconds (30 minutes)
5. **Actions When Occupied:**
    ```yaml
    - action: light.turn_on
      target:
        entity_id: light.laundry_room
    ```
6. **Actions When Vacated:**
    ```yaml
    - action: light.turn_off
      target:
        entity_id: light.laundry_room
    ```
7. **Name your automation:** `Laundry Room Presence: Control`

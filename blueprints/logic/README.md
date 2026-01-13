# Logic Blueprints

Hardware-agnostic automation blueprints that work with any compatible device.

---

## Automation Blueprints

### Logic: Humidity Fan Control (`humidity_fan_control.yaml`)

[![Open your Home Assistant instance and show the blueprint import dialog.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fmerichar%2Fha-blueprints%2Fmain%2Fblueprints%2Flogic%2Fhumidity_fan_control.yaml)

Automates a fan based on humidity levels using dual thresholds and a safety timeout. Commonly used for bathroom exhaust fans.

#### Operation
* **High threshold:** Fan turns on when humidity rises above the activation threshold
* **Low threshold:** Fan turns off when humidity drops below the deactivation threshold
* **Maximum runtime:** Forces fan off after continuous run-time limit to prevent excessive motor wear

#### Prerequisites
* **Humidity Sensor:** Sensor entity with `humidity` device class
* **Target Entity:** Fan or switch entity controlling the fan

#### Configuration
* **Activation Threshold:** Humidity percentage to start the fan (default 70%)
* **Deactivation Threshold:** Humidity percentage to stop the fan (default 60%)
* **Maximum Runtime:** Maximum continuous run-time in minutes (default 30)

#### Setup Example (Pink Bathroom)
1. **Sensor:** `sensor.pink_bathroom_fan_wall_switch_humidity`
2. **Fan:** `fan.pink_bathroom_exhaust_fan`
3. **Configuration:**
    * **Activation Threshold:** 65%
    * **Deactivation Threshold:** 55%
    * **Maximum Runtime:** 15 Minutes
4. **Name your automation:** `Pink Bathroom: Humidity Fan Control`


---

## Script Blueprints

### Logic: Random Color Bop (`random_color_bop.yaml`)

[![Open your Home Assistant instance and show the blueprint import dialog.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fmerichar%2Fha-blueprints%2Fmain%2Fblueprints%2Flogic%2Frandom_color_bop.yaml)

Rapidly cycles lights to random colors by updating a configurable subset per iteration, creating organic multi-color party effects.

#### How It Works
* **Deep Expansion:** Recursively flattens nested groups into individual bulb commands
* **Subset Updates:** Only updates a randomized subset of lights per cycle for organic, multi-color effects
* **Hybrid Support:** Auto-detects `hs`, `rgb`, and `xy` color capabilities
* **Strobe Mode:** White-only lights randomly flash between 0% and target brightness
* **Performance:** Capability checks run once at execution to minimize overhead

#### Prerequisites
* **Hue Hub (Recommended):** Script sends frequent local API calls

#### Configuration
* **Brightness:** Global brightness level (default 100%)
* **Bop Count:** Number of individual bulbs to update per cycle (default 3)
* **Transition Speed:** Fade duration between colors (default 0.3s)
* **Refresh Rate:** Delay between color shifts (default 0.8s)

#### Setup Example (Family Room)
1. **Areas:** Select areas to include (e.g., `area.family_room`)
2. **Configuration:**
    * **Brightness:** 100%
    * **Bop Count:** 3
    * **Transition Speed:** 0.3s
    * **Refresh Rate:** 0.8s
3. **Name your script:** `Family Room: Random Color Bop`

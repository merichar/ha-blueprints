# Script Blueprints

## Random Color Bop (`random_color_bop.yaml`)

[![Open your Home Assistant instance and show the blueprint import dialog.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fmerichar%2Fha-blueprints%2Fmain%2Fblueprints%2Fscript%2Frandom_color_bop.yaml)

Rapidly cycles lights to random colors by updating a configurable subset per iteration, creating organic multi-color party effects.

### How It Works
* **Deep Expansion:** Recursively flattens nested groups into individual bulb commands
* **Subset Updates:** Only updates a randomized subset of lights per cycle for organic, multi-color effects
* **Hybrid Support:** Auto-detects `hs`, `rgb`, and `xy` color capabilities
* **Strobe Mode:** White-only lights randomly flash between 0% and target brightness
* **Performance:** Capability checks run once at execution to minimize overhead

### Prerequisites
* **Hue Hub (Recommended):** Script sends frequent local API calls

### Configuration
* **Brightness:** Global brightness level (default 100%)
* **Bop Count:** Number of individual bulbs to update per cycle (default 3)
* **Transition Speed:** Fade duration between colors (default 0.3s)
* **Refresh Rate:** Delay between color shifts (default 0.8s)

### Setup Example (Family Room)
1. **Areas:** Select areas to include (e.g., `area.family_room`)
2. **Configuration:**
    * **Brightness:** 100%
    * **Bop Count:** 3
    * **Transition Speed:** 0.3s
    * **Refresh Rate:** 0.8s
3. **Name your script:** `Family Room: Random Color Bop`

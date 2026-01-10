# Inovelli Blue Series (VZM-SN)

Blueprints for Inovelli Blue Series devices (VZM30-SN, VZM31-SN, and VZM35-SN) using the ZHA integration. Optimized for Smart Bulb Mode.

## Inovelli Blue: Unified Switch Control (`inovelli_vzm_sn_smart_remote.yaml`)

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fmerichar%2Fha-blueprints%2Fmain%2Fblueprints%2Finovelli%2Fblue-series%2Finovelli_vzm_sn_smart_remote.yaml)

This blueprint provides a unified interface for cycling scenes and managing dimming levels. It treats the physical switch as a remote controller for smart bulbs or smart fans. Includes self-contained reset logic based on light state and inactivity.

### Operation
* **Button 2 (Up) Single Press:** Cycles scenes. Resets to the first scene if the light is currently off or if the switch has been inactive for the duration of the Reset Timeout.
* **Button 2 (Up) Hold:** Increases brightness by 10% increments.
* **Button 1 (Down) Single Press:** Turns off the target entity.
* **Button 1 (Down) Hold:** Decreases brightness by 10% increments.

### Prerequisites
* **Smart Bulb Mode:** The switch must have Smart Bulb Mode enabled.
* **Scene Tracker Helper:** Requires an `input_select` helper to track rotation. See [Centralized Helper Guide](../../../helpers/README.md) for setup.
* **Entity Naming:** Scenes must follow the pattern `scene.[area_prefix]_[scene_name]`.

### Configuration
* **Reset Timeout:** The number of seconds (default 300) the switch must be inactive before the next press returns to the first scene.
* **Area Prefix:** The prefix used in your scene names (e.g., `living_room`).
* **Scene Helper:** The input_select dropdown used to track the current scene.

### Setup Example (Living Room)
1. Create `input_select.living_room_scene_tracker` with options: `Bright`, `Movie`, `Ambient`.
2. Ensure scenes `scene.living_room_bright`, `scene.living_room_movie`, and `scene.living_room_ambient` exist.
3. Configure the blueprint:
    * Area Prefix: `living_room`
    * Target Entity: `area.living_room`
    * Scene Helper: `input_select.living_room_scene_tracker`

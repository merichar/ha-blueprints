# Inovelli Blue Series (VZM-SN)

Blueprints for Inovelli Blue Series devices (VZM30-SN, VZM31-SN, and VZM35-SN) using the ZHA integration. These are optimized for devices running in Smart Bulb Mode.

## Inovelli Blue: Unified Switch Control (`inovelli_vzm_sn_smart_remote.yaml`)

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fmerichar%2Fha-blueprints%2Fmain%2Fblueprints%2Finovelli%2Fblue-series%2Finovelli_vzm_sn_smart_remote.yaml)

This blueprint provides a unified interface for cycling scenes and managing dimming levels. It treats the physical switch as a remote controller for smart bulbs or smart fans.

### Operation
* Button 2 (Up) Single Press: Cycles through the Scene Tracker helper. If the target entity is currently off, it resets to the first scene in the list.
* Button 2 (Up) Hold: Increases brightness of the target entity in 10% increments until released.
* Button 1 (Down) Single Press: Turns off the target entity.
* Button 1 (Down) Hold: Decreases brightness of the target entity in 10% increments until released.

### Prerequisites
* Smart Bulb Mode: The switch must have Smart Bulb Mode enabled.
* Scene Tracker Helper: Requires an `input_select` helper to track rotation. See [Centralized Helper Guide](../../../helpers/README.md) for setup.
* Entity Naming: Scenes must follow the pattern `scene.[area_prefix]_[scene_name]`.

### Setup Example (Living Room)
1. Create `input_select.living_room_scene_tracker` with options: `Bright`, `Movie`, `Ambient`.
2. Ensure scenes `scene.living_room_bright`, `scene.living_room_movie`, and `scene.living_room_ambient` exist.
3. Configure the blueprint:
    * Area Prefix: `living_room`
    * Target Entity: `light.living_room_lights`
    * Scene Helper: `input_select.living_room_scene_tracker`

### Synchronization Note
This blueprint does not internally reset the Scene Tracker helper on a down press. To ensure synchronization when using voice assistants (Alexa) or mobile apps, use the **Logic: State-Based Scene Reset** blueprint.

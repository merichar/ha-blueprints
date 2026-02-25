# Lutron Aurora

Blueprints for the Lutron Aurora smart bulb dimmer (Z3-1BRL) using the ZHA integration.

## Lutron Aurora: Control Scene (`lutron_aurora_control_scene.yaml`)

[![Open your Home Assistant instance and show the blueprint import dialog.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fmerichar%2Fha-blueprints%2Fmain%2Fblueprints%2Flutron%2Faurora%2Flutron_aurora_control_scene.yaml)

Scene cycling and direct brightness control for the Lutron Aurora knob dimmer. Treats the knob as a controller for smart bulbs. Includes self-contained reset logic based on light state and inactivity.

### Operation
* **Knob Press:** Cycles scenes. Resets to the first scene if the light is currently off or if the knob has been inactive for the duration of the Reset Timeout.
* **Knob Rotate:** Sets brightness directly based on knob position. Rotating to minimum (0) turns off the target entity.

### How It Works

**Sequence Tracking**
The blueprint reads the Scene Tracker helper to determine which scene to activate. Each press activates the current scene and advances the tracker to the next option in the list.

**State-Based Reset**
The Scene Tracker automatically resets to the first option when the associated lights are off. This ensures the first scene always triggers after darkness, regardless of how the lights were turned off.

**Inactivity Reset**
After the configured Reset Timeout period of no knob activity, the next press returns to the first scene.

**Direct Brightness**
Rotating the knob sets brightness proportionally (knob position 1–254 maps to 1–99%). Rotating to the minimum (0) turns the lights off. This adjusts brightness without cycling scenes.

### Prerequisites
* **ZHA Integration:** The Aurora must be paired through ZHA.
* **Scene Tracker Helper:** Requires an `input_select` helper. See [Helpers Guide](../../../helpers/README.md) for setup.
* **Entity Naming:** Scenes must follow the pattern `scene.[area_prefix]_[scene_name]`.

### Configuration
* **Reset Timeout:** Seconds of inactivity before the next press returns to the first scene (default 5).
* **Area Prefix:** The prefix used in your scene names (e.g., `living_room`).
* **Scene Helper:** The `input_select` dropdown used to track the current scene.

### Setup Example (Living Room)
1. Create `input_select.living_room_scene_tracker` with options: `Bright`, `Movie`, `Ambient`.
2. Ensure scenes `scene.living_room_bright`, `scene.living_room_movie`, and `scene.living_room_ambient` exist.
3. Configure the blueprint:
    * Area Prefix: `living_room`
    * Target Entity: `area.living_room`
    * Scene Helper: `input_select.living_room_scene_tracker`
4. Name your automation: `Living Room Wall Switch: Control Scene`

# Philips Hue

Blueprints for Philips Hue remote controllers using the ZHA integration.

## Philips Hue Dimmer: Control Scene (`philips_hue_dimmer_control_scene.yaml`)

[![Open your Home Assistant instance and show the blueprint import dialog.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fmerichar%2Fha-blueprints%2Fmain%2Fblueprints%2Fphilips-hue%2Fphilips_hue_dimmer_control_scene.yaml)

This blueprint provides a unified interface for cycling scenes and managing dimming levels using the Hue Dimmer Switch. It treats the remote as a controller for smart bulbs or smart fans. Includes self-contained reset logic based on light state and inactivity.

### Operation
* **On Button Press:** Cycles scenes. Resets to the first scene if the light is currently off or if the remote has been inactive for the duration of the Reset Timeout.
* **Up Button Hold:** Increases brightness by 10% increments.
* **Off Button Press:** Turns off the target entity.
* **Down Button Hold:** Decreases brightness by 10% increments.

### How It Works

**Sequence Tracking**
The blueprint reads the Scene Tracker helper to determine which scene to activate. Each button press activates the current scene and advances the tracker to the next option in the list.

**State-Based Reset**
The Scene Tracker automatically resets to the first option when the associated lights turn off. This ensures the first scene always triggers after darkness, regardless of how the lights were turned off (remote, voice assistant, app, or automation). This state-based approach keeps the system synchronized across all control methods without requiring additional background automations.

**Inactivity Reset**
After the configured Reset Timeout period of no button presses, the next press returns to the first scene. This provides predictable behavior when returning to a room after extended absence.

### Prerequisites
* **ZHA Integration:** The Hue Dimmer must be paired through ZHA (not the Hue Bridge integration).
* **Scene Tracker Helper:** Requires an `input_select` helper to track rotation. See [Helpers Guide](../../helpers/README.md) for setup.
* **Entity Naming:** Scenes must follow the pattern `scene.[area_prefix]_[scene_name]`.

### Configuration
* **Reset Timeout:** The number of seconds (default 5) the remote must be inactive before the next press returns to the first scene.
* **Area Prefix:** The prefix used in your scene names (e.g., `living_room`).
* **Scene Helper:** The input_select dropdown used to track the current scene.

### Setup Example (Living Room)
1. Create `input_select.living_room_scene_tracker` with options: `Bright`, `Movie`, `Ambient`.
2. Ensure scenes `scene.living_room_bright`, `scene.living_room_movie`, and `scene.living_room_ambient` exist.
3. Configure the blueprint:
    * Area Prefix: `living_room`
    * Target Entity: `area.living_room`
    * Scene Helper: `input_select.living_room_scene_tracker`
4. Name your automation: `Living Room Remote: Control Scene`

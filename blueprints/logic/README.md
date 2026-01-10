# Logic Blueprints

Hardware-agnostic blueprints designed to handle the underlying automation logic and state management of the home.

## Logic: State-Based Scene Reset (`state_based_reset.yaml`)

This blueprint ensures that Scene Tracker helpers stay synchronized with the actual state of the room, regardless of how the lights were controlled.

### The Problem
When lights are turned off via voice assistants (Alexa/Google Assistant), mobile apps, or automated routines, a physical wall switch has no native way of knowing the room is dark. Without a state-based reset, the next "Up" press on a switch would trigger the next scene in the sequence rather than starting from the beginning.

### The Solution
By monitoring the `light` entity itself, this blueprint triggers a reset of the `input_select` helper whenever the light enters the `off` state. This makes the system "trigger-agnostic," ensuring a consistent experience regardless of how the lights were turned off.

### Configuration
* Light Entity: The primary light or light group for the area.
* Scene Tracker Helper: The `input_select` dropdown associated with that area.
* Reset Delay: A configurable buffer (default 5s) to prevent the helper from resetting during brief network flickers or rapid scene transitions.

### Setup
* **Light Entity:** The main light or group for the area. e.g.: `light.living_room_lights`
* **Scene Helper:** The `input_select` dropdown for that area. e.g.: `input_select.living_room_scene_tracker`
* **Delay:** A short buffer (default 5s) to prevent resets during momentary flickers or rapid scene changes. e.g.: `10`

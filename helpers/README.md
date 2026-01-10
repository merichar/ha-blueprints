# Helper Setup Guide

This project relies on Home Assistant Helpers to maintain state and provide consistent behavior across different rooms.

## Scene Tracker (Dropdown)

The Scene Tracker is an `input_select` helper that acts as a "playlist pointer" for a specific area. It allows the wall switches to know which scene to trigger next in a sequence.

### 1. Creation Steps
1. Navigate to **Settings** > **Devices & Services** > **Helpers**.
2. Click **Create Helper** and select **Dropdown**.
3. **Name:** Use the format `[Area] Scene Tracker` (e.g., `Living Room Scene Tracker`).
4. **Options:** Add your scene names in the exact order you want them to cycle.
   * *Note: The text must match the end of your scene entity IDs.*
   * *e.g.: If the option is "Movie", the scene entity must be "scene.living_room_movie".*

### 2. Behavioral Rules and State Resets
To ensure a consistent experience regardless of how lights are controlled (Voice, App, or Switch), the following logic is applied:

* **Sequence Tracking:** The helper stores the currently active scene. The wall switch blueprint reads this value to determine the "next" scene in the list.
* **State-Based Reset:** The helper should be reset to the first option (e.g., "Bright") whenever the associated light group enters an `off` state.
* **Why move reset out of the switch?** By tying the reset to the light's state rather than a button press, the system remains synchronized even when lights are turned off via Alexa, Google Assistant, or automated timers.

## Why use Helpers?
Home Assistant Scenes are "stateless." These helpers provide the necessary memory for rotation. By decoupling the "reset" logic from the physical switch, the "Up" button on your Inovelli or Hue switch will always trigger the primary scene first after the room has been dark, regardless of how the lights were previously turned off.

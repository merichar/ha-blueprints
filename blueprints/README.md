# Blueprints Library

This directory contains Home Assistant Blueprints designed for a standardized, area-aware smart home.

## Installation

To use these blueprints in your Home Assistant instance:

1. **Copy the File:** Copy the "Raw" URL of the .yaml file you want to use from this repository.
2. **Import:** In Home Assistant, navigate to Settings > Automations & Scenes > Blueprints.
3. **Add:** Click "Import Blueprint" and paste the URL.
   * Note: You may also manually create the matching directory structure in your local config/blueprints/ folder and save the code directly.

## Structure Overview

* **inovelli:** Manufacturer-specific blueprints for Inovelli Blue Series switches.
* **philips-hue:** (Planned) Battery-powered remote controllers.
* **logic:** Hardware-agnostic logic blueprints (e.g., State-Based Resets).

## The Area-Aware Pattern

Most blueprints in this repository follow a specific naming convention to simplify room management.

### 1. Naming Scenes
We utilize an Area Prefix logic. Scenes should be named using the following format:
`scene.[area]_[scene_name]`
e.g.: `scene.living_room_bright`, `scene.living_room_movie`

### 2. The Scene Tracker
Each room requires an input_select (Dropdown) helper.
* The Blueprint reads the current state of this helper.
* It uses that state to determine which `scene.[area]_[state]` to trigger.
* Refer to the [Helpers Guide](../helpers/README.md) for setup details.

### 3. State Synchronization
Because this setup utilizes Smart Bulb Mode, the "off" logic is decoupled. 
* The Switch sends the off command to the target entity.
* A Logic Blueprint monitors the light entity state and resets the Scene Tracker.
* This ensures Alexa and physical switches stay in sync.

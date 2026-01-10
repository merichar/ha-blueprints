# Blueprints Library

This directory contains Home Assistant Blueprints designed for a standardized, area-aware smart home.

## Installation

To use these blueprints in your Home Assistant instance, click the buttons below or copy the URL of the .yaml file and paste it into the Home Assistant Blueprint import page.

### Inovelli Blue: Unified Switch Control
[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fmerichar%2Fha-blueprints%2Fmain%2Fblueprints%2Finovelli%2Fblue-series%2Finovelli_vzm_sn_smart_remote.yaml)

### Manual Installation ###

1. **Copy the File:** Copy the URL of the raw .yaml file you want to use from this repository.
2. **Import:** In Home Assistant, navigate to Settings > Automations & Scenes > Blueprints.
3. **Add:** Click "Import Blueprint" and paste the URL.
   * Note: You may also manually create the matching directory structure in your local config/blueprints/ folder and save the code directly.

## Structure Overview

* **inovelli:** Manufacturer-specific blueprints for Inovelli Blue Series switches.
* **philips-hue:** (Planned) Battery-powered remote controllers.
* **logic:** (Planned) Hardware-agnostic logic blueprints.

## The Area-Aware Pattern

Most blueprints in this repository follow a specific naming convention to simplify room management.

### 1. Naming Scenes
We use an Area Prefix logic. Scenes should be named using the following format:
`scene.[area]_[scene_name]`
e.g.: `scene.living_room_bright`, `scene.living_room_movie`

### 2. The Scene Tracker
Each room requires an input_select (Dropdown) helper.
* The Blueprint reads the current state of this helper.
* It uses that state to determine which `scene.[area]_[state]` to trigger.
* Refer to the [Helpers Guide](../helpers/README.md) for setup details.

### 3. Predictability and Resets
These blueprints include built-in logic to ensure the switch remains predictable. 
* **State Reset:** If the target entity is off, the next press starts at the first scene.
* **Time Reset:** If the switch has not been used for a set duration (e.g., 5 minutes), the next press starts at the first scene.
* This ensures synchronization with voice assistants and apps without requiring extra background automations.

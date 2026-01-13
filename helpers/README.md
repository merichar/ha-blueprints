# Helper Setup Guide

Home Assistant Helpers provide persistent state for automation blueprints. This guide covers creating helpers used across this blueprint library.

## Scene Tracker

An `input_select` helper that tracks the current scene for area-based scene control.

### Setup

1. Navigate to **Settings** > **Devices & Services** > **Helpers**
2. Click **Create Helper** > **Dropdown**
3. **Name:** `[Area] Scene Tracker` (e.g., `Living Room Scene Tracker`)
4. **Options:** Scene names in the order you want them to cycle
   - Options must match your scene entity suffixes
   - Example: Option "Bright" becomes Scene `scene.living_room_bright`
   - Example: Option "Movie" becomes Scene `scene.living_room_movie`

Used by scene control blueprints to track and cycle through scenes. See individual blueprint documentation for details.

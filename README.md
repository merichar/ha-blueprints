# Home Assistant Blueprints

## Available Blueprints

### [Logic Blueprints](blueprints/logic/README.md)
Hardware-agnostic automation blueprints that work with any compatible device.

- **Humidity Fan Control** - Automate fans based on humidity with dual thresholds and a timeout
- **Random Color Bop** - Random color cycling that updates a subset of lights per iteration for party effects

### [Inovelli Blue Series](blueprints/inovelli/blue-series/README.md)
Blueprints for Inovelli Blue Series switches (VZM30-SN, VZM31-SN, VZM35-SN) using the ZHA integration.

- **Scene Control** - Unified interface for cycling scenes and managing dimming with smart bulbs

### [Philips Hue](blueprints/philips-hue/README.md)
Blueprints for Philips Hue remote controllers using the ZHA integration.

- **Dimmer Scene Control** - Scene cycling and dimming control for Hue Dimmer Switch

---

## Installation

### Import via Home Assistant
Each blueprint's README includes an import badge. Click the category links above for detailed documentation.

### Manual Installation
1. **Copy the File:** Copy the raw .yaml file URL from this repository.
2. **Import:** Navigate to Settings > Automations & Scenes > Blueprints in Home Assistant.
3. **Add:** Click "Import Blueprint" and paste the URL.
   * Alternatively, manually create the directory structure in your config/blueprints/ folder and save the file directly.

---

## Naming Conventions & Area-Aware Pattern

### Blueprint Naming
All blueprints follow a consistent naming pattern:

**`[Category]: [Optional Trigger] [Thing] Control`**

**Categories:**
- **Logic:** Hardware-agnostic automation blueprints
- **Inovelli Blue:** Inovelli-specific hardware blueprints
- **Philips Hue:** Philips Hue-specific hardware blueprints
- *Additional hardware categories as needed*

**Components:**
- **Trigger** (optional): The input or condition that activates the control
  - Include for Logic blueprints when not obvious from context
  - Omit for hardware blueprints where implicit (e.g., button press)
- **Thing**: The target device, system, or mode being controlled
- **Control**: Standardized suffix

**Examples:**
- `Logic: Humidity Fan Control` - Humidity (trigger) controls Fan
- `Inovelli Blue: Scene Control` - Button press (implicit) controls Scenes
- `Philips Hue: Dimmer Scene Control` - Button press (implicit) controls Scenes

### Automation Instance Naming
Automation instances mirror the blueprint structure with a location prefix: `[Location]: [Input/Trigger] [Thing] Control`

**Examples:**
- `Main Ensuite: Humidity Fan Control`
- `Living Room: Wall Switch Scene Control`
- `Main Bedroom: Remote Scene Control`

**For multiple remotes in the same room:** Include the remote's home location:
- `Main Bedroom: Alice Nightstand Remote Scene Control`
- `Main Bedroom: Bob Nightstand Remote Scene Control`

### Scene Naming
Scenes use an area prefix for area-aware automation:
```
scene.[area]_[scene_name]
```
**Examples:** `scene.living_room_bright`, `scene.living_room_movie`

### Helpers
Some blueprints require Home Assistant helpers for state management. See the [Helpers Guide](helpers/README.md) for setup instructions.

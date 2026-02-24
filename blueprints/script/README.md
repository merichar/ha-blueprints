# Script Blueprints

## Random Color Bop (`random_color_bop.yaml`)

[![Open your Home Assistant instance and show the blueprint import dialog.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fmerichar%2Fha-blueprints%2Fmain%2Fblueprints%2Fscript%2Frandom_color_bop.yaml)

Rapidly cycles lights to random colors by updating a configurable subset per iteration, creating organic multi-color party effects.

### How It Works
* **Deep Expansion:** Recursively flattens nested groups into individual bulb commands
* **Subset Updates:** Only updates a randomized subset of lights per cycle for organic, multi-color effects
* **Hybrid Support:** Auto-detects `hs`, `rgb`, and `xy` color capabilities
* **Strobe Mode:** White-only lights randomly flash between 0% and target brightness
* **Performance:** Capability checks run once at execution to minimize overhead

### Prerequisites
* **Hue Hub (Recommended):** Script sends frequent local API calls

### Configuration
* **Brightness:** Global brightness level (default 100%)
* **Bop Count:** Number of individual bulbs to update per cycle (default 3)
* **Transition Speed:** Fade duration between colors (default 0.3s)
* **Refresh Rate:** Delay between color shifts (default 0.8s)

### Setup Example (Family Room)
1. **Areas:** Select areas to include (e.g., `area.family_room`)
2. **Configuration:**
    * **Brightness:** 100%
    * **Bop Count:** 3
    * **Transition Speed:** 0.3s
    * **Refresh Rate:** 0.8s
3. **Name your script:** `Family Room: Random Color Bop`

---

## Media Sequence (`media_sequence.yaml`)

[![Open your Home Assistant instance and show the blueprint import dialog.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fmerichar%2Fha-blueprints%2Fmain%2Fblueprints%2Fscript%2Fmedia_sequence.yaml)

Sequential media playback for automations. Define any number of arbitrarily-sourced tracks (e.g.: local files, radio stations, direct streams) as a JSON list and run on any HA media player. The final track plays until the script is stopped.

### How It Works
* **Arbitrary track count:** Tracks are defined as a JSON array with no fixed limit
* **Auto-advance:** Each track plays for a configurable duration before the next starts
* **Final track hold:** The last track plays indefinitely until `script.turn_off` is called
* **Universal player support:** Works with any HA media player (e.g.: Chromecast, ESPHome I2S, Apple TV, PS4, Echo)
* **Flexible sources:** Local media files, HA radio browser stations, or any direct HTTP stream URL

### Configuration
* **Media Player:** Any `media_player` entity
* **Tracks:** A JSON array defined by the [Track JSON Format](#track-json-format)

### Track JSON Format

Each track is an object with:
| Field | Required | Description |
|-------|----------|-------------|
| `uri` | Yes | Full URI or URL of the media |
| `type` | No | Content type (default: `audio/mpeg`) |
| `duration` | No | Seconds before advancing. Omit or use `0` on the final track |

**Supported content types:** `audio/mpeg`, `audio/aac`, `audio/ogg`, `audio/flac`, `audio/x-wav`, `music`

**URI formats by source:**
* Local file: `media-source://media_source/local/filename.mp3`
* Radio browser: `media-source://radio_browser/<station-uuid>`
* Direct stream: `http://stream.example.com/radio.aac`

> **Note for ESPHome / I2S players:** Use direct HTTP URLs; ESPHome cannot resolve `media-source://` paths. All other player types (Chromecast, Apple TV, etc.) support `media-source://` natively.

### Example Track List

```json
[
  {
    "uri": "media-source://media_source/local/fun-disco-1.mp3",
    "type": "audio/mpeg",
    "duration": 204,
    "comment": "Local MP3, plays on any player that supports HA media source"
  },
  {
    "uri": "http://icecast.example.com:8000/disco128.aac",
    "type": "audio/aac",
    "duration": 180,
    "comment": "Direct HTTP stream, works on ESPHome I2S and all other players"
  },
  {
    "uri": "media-source://radio_browser/466858af-76b1-4e00-8f0e-29867c00084e",
    "type": "audio/aac",
    "duration": 300,
    "comment": "Disco Radio Station"
  },
  {
    "uri": "media-source://media_source/local/party-outro.mp3",
    "type": "audio/mpeg",
    "comment": "Final track: no duration, plays until disco switch is turned off"
  }
]
```

> **Note:** The `comment` field is ignored; use it to annotate tracks.

### Setup Example (Family Room)
1. **Media Player:** `media_player.family_room_tv`
2. **Tracks:** JSON array (see [Example Track List](#example-track-list))
3. **Name your script:** `Family Room: Disco Media Sequence`

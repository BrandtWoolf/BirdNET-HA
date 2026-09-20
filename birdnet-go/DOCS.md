# BirdNET-Go add-on documentation

BirdNET-Go is a realtime soundscape analyser that runs local AI inference to
detect birds (and optionally wildlife and bats) from audio, and presents the
results in a web dashboard. This add-on runs the upstream
[`ghcr.io/tphakala/birdnet-go`](https://github.com/tphakala/birdnet-go) image
under the Home Assistant Supervisor.

## Installation

1. **Settings → Add-ons → Add-on Store**.
2. ⋮ menu → **Repositories** → add `https://github.com/BrandtWoolf/BirdNET-HA`.
3. Install **BirdNET-Go**, then **Start** it.
4. Click **Open Web UI** and complete the first-run onboarding wizard
   (location, locale, audio source, optional password).

The add-on exposes the web interface on port `8080`. You can change or remove
the host port under the add-on's **Network** tab.

## Configuration

Most configuration is done inside the BirdNET-Go **web UI**, which hot-reloads
settings without a restart. The add-on options are intentionally empty so the
app owns its own configuration.

### Persistent storage

| Container path | Backed by                          | Contents                              |
| -------------- | ---------------------------------- | ------------------------------------- |
| `/config`      | `addon_config` (`/addon_configs/`) | `config.yaml` and app configuration   |
| `/data`        | Add-on data volume                 | SQLite database, audio clips, logs    |

Both are persisted and included in Home Assistant **backups** automatically.
The `share` and `media` folders are also mounted (at `/share` and `/media`)
so you can export clips to, or import audio from, Home Assistant's shared
storage.

### Timezone

The add-on inherits the timezone configured in Home Assistant
(**Settings → System → General**), so detection timestamps match your system.

## Audio input

BirdNET-Go needs an audio source. Two options:

### RTSP stream (recommended, works on any host)

Point BirdNET-Go at an RTSP audio stream in the web UI under
**Settings → Audio → Audio Sources**. Common sources:

- An ESP32 / M5Stack RTSP microphone
  (see the upstream project's hardware list).
- An `ffmpeg` RTSP feed from an existing microphone or camera.

RTSP is the most portable option and is required on macOS/Windows-based test
setups and most virtualized Home Assistant installs.

### Sound card (Linux hosts with attached hardware)

This add-on requests `audio: true`, so the Supervisor maps the host audio
subsystem (ALSA `/dev/snd`) into the container. On a Home Assistant OS or
Supervised install running on hardware with a USB sound card, select the ALSA
capture device in **Settings → Audio → Audio Sources**.

> Note: sound-card capture only works when Home Assistant runs directly on
> hardware with the sound device attached. It does not work in most VM or
> container-based installs — use RTSP there.

## Home Assistant integration (MQTT auto-discovery)

BirdNET-Go can publish detections to MQTT with Home Assistant auto-discovery,
which creates entities in Home Assistant automatically.

1. Install and start the **Mosquitto broker** add-on (this add-on declares a
   soft `mqtt:want` dependency on it) and make sure the
   [MQTT integration](https://www.home-assistant.io/integrations/mqtt/) is set
   up in Home Assistant.
2. In the BirdNET-Go web UI, go to
   **Settings → Integrations → MQTT** and enable it.
3. Set the broker to `core-mosquitto`, port `1883`, and enter the MQTT
   username/password you created for Mosquitto.
4. Enable **Home Assistant discovery**.

New detections will then appear as entities in Home Assistant.

## Updating

This add-on tracks the upstream `nightly` image tag. To pull the latest build,
use **Rebuild** on the add-on's info page (or reinstall). Your `/config` and
`/data` are preserved across updates.

## Troubleshooting

- **No detections:** confirm an audio source is configured and active under
  **Settings → Audio**, and check the add-on **Log** tab.
- **Web UI not reachable:** verify the port mapping under the **Network** tab
  and that the add-on is running.
- **Permissions/first start:** the container fixes ownership of `/config` and
  `/data` on startup; the first start after install can take a bit longer.

For upstream documentation see the
[BirdNET-Go wiki](https://github.com/tphakala/birdnet-go/wiki).

## Support

- Add-on issues: <https://github.com/BrandtWoolf/BirdNET-HA/issues>
- Upstream BirdNET-Go: <https://github.com/tphakala/birdnet-go>

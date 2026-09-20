# Changelog

## 20260823

- Initial release of the BirdNET-Go Home Assistant add-on.
- Pinned to the upstream stable release `ghcr.io/tphakala/birdnet-go:20260823`
  (multi-arch: amd64, aarch64).
- Persists configuration (`/config`) and data (`/data`) via the Supervisor.
- Exposes the web interface on port 8080 with an **Open Web UI** button.
- Maps host audio (`audio: true`) for optional sound-card capture, plus
  `share` and `media` for clip import/export.
- Declares a soft MQTT dependency for Home Assistant auto-discovery.

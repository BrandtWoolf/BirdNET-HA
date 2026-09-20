# Changelog

## nightly

- Initial release of the BirdNET-Go Home Assistant add-on.
- Wraps the upstream multi-arch `ghcr.io/tphakala/birdnet-go:nightly` image.
- Persists configuration (`/config`) and data (`/data`) via the Supervisor.
- Exposes the web interface on port 8080 with an **Open Web UI** button.
- Maps host audio (`audio: true`) for optional sound-card capture, plus
  `share` and `media` for clip import/export.
- Declares a soft MQTT dependency for Home Assistant auto-discovery.

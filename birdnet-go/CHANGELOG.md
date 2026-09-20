# Changelog

## 20260823.1

- Serve the web UI through Home Assistant **ingress** for a consistent URL and
  the **Show in sidebar** option. Direct host-port access is now optional.
- Build the add-on locally `FROM` the pinned upstream image, decoupling the
  add-on version from the upstream release tag.

## 20260823

- Initial release of the BirdNET-Go Home Assistant add-on.
- Pinned to the upstream stable release `ghcr.io/tphakala/birdnet-go:20260823`
  (multi-arch: amd64, aarch64).
- Persists configuration (`/config`) and data (`/data`) via the Supervisor.
- Exposes the web interface through Home Assistant **ingress**, so it opens at a
  consistent Home Assistant URL and supports the **Show in sidebar** option.
  Direct port access remains available as an option via the Network tab.
- Maps host audio (`audio: true`) for optional sound-card capture, plus
  `share` and `media` for clip import/export.
- Declares a soft MQTT dependency for Home Assistant auto-discovery.

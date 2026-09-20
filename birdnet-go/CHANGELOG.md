# Changelog

Version numbers below are the **add-on** version (semantic versioning). The
bundled upstream BirdNET-Go release is tracked separately in `build.yaml`.

## 1.0.2

- Map host video devices (`video: true`) so the Intel iGPU render node
  (`/dev/dri/renderD128`) is available for OpenVINO GPU acceleration on
  Intel-based hosts (e.g. Intel NUC). Fixes the "GPU device node cannot be
  opened" error in the AI model settings. Hosts without a GPU are unaffected.

## 1.0.1

- Make the ingress sidebar panel visible to non-admin users as well
  (`panel_admin: false`).

## 1.0.0

- First versioned release of the BirdNET-Go Home Assistant add-on.
- Based on upstream BirdNET-Go `20260823` (multi-arch: amd64, aarch64).
- Web UI served through Home Assistant **ingress** for a consistent URL and the
  **Show in sidebar** option; optional direct host-port access via the Network
  tab.
- Built locally `FROM` the pinned upstream image, decoupling the add-on version
  from the upstream release tag.
- Persists configuration (`/config`) and data (`/data`) via the Supervisor.
- Maps host audio (`audio: true`) for optional sound-card capture, plus
  `share` and `media` for clip import/export.
- Declares a soft MQTT dependency for Home Assistant auto-discovery.

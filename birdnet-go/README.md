# BirdNET-Go

Realtime soundscape analyser for birds, wildlife, and bats. Self-hosted, 24/7,
local AI inference with a fast web dashboard — running as a Home Assistant
add-on.

This add-on wraps the upstream, multi-arch
[`ghcr.io/tphakala/birdnet-go`](https://github.com/tphakala/birdnet-go) image
and manages it through the Home Assistant Supervisor.

## Features

- BirdNET v2.4 local AI detection (6,500+ bird species), plus optional Perch,
  BattyBirdNET, and Geomodel models from the in-app gallery.
- Svelte web dashboard with live spectrograms and detection heatmaps.
- Audio input from a sound card (Linux hosts) or RTSP streams.
- MQTT publishing with **Home Assistant auto-discovery**.
- SQLite storage persisted through the Supervisor.

## Installation

1. In Home Assistant, go to **Settings → Add-ons → Add-on Store**.
2. Click the ⋮ menu (top-right) → **Repositories**, and add:
   `https://github.com/BrandtWoolf/BirdNET-HA`
3. Find **BirdNET-Go** in the store, click **Install**, then **Start**.
4. Open the web UI with **Open Web UI** and follow the onboarding wizard. The UI
   is served through Home Assistant ingress; enable **Show in sidebar** to pin
   it to the sidebar.

See [DOCS.md](DOCS.md) for detailed configuration, audio setup, and MQTT / Home
Assistant integration.

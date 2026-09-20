# BirdNET-HA

A [Home Assistant](https://www.home-assistant.io/) add-on that runs
[BirdNET-Go](https://github.com/tphakala/birdnet-go) — a realtime, self-hosted,
local-AI soundscape analyser for birds, wildlife, and bats.

This repository is a **Home Assistant add-on repository**. It also ships a
Docker Compose stack for local development and testing outside Home Assistant.

## Install as a Home Assistant add-on

1. In Home Assistant, open **Settings → Add-ons → Add-on Store**.
2. Click the ⋮ menu (top-right) → **Repositories** and add:

   ```
   https://github.com/BrandtWoolf/BirdNET-HA
   ```

3. Install **BirdNET-Go** from the store, **Start** it, then **Open Web UI**
   and follow the onboarding wizard.

Full add-on documentation: [`birdnet-go/DOCS.md`](birdnet-go/DOCS.md).

## Repository layout

| Path                         | Purpose                                             |
| ---------------------------- | --------------------------------------------------- |
| `repository.yaml`            | Home Assistant add-on repository manifest           |
| `birdnet-go/`                | The BirdNET-Go add-on (config + docs)               |
| `birdnet-go/config.yaml`     | Add-on manifest (wraps the upstream image)          |
| `birdnet-go/DOCS.md`         | Detailed add-on documentation                       |
| `docker-compose.yml`         | Local dev stack (run BirdNET-Go without HA)         |
| `.env.example`               | Template for the local dev stack                    |

## Local development stack (without Home Assistant)

Handy for testing the container on a laptop or server.

### Prerequisites

- [Docker Desktop](https://docs.docker.com/desktop/) (or Docker Engine + Compose v2)

### Quick start

```bash
cp .env.example .env      # adjust WEB_PORT / TZ if you like
docker compose up -d      # pull image and start the container
docker compose logs -f    # watch startup logs
```

Then open http://localhost:8080 and follow the onboarding wizard. Stop with
`docker compose down`; config and data persist in `./config` and `./data`.

### Audio input on macOS / Windows

Sound-card passthrough (`--device /dev/snd`) is **Linux-only** and does not work
on macOS or Windows Docker Desktop. There, provide audio via an **RTSP stream**
configured in the web UI under *Audio Sources*. On a Linux host with a real
sound card, uncomment the `devices` block in `docker-compose.yml`.

## Credits

BirdNET-Go is developed by [@tphakala](https://github.com/tphakala) and
contributors. This repository only packages it for Home Assistant.

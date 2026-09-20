# BirdNET-HA

Home Assistant app to run [BirdNET-Go](https://github.com/tphakala/birdnet-go).

## Local Docker stack

A minimal Docker Compose stack to stand up the `birdnet-go` container locally.

### Prerequisites

- [Docker Desktop](https://docs.docker.com/desktop/) (or Docker Engine + Compose v2)

### Quick start

```bash
cp .env.example .env      # adjust WEB_PORT / TZ if you like
docker compose up -d      # pull image and start the container
docker compose logs -f    # watch startup logs
```

Then open the web UI at http://localhost:8080 and follow the onboarding wizard.

Stop the stack with `docker compose down` (your config and data persist in
`./config` and `./data`).

### Layout

| Path                 | Purpose                                       |
| -------------------- | --------------------------------------------- |
| `docker-compose.yml` | BirdNET-Go service definition                 |
| `.env.example`       | Template for local settings (copy to `.env`)  |
| `config/`            | Persisted `config.yaml` and app configuration |
| `data/`              | Persisted database, audio clips, and logs     |

### Audio input on macOS

Sound-card passthrough (`--device /dev/snd`) is **Linux-only** and does not
work on macOS or Windows Docker Desktop. On macOS, provide audio to BirdNET-Go
via an **RTSP stream** and configure it in the web UI under *Audio Sources*.
An ESP32/M5Stack RTSP microphone or an `ffmpeg` RTSP feed both work well.

On a Linux host with a real sound card, uncomment the `devices` block in
`docker-compose.yml` to pass `/dev/snd` into the container.

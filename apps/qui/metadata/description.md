# qui

A fast, modern web interface for qBittorrent. Manage multiple qBittorrent instances from a single lightweight application.

## Features

- **Multi-instance support** — Manage all your qBittorrent instances from one place
- **Cross-seed** — Automatically find and add matching torrents across trackers
- **Automations** — Rule-based torrent management with conditions and actions
- **Backups & restore** — Scheduled snapshots with multiple restore modes
- **Reverse proxy** — Transparent qBittorrent proxy for external apps
- **Fast & responsive** — Optimized for performance with large torrent collections
- **Multi-language** — English, German, French, Italian, Czech, Ukrainian, Korean, Portuguese, Chinese

## First-run setup

1. Open qui and add your qBittorrent instance:
   - **Name:** any label (e.g., "Main")
   - **Host:** `http://192.168.18.251:40243` (or your qBittorrent URL)
   - **Username:** your qBittorrent username
   - **Password:** your qBittorrent password
2. Save — qui connects and shows your torrents in a modern UI

## Data location

| Path | Content |
|---|---|
| `${APP_DATA_DIR}/config` | App config, database, automations |

## Tech stack

Go, single binary. Licensed under GPL-2.0.

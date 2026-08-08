# Shelfmark

A self-hosted book and audiobook search tool. Search across multiple sources, request books, and send downloads to your library tools.

## Features

- **Multi-source search** — Web, torrent, usenet, and IRC source support
- **Universal search** — Metadata providers (Hardcover, Open Library, Google Books) for rich discovery
- **Audiobook support** — Full audiobook search and download with dedicated processing
- **Multi-user & requests** — Share with others, let users browse and request books, manage approvals
- **Download clients** — Integrates with Prowlarr, qBittorrent, SABnzbd
- **Library integration** — Auto-imports to Calibre, Calibre-Web, Audiobookshelf, Grimmory
- **Authentication** — Built-in login, OIDC SSO, proxy auth, or Calibre-Web database
- **Real-time progress** — Unified download queue with live status updates

## First-run setup

After installing, open Shelfmark and configure in Settings:
1. **Sources** — Add Prowlarr URL + API key, or configure direct sources
2. **Download clients** — Add qBittorrent or SABnzbd connection details
3. **Download path** — Set to `/books` (maps to app data directory)

To connect qBittorrent/SABnzbd download paths, add a user-config override:

```yaml
# /root/runtipi/user-config/<store-name>/shelfmark/docker-compose.yml
services:
  shelfmark:
    volumes:
      - ${APP_DATA_DIR}/config:/config
      - ${APP_DATA_DIR}/books:/books
      - /root/runtipi/media/torrents:/root/runtipi/media/torrents
      - /root/runtipi/media/usenet:/root/runtipi/media/usenet
```

## Data locations

| Path | Content |
|---|---|
| `${APP_DATA_DIR}/config` | App config, database, artwork cache |
| `${APP_DATA_DIR}/books` | Downloaded books (default destination) |

## Tech stack

Python (Flask), Vue.js. Licensed under MIT.

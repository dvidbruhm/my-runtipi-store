# Filebrowser Quantum

A modern self-hosted web-based file manager — a major fork of the original Filebrowser with real-time indexed search, multiple sources, rich previews, and enterprise-grade authentication.

## Features

- **Real-time indexed search** — SQLite-powered search results as you type, with size and date filters
- **Multiple sources** — Mount multiple directories with include/exclude rules per source
- **Rich previews** — Thumbnails for office documents, videos, album artwork, and 3D models
- **Authentication** — Password + 2FA, OIDC, LDAP, JWT, and proxy auth
- **Sharing** — Configurable share links with permissions, expiry dates, and styling
- **Access control** — Directory-level permissions scoped to user or group
- **WebDAV** — Built-in WebDAV server for mounting as a network drive
- **API** — Long-lived API tokens with Swagger documentation at `/swagger`
- **Themes** — Multiple built-in themes with dark mode
- **Office integration** — Optional OnlyOffice integration for in-browser document editing

## First login

After installing, open the app and log in with:
- **Username:** `admin`
- **Password:** `admin`

**Change the password immediately** after first login.

## Pointing at your files

By default, Filebrowser Quantum reads from `/srv` inside the container (empty). To browse your existing files, create a user-config override:

```yaml
# /root/runtipi/user-config/<store-name>/filebrowser-quantum/docker-compose.yml
services:
  filebrowser-quantum:
    volumes:
      - ${APP_DATA_DIR}/data:/home/filebrowser/data
      - /mnt/usb-drive:/srv
```

## Data locations

| Path | Content |
|---|---|
| `${APP_DATA_DIR}/data` | Config, SQLite database, search index, thumbnail cache |
| `${APP_DATA_DIR}/srv` | Default file source (override with your path) |

## How it differs from the original Filebrowser

| Feature | Original | Quantum |
|---|---|---|
| Search | Basic filename | Real-time indexed with filters |
| Sources | Single | Multiple with rules |
| Auth | Password only | OIDC, LDAP, JWT, 2FA, proxy |
| Database | BoltDB | SQLite |
| API | No | Tokens + Swagger docs |
| WebDAV | No | Yes |
| Config | `.filebrowser.json` | `config.yaml` |

## Tech stack

Go, Vue.js, SQLite. Licensed under Apache-2.0.

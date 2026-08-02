# Minidash

A minimal, lightweight self-hosted homelab dashboard. Single Go binary, YAML config, no dependencies.

## Features

- **4 dashboard views** — default, compact, card, large (choice persists per-browser)
- **11 themes** — light, dark, sepia, Catppuccin (Frappé/Macchiato/Mocha), Nord, Dracula, Gruvbox, Tokyo Night, plus System/Auto
- **Optional sections** — group items with aggregate health dots (green/amber/red)
- **Links and notes** — notes (title + text) live alongside links in the same grid
- **Status checks** — backend pings each link (HTTP GET, status < 400 = up), shows up/down/unknown with persisted sparkline history
- **Settings page** — full links/sections management: add, edit, delete, duplicate, drag-to-reorder across sections
- **Searchable icon picker** — Simple Icons (brand logos), Lucide, Tabler — all bundled in the binary (fully offline)
- **Appearance panel** — page width, background, font, grid columns/gap, item radius/padding/border/shadow, icon sizes per view, text alignment, status-dot size/position
- **Custom CSS** — textarea whose contents inject into every page
- **Config backup/restore** — download or upload the full `config.yaml`
- **Hot-reload** — external config edits are detected and reloaded without restart

## First use

The dashboard is **public** (no login needed to view). The **Settings page** requires the password you set during installation. Use it to add/edit/reorder links and customize appearance.

## Data location

| Path | Content |
|---|---|
| `${APP_DATA_DIR}/config` | `config.yaml` (links, sections, appearance) + `status-history.json` |

## Notes

- **Docker image is built locally** on the server (`minidash:latest`). If the image is deleted (e.g., `docker system prune`), rebuild it from the source project before reinstalling.
- Single Go binary, ~7 MB image. Extremely lightweight.

## Tech stack

Go, Alpine.js, SortableJS. All assets embedded in the binary.

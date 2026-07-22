# BookOrbit

A self-hosted digital library and reading platform for ebooks, audiobooks, and comics. Organize and read your books, sync progress and annotations seamlessly across Kobo, KOReader, and the web reader, enrich your collection with metadata from multiple providers, and track reading analytics — all running on infrastructure you control.

## Features

- **Built-in web readers** — Native support for EPUB, MOBI, AZW3, PDF, comics (CBZ, CBR), and audiobooks (M4B, MP3) with no extra plugins
- **Three-way sync** — Reading progress and annotations flow bidirectionally between Kobo devices, KOReader, and the BookOrbit web reader
- **KOReader plugin** — Native on-device catalog browser with search, download, and status/rating management
- **Rich metadata** — Fetch from Google Books, Amazon, Goodreads, Open Library, Audible, ComicVine, and more
- **Multi-user & SSO** — Granular per-user permissions with OIDC support (Authentik, Keycloak, Authelia)
- **OPDS catalog** — Private feed for KOReader, Thorium, Moon+, and similar apps
- **Reading analytics** — Heatmaps, streaks, yearly goals, achievements, and dashboard widgets
- **Send-to-Kindle** — Deliver books via email
- **Book Dock** — Automated ingestion via a watched drop folder
- **Hardcover & Readwise sync** — Push reading data and highlights automatically

## First-run setup

After installing, open the app and complete the setup wizard. You'll need the **Setup Bootstrap Token** — find it in the Runtipi dashboard under this app's environment variables (`BOOKORBIT_SETUP_TOKEN`).

## Configuration

| Variable | Default | Description |
|---|---|---|
| `BOOKORBIT_POSTGRES_PASSWORD` | auto-generated | PostgreSQL password (random) |
| `BOOKORBIT_JWT_SECRET` | auto-generated | Signs login tokens (random) |
| `BOOKORBIT_SETUP_TOKEN` | auto-generated | One-time setup wizard token (random) |
| `APP_URL` | `http://localhost:8530` | External URL — **update this** if exposing via a domain (used for emails, Kobo sync, OIDC redirects) |

> **Note:** To expose BookOrbit behind a domain, update `APP_URL` in the app's environment to your full URL (e.g. `https://books.example.com`) after install.

## Data locations

| Path | Content |
|---|---|
| `${APP_DATA_DIR}/books` | Your ebook/audiobook/comic files |
| `${APP_DATA_DIR}/data` | App config, caches, metadata |
| `${APP_DATA_DIR}/postgres` | PostgreSQL database |

## Tech stack

Vue, NestJS, PostgreSQL (pgvector), Node.js. Licensed under AGPL-3.0.

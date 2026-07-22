# Librarr

**The missing \*arr for books.** Self-hosted book, audiobook, and manga search and download manager — like Sonarr/Radarr but for your reading library. Searches all configured indexers in parallel, scores results by confidence, and auto-imports into your Calibre, Audiobookshelf, Kavita, or Komga library.

## Features

- **Parallel indexer search** — searches all configured sources simultaneously with confidence scoring (title match, author match, format, seeders, file size)
- **Download management** — qBittorrent, Transmission, or SABnzbd support with auto-import on completion
- **Auto-import pipeline** — organize files by author/title, rename on import, scan into Calibre/Audiobookshelf/Kavita/Komga
- **Request workflow** — users request books, admins approve, downloads happen automatically (like Jellyseerr for books)
- **Quality profiles** — rank formats (EPUB > PDF > MOBI), auto-upgrade when a better version appears
- **Author monitoring** — follow authors and get notified when new releases are found
- **Series auto-complete** — detects gaps in series and searches for missing volumes
- **Goodreads/StoryGraph CSV import** — import your shelves and bulk-download "to-read" books
- **Torznab API** — add Librarr as an indexer in Prowlarr or Readarr (works both ways)
- **OPDS 1.2 feed** — browse your library from any e-reader app (KOReader, Moon+ Reader, Librera)
- **Multi-user auth** — session login with bcrypt, TOTP 2FA, and OIDC/SSO support
- **Tiny footprint** — single ~17MB Go binary with SQLite, ~14MB RAM idle

## First login

After installing, open the app and log in with:
- **Username:** `admin`
- **Password:** the admin password you set during installation

Additional users can be created via **Settings → User Management**.

## Prowlarr / download client setup

Connection settings for Prowlarr, qBittorrent, SABnzbd, and library managers (Calibre, Kavita, Komga, Audiobookshelf) are configured in the app's **Settings → Integrations** tab — no need to edit environment variables. The app also exposes a **Torznab API** at `/torznab/api` (use the auto-generated API key from the app's env vars) so you can add Librarr as an indexer in Prowlarr or Readarr.

## Data locations

| Path | Content |
|---|---|
| `${APP_DATA_DIR}/data` | SQLite database, settings, incoming downloads |
| `${APP_DATA_DIR}/books/ebooks` | Organized ebook library |
| `${APP_DATA_DIR}/books/audiobooks` | Organized audiobook library |
| `${APP_DATA_DIR}/books/manga` | Organized manga library |

## Tech stack

Go, SQLite (pure-Go `modernc.org/sqlite`), Tailwind CSS. Licensed under MIT.

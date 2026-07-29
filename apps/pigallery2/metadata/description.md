# PiGallery 2

A fast directory-first photo gallery website, optimized for running on low-resource servers. Point it at your photo folder and it shows your directory structure as-is.

## Features

- **Directory-first** — Your folder structure IS the gallery structure. Albums, directories, and nesting are preserved exactly
- **Fast and lightweight** — Optimized for Raspberry Pi (~50 MB RAM). Thumbnails are generated on-the-fly and cached for instant repeat views
- **Read-only** — Your photo folder is never modified
- **EXIF metadata** — Camera, lens, GPS, date, and exposure data displayed per photo
- **Timeline view** — Browse photos chronologically with date grouping
- **Map view** — Photos with GPS data plotted on an interactive map; GPX track overlay supported
- **Video support** — Plays MP4 and WebM files inline
- **Search** — Full-text search across directory names, file names, and EXIF metadata
- **Multi-user** — User accounts with role-based access control
- **Sharing** — Share galleries and directories via links with optional password protection

## Pointing PiGallery 2 at your photos

By default, PiGallery 2 reads from its internal `images` directory. To use your existing photo collection, create a user-config override at:

`/root/runtipi/user-config/<store-name>/pigallery2/docker-compose.yml`

```yaml
services:
  pigallery2:
    volumes:
      - /path/to/your/photos:/app/data/images:ro
```

The `:ro` flag ensures your photos are never modified.

## Data locations

| Path | Content |
|---|---|
| `${APP_DATA_DIR}/config` | App configuration |
| `${APP_DATA_DIR}/db` | SQLite database (metadata index) |
| `${APP_DATA_DIR}/images` | Photos (read-only — override with your photo path) |
| `${APP_DATA_DIR}/tmp` | Thumbnail generation cache |

## Tech stack

Angular, Node.js, SQLite. Licensed under MIT.

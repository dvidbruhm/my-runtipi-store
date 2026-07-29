# Filestash

A storage-agnostic file manager that works with every storage protocol. Access your files from FTP, SFTP, S3, SMB, WebDAV, IPFS, and 20+ backends through a single clean web interface.

## Features

- **Universal storage** — Connect to S3, FTP, SFTP, WebDAV, SMB, Git, IPFS, Azure, GDrive, Dropbox, and many more
- **File previewing** — Photos (including RAW), videos, PDFs, Markdown, code, and office documents
- **AI features** — Smart search, smart folders, and OCR
- **Sharing** — Generate public links with optional password protection and expiry
- **Authentication** — Built-in user management or delegate to external providers (LDAP, OAuth, WordPress, etc.)
- **Workflow engine** — Automate file operations with event-driven actions
- **Plugin architecture** — Everything is a plugin; extend or replace any component
- **Themes** — Multiple built-in themes with dark mode support

## First-run setup

After installing, open Filestash and configure your storage backend through the admin panel at `/admin`. The default admin password is set on first visit.

## Data location

| Path | Content |
|---|---|
| `${APP_DATA_DIR}/state` | App state, config, thumbnails, search index |

## Connecting to local storage

To browse files on your server (e.g., media or USB drive), create a user-config override pointing at the path:

```yaml
# /root/runtipi/user-config/<store-name>/filestash/docker-compose.yml
services:
  filestash:
    volumes:
      - ${APP_DATA_DIR}/state:/app/data/state
      - /root/runtipi/media:/mnt/media:ro
```

Then configure a "Local Storage" backend in the Filestash admin panel pointing to `/mnt/media`.

## Tech stack

Go, vanilla JavaScript. Licensed under AGPL-3.0.

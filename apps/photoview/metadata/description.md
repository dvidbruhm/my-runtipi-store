# Photoview

A simple, user-friendly photo gallery made for photographers. Point it at one or more folders on your server and it organises your media into albums that mirror your existing directory structure — no uploads, no duplication.

## Features

- **Closely tied to the filesystem** — Directories become albums and are presented exactly as they are stored, so your library stays portable
- **Automatic scanning** — New files are picked up automatically and thumbnails plus web-optimised videos are generated into a media cache for fast browsing
- **Made for photography** — RAW file formats are supported and EXIF data (camera, lens, GPS, exposure) is parsed and displayed
- **Face recognition** — Faces are detected automatically and photos of the same person are grouped together on the People page
- **Map view** — GPS-tagged photos are plotted on an interactive map (requires a free Mapbox token, see below)
- **Video support** — Common video formats play inline, transcoded on the fly for the browser
- **Sharing** — Share albums or individual media through public links, optionally protected with a password
- **Multi-user** — Each user is created along with a path on the filesystem; only photos within that path are accessible
- **Secure** — Every media resource is protected with a cookie token, passwords are properly hashed, and the API enforces a strict CORS policy

## First-run setup

1. Open the app and register the first user — this account becomes the administrator.
2. When prompted for the media path, enter `/photos`.
3. Photoview scans the folder and builds thumbnails. Large libraries take a while on the first pass; subsequent scans only pick up changes.

## Photo library

This app is wired directly to the library on the host's USB drive:

```yaml
# apps/photoview/docker-compose.yml
services:
  photoview:
    volumes:
      - ${APP_DATA_DIR}/storage:/home/photoview/media-cache
      - /pcloud-backup/Photos:/photos:ro
```

`/pcloud-backup/Photos` on the host is mounted read-only at `/photos` inside the container, so Photoview never modifies your originals.

To point it somewhere else, edit that volume line in `apps/photoview/docker-compose.yml`, commit it, and bump `tipi_version` in `apps/photoview/config.json` so Runtipi picks the change up on update. To add a second library, mount it at its own subfolder of `/photos` — a mount cannot be nested inside another mount — and enter the parent `/photos` as the media path.

### Permissions

Photoview runs as uid/gid `999` and reads the library as that user, so the files under `/pcloud-backup/Photos` must be readable by it. If scans come back empty or files are missing while the folder is clearly populated, check the USB mount's permissions on the host, e.g. with `ls -ln /pcloud-backup/Photos` — the mount options (such as `dmask`/`umask`) decide whether other users can read the drive.

## Configuration

| Variable | Default | Description |
|---|---|---|
| `PHOTOVIEW_DB_PASSWORD` | auto-generated | Password for the bundled MariaDB user |
| `PHOTOVIEW_DB_ROOT_PASSWORD` | auto-generated | Password for the bundled MariaDB root user |
| `MAPBOX_TOKEN` | unset | Optional — enables the Places/map features. Generate a free token at https://account.mapbox.com/access-tokens/ and add it to the `photoview` service's `environment` in `apps/photoview/docker-compose.yml` |

## Data locations

| Path | Content |
|---|---|
| `/pcloud-backup/Photos` (host) | Your photo library, mounted read-only at `/photos` |
| `${APP_DATA_DIR}/storage` | Media cache — thumbnails and transcoded videos |
| `${APP_DATA_DIR}/database` | MariaDB data directory (users, albums, metadata) |

## Resource notes

The bundled MariaDB container runs with a 512 MB InnoDB buffer pool, which is comfortable for large libraries. Photoview itself is idle-light, but the initial scan and video transcoding are CPU-intensive. Face recognition and video encoding can both be disabled with the `PHOTOVIEW_DISABLE_FACE_RECOGNITION` and `PHOTOVIEW_DISABLE_VIDEO_ENCODING` environment variables if you run on low-power hardware.

## Tech stack

Go, React, MariaDB. Licensed under AGPL-3.0.

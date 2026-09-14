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

## Pointing Photoview at your photos

The app ships reading from `${APP_DATA_DIR}/photos`, which starts out empty — the volume line in `docker-compose.yml` is the fallback. The real library is supplied on this server by a user-config override:

`/root/runtipi/user-config/personal-store/photoview/docker-compose.yml`

```yaml
services:
  photoview:
    volumes:
      - /mnt/usb-drive/pcloud-backup/Photos:/photos:ro
```

The override reuses the container path `/photos`, and Docker Compose merges volume entries by that container path, so this **replaces** the app's `${APP_DATA_DIR}/photos` mount rather than adding a second one to the same target. `/mnt/usb-drive/pcloud-backup/Photos` is the library on the USB drive (mounted at `/mnt/usb-drive`) — the same directory `pigallery2` and `home-gallery` are pointed at. The mount is read-only, so Photoview never modifies your originals.

To add a second library, mount it at its own subfolder of `/photos` — a mount cannot be nested inside another mount — and enter the parent `/photos` as the media path.

## Configuration

| Variable | Default | Description |
|---|---|---|
| `PHOTOVIEW_DB_PASSWORD` | auto-generated | Password for the bundled MariaDB user |
| `PHOTOVIEW_DB_ROOT_PASSWORD` | auto-generated | Password for the bundled MariaDB root user |
| `MAPBOX_TOKEN` | unset | Optional — enables the Places/map features. Generate a free token at https://account.mapbox.com/access-tokens/ and add it to the `photoview` service's `environment` in the user-config override |

## Data locations

| Path | Content |
|---|---|
| `/mnt/usb-drive/pcloud-backup/Photos` (host) | Your photo library, mounted read-only at `/photos` by the user-config override |
| `${APP_DATA_DIR}/photos` | Fallback library folder — unused while the override is in place |
| `${APP_DATA_DIR}/storage` | Media cache — thumbnails and transcoded videos |
| `${APP_DATA_DIR}/database` | MariaDB data directory (users, albums, metadata) |

## Resource notes

The bundled MariaDB container runs with a 512 MB InnoDB buffer pool, which is comfortable for large libraries. Photoview itself is idle-light, but the initial scan and video transcoding are CPU-intensive. Face recognition and video encoding can both be disabled with the `PHOTOVIEW_DISABLE_FACE_RECOGNITION` and `PHOTOVIEW_DISABLE_VIDEO_ENCODING` environment variables if you run on low-power hardware.

## Tech stack

Go, React, MariaDB. Licensed under AGPL-3.0.

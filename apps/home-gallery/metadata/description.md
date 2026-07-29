# Home Gallery

Self-hosted open-source web gallery to view your photos and videos. Features mobile-friendly UI, tagging, and AI-powered image discovery using TensorFlow.js.

## Features

- **Directory-based** — Indexes your existing photo folder structure, no duplication or uploads required
- **AI-powered discovery** — TensorFlow.js similarity search for finding similar photos (runs locally, lightweight wasm backend)
- **One-time indexing** — Initial scan builds thumbnails and embeddings, then browsing is instant
- **Video support** — Plays videos inline with generated preview thumbnails
- **Mobile-friendly** — Responsive UI optimized for phones and tablets
- **Tagging** — Organize photos with custom tags across directory boundaries
- **Streaming** — Serves optimized preview images for fast loading on slow connections
- **Watch mode** — Automatically detects new photos added to your folders

## Pointing Home Gallery at your photos

By default, Home Gallery reads from its internal `/data` directory. To use your existing photo collection, create a user-config override at:

`/root/runtipi/user-config/<store-name>/home-gallery/docker-compose.yml`

```yaml
services:
  home-gallery:
    volumes:
      - ${APP_DATA_DIR}/data:/data
      - /path/to/your/photos:/data/photos
```

Photos should be mounted as a subdirectory of `/data`. Home Gallery will index them on first run.

## Data locations

| Path | Content |
|---|---|
| `${APP_DATA_DIR}/data` | Database, thumbnails, config, embeddings |
| `/data/photos` (user-mounted) | Your photo collection (override via user-config) |

## Resource notes

Configured with `GALLERY_API_SERVER_CONCURRENT=1` for low-resource servers. For more powerful hardware, increase to 5 for faster initial indexing. The wasm ML backend is lightweight (~100 MB RAM) and much lighter than full TensorFlow/GPU-based solutions.

## Tech stack

Node.js, React, TensorFlow.js (wasm). Licensed under MIT.

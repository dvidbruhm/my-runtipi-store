# Faved

A private, open-source bookmark manager built to handle large collections and advanced use cases. Optimized for ease-of-use and efficiency. All data is stored locally — no external dependencies.

## Features

- **Nested tags** — organize bookmarks with hierarchical tags (e.g., *Go* and *Python* under *Programming Languages → Backend*)
- **Customizable tags** — color and description per tag
- **Automatic metadata** — fetches titles, descriptions, and preview images automatically
- **Duplicate detection** — warns when adding an existing bookmark
- **Instant search** and flexible **sorting**
- **Bulk actions** — delete, refetch, and tag multiple bookmarks at once
- **Multiple layouts** — card, list, and table views
- **PWA installable** — near-native app experience on mobile
- **Light/Dark mode** synced with system preference

## Integrations

- **Chrome browser extension** — save bookmarks directly from the browser
- **Bookmarklet** — lightweight save-from-any-browser tool
- **Apple Shortcuts** — integrate into iOS/macOS share sheet

## Import & Migration

Import from **Chrome, Safari, Firefox, Edge** (folder structure preserved as nested tags), **Raindrop.io**, and **Pocket** — retaining original collections, tags, and data.

## First-run setup

After installing, open the app and create your account. No configuration or secrets needed — the first user is created through the web UI.

## Data location

| Path | Content |
|---|---|
| `${APP_DATA_DIR}/data` | SQLite database + bookmark preview images |

## Tech stack

React, TypeScript, Tailwind CSS, Shadcn UI, PHP 8, SQLite, Apache. Licensed under MIT.

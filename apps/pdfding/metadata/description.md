# PdfDing

A self-hosted PDF manager, viewer and editor offering a seamless user experience on multiple devices.

## Features

- **PDF viewing** — Read PDFs in the browser with continuous scrolling. Remembers your position — continue where you stopped reading
- **PDF editing** — Add text, highlights, and drawings directly in the browser
- **Signatures** — Add signatures to PDFs and access them on all devices
- **Organization** — Workspaces, collections, multi-level tagging, starring, archiving
- **Highlights & comments** — Manage and export PDF highlights in dedicated sections
- **Sharing** — Share collections and PDFs via links or QR codes with optional access control
- **SSO** — OIDC support for single sign-on
- **2FA** — TOTP and WebAuthn support
- **Markdown notes** — Attach notes to your PDFs
- **Dark mode** — With inverted color mode and custom theme colors
- **Bulk actions** — Manage multiple PDFs at once

## First-run setup

After installing, open PdfDing and create your admin account through the sign-up page.

## Data locations

| Path | Content |
|---|---|
| `${APP_DATA_DIR}/db` | SQLite database |
| `${APP_DATA_DIR}/media` | Uploaded PDF files |

## Tech stack

Python, Django, SQLite. Licensed under AGPL-3.0.

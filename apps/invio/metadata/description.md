# Invio

Self-hosted invoicing without the bloat. Create an invoice, share a link, get paid — no menus to dig through and no monthly fees. Your data stays on your own hardware, and your clients don't need an account to view or pay an invoice.

## Features

- **Invoices & quotes** — Create invoices and quotes, duplicate them, and track draft/sent/paid status
- **Client-friendly links** — Send a secure public link; clients view and download without signing up
- **Clients & products** — Reusable client and product catalog with per-client history
- **PDF generation** — Branded invoice PDFs with your own logo, accent color, and company details
- **Email delivery** — Optional SMTP so invoices can be sent straight from the app
- **Dashboard & reporting** — Revenue charts and outstanding balance overview
- **Multi-currency** — Configurable default currency and per-invoice currency
- **Users & SSO** — Multiple users with roles, plus optional OIDC login (Authentik, Keycloak, and other OIDC providers)
- **Single container** — SQLite database included; no external database required

## First-run setup

1. Open Invio and log in with the **admin username and password** you set when installing the app (shown in the Runtipi dashboard under this app's environment variables as `INVIO_ADMIN_USER` / `INVIO_ADMIN_PASS`).
2. Open **Settings** and fill in your company details, invoice numbering, default currency, and tax rates.
3. Create a client, then create your first invoice and share its link.

## Configuration

| Variable | Default | Description |
|---|---|---|
| `INVIO_ADMIN_USER` | `admin` | Admin username |
| `INVIO_ADMIN_PASS` | — | Admin password |
| `INVIO_JWT_SECRET` | auto-generated | Signs session tokens (random) |
| `DATABASE_PATH` | `/app/data/invio.db` | SQLite database location |
| `ORIGIN` | auto-detected | External origin, set automatically from Runtipi's `APP_PROTOCOL`/`APP_DOMAIN`. **Required for logins** — SvelteKit rejects form posts whose origin doesn't match |

Optional settings (SMTP for email, OIDC/SSO, rate limiting, demo mode) are documented in the project's [`.env.example`](https://github.com/kittendevv/Invio/blob/main/.env.example) — add them to the app's environment in the Runtipi dashboard if you need them.

> **Note:** `ORIGIN` is derived automatically from Runtipi's `APP_PROTOCOL`/`APP_DOMAIN`, so it follows your install's host and port (and any domain you expose it on). It is what makes the login form work — without a matching origin, Invio returns `403 Cross-site POST form submissions are forbidden`.

## Data locations

| Path | Content |
|---|---|
| `${APP_DATA_DIR}/data` | SQLite database, settings, and uploaded logos |

## Tech stack

SvelteKit frontend, Bun/Deno backend, SQLite. Licensed under the Unlicense (public domain).

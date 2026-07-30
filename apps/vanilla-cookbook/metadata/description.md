# Vanilla Cookbook

A self-hosted recipe manager designed to keep things simple — "simply vanilla." Smart ingredient parsing and display do the hard work for you, so you can get cooking with a few clicks.

## Features

- **Smart ingredient display** — Automatic parsing of quantity, unit, and ingredient from plain text. No structured data entry required
- **Unit conversion** — Convert US volumetric to metric or imperial weights. Thousands of ingredients supported. Inline temperature conversion, fractions, and ranges
- **Recipe scaling** — Scale ingredients up or down, stored in original text format
- **Nutrition parsing** — Nutrition text parsed into a structured table with per-serving detection
- **Recipe scraping** — Paste a URL or use the browser bookmarklet. Hundreds of sites supported
- **LLM assist** — Optional AI features: recipe generation from prompt, translation, ingredient cleanup, image analysis, semantic search (OpenAI, Anthropic, Google, Ollama)
- **Shopping list** — Add from recipes, view history and stats
- **Cooking logs** — Calendar view, log notes, recook with previous scaling
- **User management** — Built-in auth with optional OAuth/OIDC (GitHub, Google, Authentik, Keycloak)
- **PWA** — Install on mobile, share URLs or text to import recipes
- **Public recipes** — Share recipes and cookbooks with friends and family
- **Import/export** — Multiple formats supported
- **Automated backups** — Weekly SQLite backups with configurable retention

## First-run setup

After installing, open Vanilla Cookbook and you'll be prompted to create the admin user.

## Exposing via Cloudflare tunnel or reverse proxy

If you access Vanilla Cookbook via a domain, update the ORIGIN env via a user-config override:

```yaml
# /root/runtipi/user-config/<store-name>/vanilla-cookbook/docker-compose.yml
services:
  vanilla-cookbook:
    environment:
      - ORIGIN=https://recipes.yourdomain.com
```

Restart the app after changing. Incorrect ORIGIN will cause login/CORS errors.

## Data locations

| Path | Content |
|---|---|
| `${APP_DATA_DIR}/db` | SQLite database (recipes, users, logs) |
| `${APP_DATA_DIR}/uploads` | Uploaded recipe images |

## Tech stack

SvelteKit, Prisma, SQLite, Node.js. Licensed under GPL-3.0.

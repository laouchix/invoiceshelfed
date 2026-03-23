# Coolify Deployment (Production)

Use the compose file below when creating your service in Coolify:

- `docker-compose.coolify.yml`

This is the simplified profile (single `webapp` service + SQLite) to reduce setup failures.

If you need an advanced profile with MariaDB + worker + scheduler, use:

- `docker/production/docker-compose.coolify.yml`

## Required Environment Variables

Set these in Coolify before first deploy:

- `APP_NAME=InvoiceShelf`
- `APP_ENV=production`
- `APP_DEBUG=false`
- `APP_URL=https://your-domain.tld`
- `APP_KEY=` (optional; generated automatically on first start if empty)
- `DB_CONNECTION=sqlite`
- `DB_DATABASE=/var/www/html/storage/app/database.sqlite`
- `SESSION_DOMAIN=your-domain.tld`
- `SANCTUM_STATEFUL_DOMAINS=your-domain.tld`

## Optional First-Boot Flags

- `AUTO_RUN_MIGRATIONS=true` (recommended on first boot)
- `AUTO_RUN_DB_SEED=false`
- `AUTO_RUN_STORAGE_LINK=true`

After first successful deployment, you can set:

- `AUTO_RUN_MIGRATIONS=false`

This avoids running migrations on every restart.

## Persistence

Make sure this volume is persistent:

- `invoiceshelf_storage`

## Services Included

- `webapp` (Laravel app + Nginx/PHP-FPM)

## Health Checks

- `webapp` uses the Laravel health endpoint: `GET /up`

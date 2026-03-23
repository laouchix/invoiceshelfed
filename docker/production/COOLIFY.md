# Coolify Deployment (Production)

Use the compose file below when creating your service in Coolify:

- `docker/production/docker-compose.coolify.yml`

## Required Environment Variables

Set these in Coolify before first deploy:

- `APP_NAME=InvoiceShelf`
- `APP_ENV=production`
- `APP_DEBUG=false`
- `APP_URL=https://your-domain.tld`
- `APP_KEY=` (optional; generated automatically on first start if empty)
- `DB_CONNECTION=mariadb`
- `DB_HOST=database`
- `DB_PORT=3306`
- `DB_DATABASE=invoiceshelf`
- `DB_USERNAME=invoiceshelf`
- `DB_PASSWORD=<strong-password>`
- `DB_ROOT_PASSWORD=<strong-root-password>`
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

Make sure both volumes are persistent:

- `invoiceshelf_mysql`
- `invoiceshelf_storage`

## Services Included

- `webapp` (Laravel app + Nginx/PHP-FPM)
- `database` (MariaDB)
- `worker` (queue worker)
- `scheduler` (Laravel scheduler)

## Health Checks

- `webapp` uses the Laravel health endpoint: `GET /up`
- `database` uses `mariadb-admin ping`

# NGINX Configuration Boilerplates

This directory contains example NGINX configuration snippets.

## Files
- `single-site.conf` – Basic reverse proxy for a single service container.
- `multi-site.conf` – Example server block with multiple `location` directives.
- `security.conf` – Common security headers and rate limiting examples.

## Usage
Copy desired file to `/etc/nginx/conf.d/` or merge into your existing `nginx.conf`.
Test configuration before reload:
```
nginx -t && systemctl reload nginx
```

## Notes
Adjust upstream hostnames to match your Docker service names (e.g. `sonarr`, `radarr`).

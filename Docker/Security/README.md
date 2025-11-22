# Security / Operations Docker Stack

Includes reverse proxy (Traefik), automatic image updates (Watchtower), and management UI (Portainer).

## Services
- Traefik v3 (ports 80/443/8080)
- Watchtower (auto updates every 5 minutes)
- Portainer CE (port 9000)

## Usage
```
docker compose up -d
```

Add labels to your other service containers to route through Traefik, e.g.:
```
labels:
  - "traefik.enable=true"
  - "traefik.http.routers.sonarr.rule=Host(`sonarr.example.com`)"
  - "traefik.http.routers.sonarr.entrypoints=websecure"
  - "traefik.http.routers.sonarr.tls.certresolver=letsencrypt"
  - "traefik.http.middlewares.sonarr-headers.headers.secure=true"
```

## Notes
- Consider restricting dashboard with auth middleware.
- Watchtower can be scoped to specific containers if needed.

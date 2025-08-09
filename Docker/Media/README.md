# Media Stack Boilerplate (Docker Compose)

A reusable Docker Compose template for a complete Plex + \*arr media stack. Everything is parameterized with environment variables so you can drop this into any host and be up and running fast.

> **Includes:** Plex, Sonarr, Radarr, Bazarr, Prowlarr, Tautulli, Overseerr, DizqueTV, FlareSolverr, AudioBookshelf, and YouTubeDL-Material (+ MongoDB).

---

## ✨ Features

* Single `docker-compose.yml` with variables for ports, paths, PUID/PGID, and tags
* `.env.example` provided—copy to `.env` and customize
* Sensible healthchecks and restart policies
* External Docker network (configurable) so you can attach other services easily
* Consistent volume layout under `./Appdata`

---

## 📦 What’s in the stack

| Service            | Purpose                               | Default Host Port                                                |
| ------------------ | ------------------------------------- | ---------------------------------------------------------------- |
| Plex               | Media server                          | `host network` (Plex defaults; Web at `http://<host>:32400/web`) |
| Sonarr             | TV shows manager                      | `${SONARR_PORT_HOST:-8989}`                                      |
| Radarr             | Movies manager                        | `${RADARR_PORT_HOST:-7878}`                                      |
| Bazarr             | Subtitles                             | `${BAZARR_PORT_HOST:-6767}`                                      |
| Prowlarr           | Indexer aggregator                    | `${PROWLARR_PORT_HOST:-9696}`                                    |
| Tautulli           | Plex stats/analytics                  | `${TAUTULLI_PORT_HOST:-8181}`                                    |
| Overseerr          | Media requests                        | `${OVERSEERR_PORT_HOST:-5055}`                                   |
| DizqueTV           | Virtual live TV channels for Plex     | `${DIZQUETV_PORT_HOST:-7373}` → container `8000`                 |
| FlareSolverr       | Cloudflare-solving proxy for indexers | `${FLARESOLVERR_PORT_HOST:-8191}`                                |
| AudioBookshelf     | Audiobooks & podcasts server          | `${ABS_PORT_HOST:-13378}` → container `80`                       |
| YouTubeDL-Material | YouTube/URL downloader                | `${YTDL_MATERIAL_PORT_HOST:-8998}` → container `17442`           |
| MongoDB            | DB for YTDL-Material                  | internal only                                                    |

> Ports are configurable via `.env`. Values above show defaults.

---

## 🚀 Quick Start

1. **Clone** this repo.
2. **Copy** the environment file:

   ```bash
   cp .env.example .env
   ```
3. **Edit `.env`** and set your paths, users, groups, and timezone.
4. **Create the external network** (or change its name in `.env`):

   ```bash
   docker network create Media
   ```
5. **Start the stack**:

   ```bash
   docker compose up -d
   ```
6. Open the web UIs using the host + ports from the table above.

> For **Plex first-run**, you can optionally set `PLEX_CLAIM` in `.env` to link the server to your Plex account quickly.

---

## 🗂️ Directory Layout

```
.
├─ docker-compose.yml
├─ .env                # your real values (not committed)
├─ .env.example        # safe example template
└─ Appdata/
   ├─ Sonarr/config/
   ├─ Radarr/config/
   ├─ Bazarr/config/
   ├─ Prowlarr/config/
   ├─ Tautulli/config/
   ├─ Overseerr/config/
   ├─ DizqueTV/data/
   ├─ PlexMediaServer/config/
   └─ YTMP4/
      ├─ appdata/ audio/ video/ subscriptions/ users/ db/
```

> Application content libraries (e.g., movies, TV, downloads, NAS paths) live **outside** `Appdata` and are configured via `.env` variables.

---

## ⚙️ Configuration via `.env`

This repo ships with a **complete** `.env.example`—copy it to `.env` and customize. Key groups:

* **Global**

  * `TZ` — timezone (e.g., `Europe/London` or `UTC`)
  * `APPDATA_ROOT` — where containers store configs (default `./Appdata`)
  * `NETWORK_NAME` — external Docker network name (default `Media`)
  * `NAS_ROOT`, `BACKUP_ROOT`, `HOSTS_FILE` — optional host mounts

* **Library Paths** (map to your storage)

  * `TV_PATH`, `MOVIES_PATH`, `DOWNLOADS_PATH`, `ARCHIVE_PATH`
  * `AUDIOBOOKS_PATH`, `PODCASTS_PATH`

* **PUID/PGID**

  * Each app has `*_PUID` and `*_PGID`. Set these to a host user/group that owns your media directories so containers can read/write without permission issues.
  * Check IDs with:

    ```bash
    id $USER
    ```

* **Ports**

  * `*_PORT_HOST` values expose container ports on your host. Change if ports conflict.

* **Tags / Versions**

  * Each image exposes a `*_TAG` (e.g., `latest`, `nightly`, or specific versions).

* **Plex**

  * Optional: `PLEX_CLAIM` token for first-run claim.

* **YouTubeDL-Material**

  * `YTDL_MONGO_URL` defaults to the internal Mongo service name.
  * You can toggle `YTDL_USE_LOCAL_DB` and `YTDL_WRITE_CONFIG` as needed.

---

## 🔒 Security & Notes


* Consider restricting ports at the firewall or bind to localhost (e.g., `127.0.0.1:8989:8989`) if reverse-proxying.
* The optional `/etc/hosts` bind is commented or optionalized—enable only if you know you need it

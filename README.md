
<p align="center"> <img src="Images/Header.png" alt="Header Images"></p>

# 🚀 Awesome Code and Configuration Boilerplates 🛠️

### Welcome! This repository provides elegant, well-structured boilerplate code and configuration examples to jumpstart self-hosted, containerized, and service-managed environments.

[![GPLv3 License](https://img.shields.io/badge/License-GPL%20v3-yellow.svg)](https://opensource.org/licenses/)

## Copy Projects Locally

Clone the project:

```bash
git clone https://github.com/Brandon-Roff/Boiler-Plates.git
cd Boiler-Plates
```

## 📑 Table of Contents
1. Boilerplate Index
2. Media Stack (Docker)
3. Selfhosted 365 (Docker)
4. Additional Stacks
5. Config Boilerplates
6. Security & Hardening
7. Roadmap
8. Release Automation
9. Contributing
10. License & Optimizations

# 1. Boilerplate Index

### 2. Media Stack

| Program | Project URL | Docker-Compose 🐳 | Systemd | Standard Port |
| :--: | :--: | :--: | :--: | :--: |
| [Bazarr 🗚](Docker/Media/Bazarr/) | https://www.bazarr.media/ | `✅` | `❌` | 6767/tcp |
| [Lidarr 🎵](Docker/Media/Lidarr/) | https://lidarr.audio/ | `✅` | `❌` | 8686/tcp |
| [Prowlarr 🌐🔗](Docker/Media/Prowlarr) | https://prowlarr.com/ | `✅` | `❌` | 9696/tcp |
| [Radarr 🎬](Docker/Media/Radarr/) | https://radarr.video/ | `✅` | `❌` | 7878/tcp |
| [Sonarr 📺](Docker/Media/Sonarr/) | https://sonarr.tv/ | `✅` | `❌` | 8989/tcp |
| [Transmission 🧲](Docker/Media/Transmission/docker-compose.yml) | https://transmissionbt.com/ | `✅` | `❌` | 9091/tcp |
| [Podgrab 🎧](Docker/Media/PodGrab/docker-compose.yml) | https://github.com/akhilrex/podgrab | `✅` | `❌` | 8787/tcp |

Install them all with the MediaBox [Docker Compose Template](Docker/Media/docker-compose.yml).

### 3. Selfhosted 365

| Program | Project URL | Docker-Compose 🐳 | Systemd | Standard Port |
| :--: | :--: | :--: | :--: | :--: |
| [Nextcloud](Docker/Selfhosted-365/Nextcloud) | https://nextcloud.com/ | `✅` | `❌` | 8080/tcp |
| [OnlyOffice](Docker/Selfhosted-365/OnlyOffice) | https://www.onlyoffice.com/en/ | `✅` | `❌` | 8081/tcp |
| [Draw.io](Docker/Selfhosted-365/Draw.io) | https://app.diagrams.net/ | `✅` | `❌` | 8082/tcp |

### 4. Additional Stacks

| Category | Path | Notes |
| :-- | :-- | :-- |
| Database | `Docker/Database/docker-compose.yml` | Add Postgres / MySQL / Redis services |
| Monitoring | `Docker/Monitoring/docker-compose.yml` | Prometheus + Grafana placeholder |
| Web | `Docker/Web/docker-compose.yml` | Generic reverse proxy starter |

### 5. Config Boilerplates

| Type | Directory | Highlights |
| :-- | :-- | :-- |
| NGINX | `Configs/NGINX/` | Single-site, multi-site, security headers |
| Apache | `Configs/Apache/` | VirtualHost examples + security |
| Systemd | `Systemd/` | Manage docker compose projects & generic apps |

### 6. Security & Hardening

| Component | Path | Purpose |
| :-- | :-- | :-- |
| Fail2Ban | `Security/Fail2Ban/` | Intrusion prevention (SSH, NGINX, Transmission) |
| Traefik Stack | `Docker/Security/docker-compose.yml` | Reverse proxy + TLS + dashboard |
| Watchtower | `Docker/Security/docker-compose.yml` | Automated image updates |
| Portainer | `Docker/Security/docker-compose.yml` | Container management UI |
| UFW | `Security/UFW.md` | Host firewall baseline rules |

Quick start (security stack):
```bash
cd Docker/Security
docker compose up -d
```

Add labels to app containers for Traefik routing (see stack README). Apply Fail2Ban filters then restart service.

## 7. 🛤️ Roadmap

- Expand Docker Compose templates (DB & Monitoring full stack)
- Add Traefik reverse proxy examples
- Add Kubernetes manifests
- Add systemd timer examples
- Provide SSL (LetsEncrypt) automation scripts

## 8. 🚀 Release Automation

Automatic releases are created on each push to `main` using `.github/workflows/auto-release.yml`.

Versioning rules (semantic-ish):
- Start at `v0.1.0` if no tag exists
- MAJOR bump for `BREAKING CHANGE` or `!` markers
- MINOR bump for any `feat:` commit
- PATCH bump otherwise

Each release contains commit subjects since the last tag. Manual trigger available via workflow dispatch.

## 9. 🤝 Contributing

1. Fork the repository
2. Create a branch: `git checkout -b feat/my-feature`
3. Commit using Conventional Commits (`feat:`, `fix:`, `docs:` etc.)
4. Push and open a Pull Request

Please keep examples minimal and well-commented.

## 10. License & Optimizations

GPLv3 — see badge above.

Optimizations depend per project.


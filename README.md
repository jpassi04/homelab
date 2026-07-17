# Homelab Infrastructure

## Overview
Self-hosted media server and personal infrastructure running on Proxmox bare metal. Multi-container stack orchestrated with Docker/Portainer, designed for media automation, backup, and monitoring.

**Status:** Active | **Last Updated:** 7/16/26
  
## What's Running

| Service | Purpose |
|---------|---------|
| **Homarr** | Personal dashboard & service portal
| **TrueNAS** | Storage (seperate hardware)
| **Jellyfin** | Media streaming
| **Sonarr** | Automated TV episode ingestion
| **Radarr** | Automated movie ingestion
| **Prowlarr** | Indexer aggregation/sync
| **qBittorrent** | Torrent client (VPN sidecar)
| **Tailscale** | Remote VPN server access
| **Vaultwarden** | Self-hosted password manager
| **Nginx Proxy Manager** | Reverse proxy
| **Prometheus** | Metrics collection
| **Grafana** | Visualization & alerting
| **Uptime Kuma** | Service health monitoring
  
---

## Key Technical Decisions

---

### VPN sidecar
qBittorrent runs securely in isolation with gluetun as a sidecar container using ProtonVPN (WireGuard). This:
- Keeps all torrent traffic encrypted without host-level VPN
- Allows other containers to bypass VPN
- Easier to manage/restart than host-level VPN

**Config:** See (add docker-compose.yml)

---

### Storage Architecture
- TrueNAS NAS mounted via SMB on Ubuntu Server at `/mnt/media`
- Sonarr/Radarr import to `/mnt/media/tv` and `/mnt/media/movies`
- Jellyfin streams directly from `/mnt/media`
- qBittorrent downloads to `/home/downloads` (local), arr suite moves to `/mnt/media` (over SMB)

---

### Monitoring Stack
Prometheus scrapes container metrics, Grafana displays them. Uptime Kuma provides external uptime monitoring on services.

---

## Lessons Learned

---

## Project Structure


---

## Future Improvements

- [ ] Add TLS to internal services (not just reverse proxy)
- [ ] Implement automated config backups to NAS
- [ ] Set up Duplicati for encrypted off-site backup
- [ ] Add Paperless-ngx for document archival
- [ ] Explore Kubernetes for orchestration

---

## Technologies Used

**OS:** Proxmox
**Containerization:** Docker, Docker Compose, Portainer  
**Storage:** TrueNAS, SMB, Docker volumes  
**Networking:** Nginx Proxy Manager, gluetun, ProtonVPN  
**Observability:** Prometheus, Grafana, Uptime Kuma  
**Media:** Jellyfin, Sonarr, Radarr, Prowlarr, qBittorrent  
**Security:** Vaultwarden, Tailscale

---

## License

This is a personal project. Feel free to use configs as reference.

# UFW (Uncomplicated Firewall) Boilerplate

Basic commands to lock down a host.

```bash
ufw default deny incoming
ufw default allow outgoing
ufw allow 22/tcp    # SSH
ufw allow 80/tcp    # HTTP
ufw allow 443/tcp   # HTTPS
ufw allow 9000/tcp  # Portainer (optional)
ufw allow 8080/tcp  # Traefik dashboard (restrict or remove in production)
ufw enable
ufw status verbose
```

To delete a rule:
```
ufw status numbered
ufw delete <number>
```

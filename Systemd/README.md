# Systemd Service Boilerplates

Example systemd unit files for managing applications.

## Files
- `docker-compose@.service` – Template to manage a docker compose project as a service.
- `generic-app.service` – Runs a simple binary or script.

## Usage
Place unit file in `/etc/systemd/system/` then:
```
systemctl daemon-reload
systemctl enable myapp.service
systemctl start myapp.service
```

For the docker-compose template:
```
# Assuming /opt/mediabox contains docker-compose.yml
systemctl enable docker-compose@mediabox.service
systemctl start docker-compose@mediabox.service
```

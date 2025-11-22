# Fail2Ban Boilerplates

Example configuration to quickly harden your self-hosted stack.

## Files
- `jail.local` – Overrides default jail settings, enabling common protections.
- `filter.d/nginx-http-auth.conf` – Detects repeated failed basic auth attempts.
- `filter.d/transmission.conf` – Bans brute-force attempts against Transmission Web UI.
- `filter.d/sshd-ddos.conf` – Extended DDoS protection for SSH.

## Usage
Copy `jail.local` to `/etc/fail2ban/jail.local` and the filter files into `/etc/fail2ban/filter.d/` then restart:
```
systemctl restart fail2ban
fail2ban-client status
```

Adjust `ignoreip` to include your LAN or VPN ranges.

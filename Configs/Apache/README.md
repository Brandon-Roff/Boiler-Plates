# Apache HTTPD Configuration Boilerplates

Example virtual host definitions and common snippets.

## Files
- `vhost-single.conf` – Single reverse proxy virtual host.
- `vhost-multisite.conf` – Multiple reverse proxy paths for media stack.
- `security.conf` – Security headers & request limiting examples.

Enable required Apache modules:
```
a2enmod proxy proxy_http headers remoteip rewrite
```

Then place files in `/etc/apache2/sites-available/` and enable:
```
a2ensite vhost-single.conf && systemctl reload apache2
```

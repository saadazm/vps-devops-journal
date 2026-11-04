# Portfolio Site Notes

## Deployment Steps

- Update the domain in `docker-compose.yml`.
- Deploy with `docker compose up -d`.
- Verify HTTPS certificate issuance.

## Security Audit (2026-W45)

- **Exposed ports** — none. Already routed through Traefik on the `proxy` network only.
- **Restart policy** — already `unless-stopped`. No change.
- **Resource limits** — added `deploy.resources.limits` (0.5 CPU / 256M memory). Starting point only — bump if the site serves heavier traffic.
- **Root user** — `nginx:alpine` runs its master process as root by default. Tested overriding to `user: nginx`: it fails startup with `mkdir() "/var/cache/nginx/client_temp" failed (13: Permission denied)` because `/var/cache/nginx` is root-owned in the image and nginx needs to bind/read config as the master process. Accepted as a known risk for now — a clean fix would mean switching to the `nginxinc/nginx-unprivileged` image (listens on 8080) instead of patching this one, which is out of scope here.


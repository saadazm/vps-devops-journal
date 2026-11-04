# Uptime Kuma Notes

## Deployment Steps

- Replace `status.example.com`.
- Deploy with `docker compose up -d`.
- Add monitors for all public services.

## Security Audit (2026-W45)

- **Exposed ports** — none. Already routed through Traefik on the `proxy` network only.
- **Restart policy** — already `unless-stopped`. No change.
- **Resource limits** — added `deploy.resources.limits` (0.5 CPU / 512M memory). Starting point only — scale up if monitoring many targets at tight intervals.
- **Root user** — `louislam/uptime-kuma:latest` runs as root by default (`docker inspect` shows empty `Config.User`; its entrypoint logs "Starting application with user 0 group 0"). The image ships a documented `PUID`/`PGID` mechanism for this instead of a plain `user:` override — the entrypoint needs to start as root once to `chown` `/app/data`, then drops to the given UID/GID via `setpriv` before launching the app. Added `PUID=1000` / `PGID=1000` and verified by running the container: logs show `changed ownership of '/app/data' from root:root to 1000:1000` then `Starting application with user 1000 group 1000`, and the app starts healthy. A bare `user: "1000:1000"` override would have skipped the `chown` step and broken writes to a fresh volume — this is why the fix goes through the image's own env vars instead.


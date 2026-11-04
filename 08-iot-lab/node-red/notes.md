# Node-RED Notes

## Deployment Notes

- Replace placeholder domain.
- Add authentication before exposing publicly.
- Back up `/data` regularly.

## Security Audit (2026-W45)

- **Exposed ports** — none. Already routed through Traefik on the `proxy` network only.
- **Restart policy** — already `unless-stopped`. No change.
- **Resource limits** — added `deploy.resources.limits` (0.5 CPU / 512M memory). Starting point only — tune up if flows are heavy or run many parallel contexts.
- **Root user** — `nodered/node-red:latest` already runs as the non-root `node-red` user by default (confirmed via `docker inspect --format='{{.Config.User}}'`). No change needed.
- Admin-auth and the example-flow setup for this stack are tracked separately — out of scope for this audit.


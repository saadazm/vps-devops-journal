# n8n Automation Notes

## Deployment Steps

- Replace placeholder domains.
- Add production credentials through `.env`.
- Deploy with `docker compose up -d`.

## Security Audit (2026-W45)

- **Exposed ports** — none. Already routed through Traefik on the `proxy` network only.
- **Restart policy** — already `unless-stopped`. No change.
- **Resource limits** — added `deploy.resources.limits` (1.0 CPU / 1G memory). n8n gets the most headroom of the lightweight stacks since workflow execution can spike memory. Starting point only — tune per actual workflow load.
- **Root user** — `n8nio/n8n:latest` already runs as the non-root `node` user by default (confirmed via `docker inspect --format='{{.Config.User}}'`). No change needed.


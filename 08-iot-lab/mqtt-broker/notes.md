# MQTT Broker Notes

## Deployment Notes

- Configure authentication before exposing MQTT outside a private network.
- Prefer TLS for public broker access.

## Security Audit (2026-W45)

- **Exposed ports** — this was the one real finding in the audit: `1883:1883` published the broker directly to the host (and from there, the VPS's public IP), with no authentication (`allow_anonymous true` in the default `mosquitto.conf`). Fixed by removing the `ports:` mapping entirely and moving the service onto its own internal `mqtt-internal` Docker network, so only other containers joined to that network can reach it — nothing on the host or the internet can.
  - **Tradeoff** — this breaks the broker's current reachability for any real MQTT client outside this Docker host (e.g. a physical IoT device on the LAN, or a sensor publishing over the internet straight to the VPS IP on port 1883). If that's an active use case, don't restore the host port mapping as-is — wait for the planned Mosquitto auth + TLS hardening (tracked separately, not part of this audit) and re-expose deliberately behind that, or route external access through a VPN/Tailscale instead of a bare published port.
  - No Mosquitto auth, TLS, or config changes were made here — that's explicitly a separate task.
- **Restart policy** — already `unless-stopped`. No change.
- **Resource limits** — added `deploy.resources.limits` (0.5 CPU / 256M memory). Mosquitto is a lightweight C binary; this is generous headroom. Starting point only.
- **Root user** — the container's top-level default user is root (`docker inspect` shows empty `Config.User`), but that's only so the entrypoint can `chown` `/mosquitto/data` on first run. Checked what the actual broker process runs as by starting it and inspecting the running process: it drops to the built-in `mosquitto` user (uid/gid 1883) before listening on 1883 — confirmed via `ps aux` inside a running container showing `mosquitto` as the process owner, not `root`. No `user:` override needed, and adding one would skip the entrypoint's one-time `chown`, breaking write permissions on a freshly created volume.


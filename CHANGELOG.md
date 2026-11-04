# Changelog

Track what changed, what was learned, and what still needs follow-up.

## 2026-W18

- Initialized VPS DevOps journal structure.

## 2026-W45

- Expanded `01-vps-setup`: added provider/provisioning notes and local SSH key setup; documented hostname and unattended security upgrades in `ubuntu-essentials.md`.
- Audited all 5 `docker-compose.yml` stacks (exposed ports, restart policies, resource limits, root-running containers): stopped `mqtt-broker` from publishing `1883` to the host (moved to an internal `mqtt-internal` network — tradeoff documented in its `notes.md`), added `deploy.resources.limits` to all 5 services, confirmed restart policies were already compliant, added `PUID`/`PGID` to `uptime-kuma` to run non-root, and confirmed `n8n`/`node-red`/`mqtt-broker`'s actual process already run non-root by default while `nginx:alpine` (portfolio-site) does not and was documented as an accepted risk.


# VPS Provisioning

## Choosing a Provider/Plan

- Pick a region close to the majority of users or the domain's audience.
- Size for the workload: Docker + Traefik + a few small apps runs fine on 1-2 vCPU / 2-4 GB RAM.
- Prefer providers that support cloud-init and SSH-key injection at creation time.

## At Creation Time

- Choose a current Ubuntu LTS image.
- Paste the **public** key (`~/.ssh/id_ed25519.pub`) into the provider's SSH key field so root login works key-only from the first boot.
- Enable any free provider backups/snapshots at creation if available.

## First Login

```bash
ssh root@<vps-ip>
```

Then follow [initial-server-hardening.md](initial-server-hardening.md) to create a non-root user and lock down SSH.

## Record Per Server

| Field | Value |
| --- | --- |
| Provider | |
| Plan / size | |
| Region | |
| Public IPv4 | |
| Created | |

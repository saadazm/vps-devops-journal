# VPS Setup

Provisioning notes for a fresh Ubuntu VPS.

## Checklist

- Provision the VPS and inject an SSH key at creation ([vps-provisioning.md](vps-provisioning.md)).
- Generate/reuse a local SSH key and add a `~/.ssh/config` alias ([local-ssh-setup.md](local-ssh-setup.md)).
- Create non-root sudo user.
- Add SSH public key authentication.
- Disable root SSH login.
- Enable UFW firewall.
- Set timezone and hostname.
- Enable unattended security upgrades.
- Add swap if the VPS has limited memory.
- Point domain DNS records to the VPS IP.

## Notes

- [vps-provisioning.md](vps-provisioning.md) — picking a provider/plan and first login.
- [local-ssh-setup.md](local-ssh-setup.md) — generating a key locally and connecting by alias.
- [initial-server-hardening.md](initial-server-hardening.md) — non-root user, SSH lockdown, firewall baseline.
- [ubuntu-essentials.md](ubuntu-essentials.md) — packages, timezone, hostname, swap, auto security updates.
- [dns-domain-setup.md](dns-domain-setup.md) — DNS records and verification.


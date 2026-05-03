# VPS Firewall Rules

## Baseline

```bash
sudo ufw allow OpenSSH
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw enable
sudo ufw status verbose
```

## Rationale

Only expose ports that are required for SSH and public web traffic.


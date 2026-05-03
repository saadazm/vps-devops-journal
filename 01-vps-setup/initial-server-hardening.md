# Initial Server Hardening

## Goals

- Use SSH keys instead of passwords.
- Disable direct root login.
- Allow only required ports.
- Keep packages updated.

## Baseline Commands

```bash
sudo apt update && sudo apt upgrade -y
sudo adduser deploy
sudo usermod -aG sudo deploy
```

## SSH Hardening

Edit `/etc/ssh/sshd_config`:

```text
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
```

Restart SSH:

```bash
sudo systemctl restart ssh
```

## Firewall

```bash
sudo ufw allow OpenSSH
sudo ufw enable
sudo ufw status verbose
```


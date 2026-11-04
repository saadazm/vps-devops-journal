# Local SSH Setup

## Generate a Key (once per machine)

```bash
ssh-keygen -t ed25519 -C "deploy@local" -f ~/.ssh/id_ed25519
```

## Copy Key to Server

```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub deploy@<vps-ip>
```

If `ssh-copy-id` isn't available, append the `.pub` contents to `~/.ssh/authorized_keys` on the server manually.

## `~/.ssh/config` Alias

```text
Host vps
    HostName <vps-ip>
    User deploy
    IdentityFile ~/.ssh/id_ed25519
```

Then connect with:

```bash
ssh vps
```

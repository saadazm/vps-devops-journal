# Ubuntu Essentials

## Useful Packages

```bash
sudo apt install -y curl wget git unzip htop ncdu ufw ca-certificates gnupg lsb-release
```

## Timezone

```bash
timedatectl list-timezones
sudo timedatectl set-timezone Asia/Dhaka
```

## Swap

Create swap when memory is limited and Docker workloads may spike.

```bash
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```


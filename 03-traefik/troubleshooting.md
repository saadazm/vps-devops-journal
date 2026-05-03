# Traefik Troubleshooting

## Certificate Not Issued

- Confirm DNS points to the VPS.
- Confirm ports `80` and `443` are open.
- Check Traefik logs.
- Confirm the ACME email and resolver name are correct.

## Container Not Reachable

- Confirm the container is on the `proxy` network.
- Confirm `traefik.enable=true` is set.
- Confirm router host rule matches the requested domain.


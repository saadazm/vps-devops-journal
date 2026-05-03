# Traefik

Traefik is the reverse proxy and TLS entrypoint for Docker-hosted services.

## Typical Flow

- Public traffic enters on ports `80` and `443`.
- Traefik reads Docker labels.
- Routers match hostnames.
- Services receive traffic on internal Docker networks.
- Let's Encrypt issues certificates through ACME.


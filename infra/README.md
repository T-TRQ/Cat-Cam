# Infrastructure

Deployment plumbing for the system. Lives here so it's versioned alongside the code it deploys.

Contents (over time):
- `docker-compose.yml` and overrides for the server stack
- systemd unit files for the Pi capture service
- Tailscale ACL config
- Backup scripts
- Monitoring / log shipping config

Secrets are never committed here. Use `*.example` files for templates and keep real values in `.env` files (gitignored) or a secrets manager.

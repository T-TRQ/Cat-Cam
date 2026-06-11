# Cat Cam

A home camera surveillance system for watching my cat, built as a long-running learning project focused on network and application security.

## Status

Early development. See [CHANGELOG.md](CHANGELOG.md) for what's been built so far.

## What this is

A Raspberry Pi captures video from a USB webcam and securely sends events to a self-hosted server, which exposes a web dashboard (and eventually a mobile app) for viewing live and recorded footage.

The project is structured so that security is a first-class concern rather than an afterthought. See [docs/threat-model.md](docs/threat-model.md) and the [docs/adr/](docs/adr/) folder for the design rationale.

## Architecture (high level)

> A diagram will live here later.

- **Pi node (`pi/`)** — captures video, does motion detection, ships events to the server. Treated as a low-trust device.
- **Server (`server/`)** — API, database, auth, media storage. Runs on a self-hosted Linux machine. Authoritative.
- **Web app (`web/`)** — browser dashboard. React / Next.js. Designed mobile-friendly so iPhone users can use it via Safari without a native app.
- **Infra (`infra/`)** — Docker Compose files, systemd units, Tailscale config, deployment scripts.
- **Docs (`docs/`)** — threat model, Architecture Decision Records (ADRs), design notes.

## Getting started

> To be written when there's something to start. For now, see [JOURNAL.md](JOURNAL.md) for current status.

## Security

See [SECURITY.md](SECURITY.md) for the security policy and [docs/threat-model.md](docs/threat-model.md) for the threat model.

## License

MIT — see [LICENSE](LICENSE).

# Security Policy

## About this project

This is a personal home camera surveillance system for a single user (me). It is also a learning project focused on building secure systems from first principles. The security posture is documented in [docs/threat-model.md](docs/threat-model.md) and the design decisions that produced it are recorded in [docs/adr/](docs/adr/).

## Reporting a vulnerability

This is a personal project, but if you find a real vulnerability and want to be helpful:

- Prefer GitHub's private security advisory feature on this repo.
- Or email: [fill in once you have a contact email you're comfortable publishing]
- Please do not open a public issue for security problems.

## Scope

**In scope:** anything in this repository — application code, configs, deployment scripts, documentation.

**Out of scope:** my personal infrastructure beyond this repo, third-party services I integrate with (Tailscale, hosting providers, etc.), physical attacks on hardware I control.

## Threat model summary

See [docs/threat-model.md](docs/threat-model.md) for the full document. In short:

- The Raspberry Pi is treated as a **low-trust** device that could be physically compromised.
- The server is the **authoritative** component and holds all sensitive state.
- No service exposes ports directly to the public internet. Remote access is via Tailscale (WireGuard-based mesh VPN).
- Secrets are never committed to the repo. See `.gitignore` and `.env.example` patterns.

## Supported versions

This project follows [Semantic Versioning](https://semver.org). Only the latest released version is supported.

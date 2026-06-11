# Changelog

All notable changes to this project will be documented here.
The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

Categories used: `Added`, `Changed`, `Deprecated`, `Removed`, `Fixed`, `Security`.

## [Unreleased]

### Added
- Initial repository scaffolding (README, LICENSE, .gitignore, SECURITY.md).
- ADR process (`docs/adr/`) with meta-ADR establishing the convention.
- Threat model template (`docs/threat-model.md`).
- Development journal (`JOURNAL.md`).

---

<!--
Example of how a release entry will look once you tag v0.1.0:

## [0.1.0] - 2026-MM-DD — Hardware loop

### Added
- Pi captures a single JPEG from the USB webcam using `fswebcam`.
- SSH key-only login on the Pi; password auth disabled.
- `ufw` baseline firewall config (default deny, allow SSH from LAN only).

### Security
- Documented baseline Pi hardening in `docs/adr/0002-pi-baseline-hardening.md`.

[Unreleased]: https://github.com/USERNAME/REPO/compare/v0.1.0...HEAD
[0.1.0]: https://github.com/USERNAME/REPO/releases/tag/v0.1.0
-->

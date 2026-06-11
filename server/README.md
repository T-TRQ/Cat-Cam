# Server

The authoritative backend. Runs on the laptop (Ubuntu Server). Responsibilities:

- API (planned: FastAPI)
- Database (planned: PostgreSQL)
- Authentication and session management — see `auth/` once it exists
- Media storage and retention
- Reverse proxy (Caddy or Nginx) for TLS termination
- AI object detection (later, using the GPU)

This is the **high-trust** component of the system. Compromise here is catastrophic; the threat model is built around making that hard. See [../docs/threat-model.md](../docs/threat-model.md).

## Subfolders

(To be added as code is written.)

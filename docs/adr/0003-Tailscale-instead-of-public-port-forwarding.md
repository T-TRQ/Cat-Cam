# ADR-0003: Tailscale instead of public port forwarding

**Status:** Accepted
**Date:** 2026-06-18

## Context

The system needs a way for the user to interact with it without being on the same network. Considering the security vulnerabilities that comes with port forwarding, the system needs to stay local while still being available to a select few authenticated users outside the network. As stated in the threat model, open ports gets scanned within minutes which adds attack surface.

## Decision

Both the PI and the server as well as the user devices will run a Tailscale or equivalent client to circumvent the need for port forwarding. Tailscale allows up to 100 devices for free which is considerably more than needed. Tailscale ACLs will also be configured to restrict device-to-device access (will be referenced in later ADR if needed).  

## Consequences

The most important consequence is what is gained: no public attack surface, only trusted devices can reach the server, MagicDNS makes hostnames easier to remember than IPs. 

The honest downsides:

The system is now dependent on Tailscales control plane. If Tailscales coordination servers go down, devices cant join the network or re-authenticate.

A lot of trust is now placed on Tailscale the company. Their software is on every device in the trust zone. If they are compromised, so is the system.

A second device thats compromised on the tailnet, effectively has LAN-equivalent access to the server. The tailnet is one big trust zone unless carved up with ACLs.

## Alternatives Considered

Public port forwarding with strong auth. Simpler infra, no third party. Rejected because the attack surface is huge and the threat model explicitly excludes internet-exposed services.

Raw WireGuard set up manually. Same security properties as Tailscale but no third-party dependency. Rejected because the operational overhead (key management, peer config, NAT traversal) is significant and Tailscale solves it well enough that the simplicity gain is worth the trust dependency.

Cloudflare Tunnel or similar reverse-tunnel services. Server makes outbound connection to Cloudflare, Cloudflare exposes a public URL. Different trade-off Cloudflare sees all the traffic, Tailscale doesn't see the data plane. Rejected because the threat model prefers peer-to-peer encrypted access over a third-party seeing the bytes.
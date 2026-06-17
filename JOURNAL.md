# Development Journal

A running log of what I worked on, decisions I made, things I tried, things that broke.

---

## 2026-05-13 — Project kickoff

Set up the repo skeleton. Read through OWASP ASVS section on authentication (V2).

Decided to write the threat model before writing any code as well as ADR-0002 and ADR-0003, so the design decisions have something to point at.

**Open questions for next session:**
- Does the Pi go on the main wifi or on a guest VLAN? My router supports VLANs but I've never configured one.
- Device authentication: mTLS or a long-lived signed token? mTLS is "more correct" but cert rotation for a single device feels like a lot.
- Do I want the server to be reachable from outside the tailnet at all? Probably not for v1.

---
